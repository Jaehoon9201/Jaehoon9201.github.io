---
title: "Compressed sensing"
category:
  - Data-processing
tags:
  - [Data-processing, Matlab]
use_math: true
---

# What is a compressive sensing?

* It could be thought compressed or random measurements.
* And then inferring what the sparse representation is in the transformed basis.
* It's somewhat NP(non-polynomial) hard problem.
* If an uncompressed signal will generally be sparse in a transform basis, the **Shannon-Nyquist theorem** may be relaxed, and the signal may be reconstructed with considerably fewer measurements than given by the Nyquist rate. It's a key idea to understand the compressive sensing.



# How to do? (For reconstructing a $f$)

* [References](https://www.youtube.com/watch?v=rt5mMEmZHfs)

1. $ f = \Psi c $

   * $\Psi$ : basis

   * $c$ : "loadings" or "coefficeints of basis"
   * ![image-20220321115321090](C:\Users\HALAB_G\AppData\Roaming\Typora\typora-user-images\image-20220321115321090.png)
   * ![image-20220321115334101](C:\Users\HALAB_G\AppData\Roaming\Typora\typora-user-images\image-20220321115334101.png)

2. $ b= \Phi f $

   * $b$ : 
     * = subsample vectror 
     * = really acquired data from processor
     * = it also could be thought as a portion of $f$.
   * $\Phi$ :  measuring matrix
   * $f$ : $ f = \Psi c $
   * ![image-20220321115455657](C:\Users\HALAB_G\AppData\Roaming\Typora\typora-user-images\image-20220321115455657.png)

3. $ b= \Phi f  = \Phi \Psi c = Ac  subject to ||c||_{1}$ 

   * If we obtain $c$ , **we can reconstruct the $f$.**

# Example code



```matlab

% reference : https://www.youtube.com/watch?v=rt5mMEmZHfs
clear; close all; clc;

n = 5000;
t = linspace(0, 1/8, n);
f = sin(1394*pi*t)+sin(3266*pi*t);
figure(1); hold on;
plot(t,f);grid on;

f_dct = dct(f);
figure(2);
plot(f_dct);grid on;

%% compressed sensing
m = 500;
temp =randperm(n);
idx = temp(1:m);
tcom_idx = t(idx);
fcom = sin(1394*pi*tcom_idx)+sin(3266*pi*tcom_idx);
figure(1);
plot(tcom_idx, fcom, 'ro','LineWidth',2,'MarkerSize',2);

D = dct(eye(n,n)); 
% setup a basis(realted to A-Matrix). 
% b= Ac --> we can find 'c'
A = D(idx,:); % setup A-Matrix

%% Method 1
% x = pinv(A)*fcom';  % =Mean square error(?)


%% Method 2
cvx_begin;
    variable x(n);
    minimize(norm(x,1));
    subject to
        A*x == fcom';
cvx_end

%% plot
reconstructed_sig = dct(x);

figure(3)
plot(t, f, t, reconstructed_sig);

figure(4)
plot(f_dct, 'b'), hold on, grid on;
plot(x, 'r');
```

![image-20220321140704176](C:\Users\HALAB_G\AppData\Roaming\Typora\typora-user-images\image-20220321140704176.png)

![image-20220321140756300](C:\Users\HALAB_G\AppData\Roaming\Typora\typora-user-images\image-20220321140756300.png)
