---
title: "Functional programming- Java-script example 1"
category:
  - Java-script
tags:
  - Java-script
use_math: true
---

## Functional programming- Java-script example 1
Firstly, making a data structure as below.

```java
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>category_classification</title>
</head>
<body>
<script>

var data = [
  { class: 1, name: 'Fault-a1', signal_peak: 0 },
  { class: 1, name: 'Fault-a2', signal_peak: 0 },
  { class: 2, name: 'Fault-b1', signal_peak: 5 },
  { class: 2, name: 'Fault-b2', signal_peak: 5 },
  { class: 2, name: 'Fault-b3', signal_peak: 6 },
  { class: 3, name: 'Fault-c1', signal_peak: 5 },
  { class: 3, name: 'Fault-c2', signal_peak: 20 },
  { class: 3, name: 'Fault-c3', signal_peak: 25 }
];
```

<mark style='background-color: #f1f8ff'>_iterator_basic </mark>  : It's for testing a simple function.

<mark style='background-color: #f1f8ff'>_iterator </mark>  : It's for testing functions containing outer and inner functions  with real-world data.

<mark style='background-color: #f1f8ff'>_dataselect</mark>  : It's for testing a simple function with real-world data.

```javascript
function _printing_basic(list, action_to_iter) {
    action_to_iter;
}

function _iterator(list, action_to_iter) {
    for (var i = 0; i < list.length; i++) {
        action_to_iter(list[i]);
    }
    return list;
}

function _dataselect(list, action) {
    var selected_data = [];
    _iterator(list, function(val) {if (action(val)) selected_data.push(val); });
    return selected_data;
}
```

using a **_printing_basic** function, we can obtain a simple printed sentence. To be printed sentence can be determined in the below code.

```javascript
console.log( _printing_basic(data, console.log( 'hello, this is for testing') ));
```

using a **_dataselect** function, we can obtain the data which are matched with **function(data) { return data.name == 'Fault-a1'; })** function.

```javascript
console.log( _dataselect(data, function(data) { return data.name == 'Fault-a1'; }) );
```

It's similar example with above one. We can obtain the data which are matched with **function(data) { return data.signal_peak > 15; }** function.

```javascript
console.log( _dataselect(data, function(data) { return data.signal_peak > 15; }));
</script>
</body>
</html>
```

## Results of above example 1
![image](https://user-images.githubusercontent.com/71545160/132465805-6b2c12ed-a7bd-4fe9-8dfa-a1284dec5966.png)

