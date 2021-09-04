---
title: "For inputting formulas on the Github"
category:
  - Github
tags:
  - HTML
---
## For inputting formulas on the Github

#### For an in-line formula

1. Modify <mark style='background-color: #f1f8ff'>_config.yml </mark>  as below.

```html
# Conversion
markdown: kramdown
highlighter: rouge
lsi: false
excerpt_separator: "\n\n"
incremental: false

```

2. Include <mark style='background-color: #f1f8ff'>mathjax_support.html </mark>  in the <mark style='background-color: #f1f8ff'>_inlcudes</mark> folder.

```html
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
    TeX: {
      equationNumbers: {
        autoNumber: "AMS"
      }
    },
    tex2jax: {
    inlineMath: [ ['$', '$'] ],
    displayMath: [ ['$$', '$$'] ],
    processEscapes: true,
  }
});
MathJax.Hub.Register.MessageHook("Math Processing Error",function (message) {
	  alert("Math Processing Error: "+message[1]);
	});
MathJax.Hub.Register.MessageHook("TeX Jax - parse error",function (message) {
	  alert("Math Processing Error: "+message[1]);
	});
</script>
<script type="text/javascript" async
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>
```

3. Insert codes like below, on the <mark style='background-color: #f1f8ff'>layout/default.html</mark> 
```html
<head>
    {% if page.use_math %}
      {% include mathjax_support.html %}
    {% endif %}
    {% include head.html %}
    {% include head/custom.html %}
</head>
```html

4. When postings, insert <mark style='background-color: #f1f8ff'>use_math: true</mark> 

```html
---
title:  'log 와 ln'
categories:
  - Math
tags: [Math]
use_math: true
---
```

it makes github work  <mark style='background-color: #f1f8ff'>& --  &.



#### For an display a formula

In fact, above setting is enough to insert formulas 'in-line' or 'display' way.

But strangely, i couldn't 'display' way using <mark style='background-color: #f1f8ff'>&& --  && </mark> 

So, I did below setting additionally.

1. Include <mark style='background-color: #f1f8ff'>Mathjax.html</mark>  in the <mark style='background-color: #f1f8ff'>_inlcudes</mark> folder.

```html
<script type="text/javascript">
  window.MathJax = {
    tex: {
      packages: ['base', 'ams']
    },
    loader: {
      load: ['ui/menu', '[tex]/ams']
    },
    startup: {
      ready() {
        MathJax.startup.defaultReady();
        const Macro = MathJax._.input.tex.Symbol.Macro;
        const MapHandler = MathJax._.input.tex.MapHandler.MapHandler;
        const Array = MathJax._.input.tex.ams.AmsMethods.default.Array;
        const env = new Macro('psmallmatrix', Array, [null, '(', ')', 'c', '.333em', '.2em', 'S', 1]);
        MapHandler.getMap('AMSmath-environment').add('psmallmatrix', env);
      }
    }
  };
</script>
<script type="text/javascript" id="MathJax-script" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js">
</script>
```

2. Include below code in the <mark style='background-color: #f1f8ff'>_layouts/default.html</mark> folder.

```html
    {% include Mathjax.html %}
```

Then, it makes also github work  <mark style='background-color: #f1f8ff'>&& --  &&</mark> .

