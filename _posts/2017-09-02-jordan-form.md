---
layout: post
title: "Jordan Normal Form"
date:   2017-09-2
---

# Introduction
In linear algebra, diagonalizing a matrix is very important for numerical reasons, but there are 
numerous cases that diagonaliing a matrix is not possible.
Jordan Normal Form (or Jordan Canonical Form) is a way to represent a matrix 
in its most diagonalizable form.  
This post serves to better understand what JNF is accomplishing mathematically. 
Note that JNF is not actually used for numerical purposes.

## A matrix in JNF
A matrix JNF will look something like 
\\(\begin{bmatrix}
J_1    & 0      & \cdots & 0 \\\
0      & J_2    & \cdots & 0 \\\
\vdots & \vdots & \ddots & \vdots \\\
0      & 0      & \cdots & J_k 
\end{bmatrix}\\) where each \\(J_i\\) is a jordan block.   
Each jordan block \\(J_i\\) has some value \\(\lambda_i\\) down the diagonal 
and ones above the diagonal.  
A \\(3\times 3\\) jordan block will look like 
\\(\begin{bmatrix}
\lambda & 1      & 0\\\
0       & \lambda & 1 \\\
0       & 0      & \lambda 
\end{bmatrix} \\)  
If a linear transformation is diagonalizable, then the JNF of the transformation
is simply the diagonalization of that matrix.  
Each jordan block will be a \\(1\times 1\\)
block. 

## Generalized Eigenvectors and Eigenspaces
A eigenvector \\(\vec{v}\\) and eigenvalue \\(\lambda\\) of a linear 
transformation \\(A\\) are values that are values that satisfy 
the equation \\(A\vec{v} =\lambda \vec{v}\\) or the equivalent equation
\\((A-\lambda I)\vec{v} = \vec{0}\\).

Generalized eigenvectors are a more general version of eigenvectors.
A generalized eigenvector of rank \\(n\\) is a vector \\(\vec{v}\\) 
that satisfies the equation \\((A-\lambda I)^n\vec{v} = \vec{0}\\) and
\\((A-\lambda I)^{n-1}\vec{v}\neq \vec{0}\\).
Given a specific \\(\lambda\\), the span of all eigenvectors for that \\(\lambda\\)
is the generalized eigenspace for \\(\lambda\\).

In some cases, using generalized eigenvectors and eigenspaces is nicer than 
just eigenvectors.  It turns out that for a linear transformation on a vector space like 
\\(\mathbb{C}^n\\), we can find \\(n\\) independent generalized eigenvectors.
As it will be shown later, generalized eigenvectors and eigenspaces are closely
related with JNF.

## JNF for Nilpotent maps  
A nilpotent transformation is a linear transforation \\(T\\) s.t. 
\\(T^n = 0\\) for some value \\(n\\).
An example of a nilpotent matrix is 
\\(\begin{bmatrix}
0 & 1 & 0 & 0 \\\
0 & 0 & 1 & 0 \\\
0 & 0 & 0 & 0 \\\
0 & 0 & 0 & 0 
\end{bmatrix}\\)  
In this matrix, we see two chains: \\(e_3\mapsto e_2\mapsto e_1\mapsto 0\\)
and \\(e_4 \mapsto 0\\).

It turns out that by choosing the right basis, any nilpotent transformation 
can be expressed as these chains that
terminate in 0, and we can thus characterize the JNF of nilpotent transformations quickly.

If \\(T:V\to V\\) is a nilpotent map, then we can express \\(V\\) as a direct sum
\\(V = V_1\oplus V_2 \oplus \cdots \oplus V_k\\) where a basis of the form
\\(v_i,\ Tv_i,\ T^2v_i,\ \ldots,\ T^{dim V_i - 1}v_i\\) can be found for each \\(V_i\\).

This can be proven with strong induction.  
Suppose that \\(T\\) sends everything to 0. 
Then, any basis for \\(T\\) will do, and we will have \\(dim(V)\\) chains.  
If \\(T\\) does not send \\(V\\) to zero, then consider \\(W = T(V)\\).  
Since \\(T\\) is nilpotent, \\(dim(W) < dim(V)\\) and we can apply the inductive 
hypothesis to find a basis for \\(W\\):
\\( \\{T \vec{v}_1, T^2\vec{v}_1,\ldots, T^{dim(W_1)-1}\vec{v}_1\\\
\ \ T\vec{v}_2, T^2\vec{v}_2,\ldots, T^{dim(W_2)-1}\vec{v}_2  \\\
\ \ \ \vdots \\\
\ \ T\vec{v}_k, T^2\vec{v}_k, \ldots, T^{dim(W_k)-1}\vec{v}_k\\}\\)

Notice that each \\(T^{dim(W_i)-1}v_i\\) is in the nullspace of \\(T\\) and we can 
complete the nullspace of \\(T\\) with \\(dim(N(T)) - k\\) vectors 
\\(\\{ u_1, \ldots, u_{dim(N(T)) - k}\\}\\).  
We can also extend the basis for \\(W\\) with \\(\\{v_1,\ldots, v_k\\}\\) to 
get a whole basis for \\(V - N(T)\\).   
Thus, the basis for \\(W\\) combined with \\(\\{u_1,\ldots, u_{dim(N(T)) - k}, 
v_1,\ldots, v_k\\}\\)
form a basis for \\(V\\).
This proves the claim.

Thus, by choosing the right basis for \\(V\\), any nilpotent matrix can 
be expressed in JNF as a matrix filled with zeros and having occasional ones above the 
diagonal.  

## Splitting T into smaller nilpotent maps
Suppose we are given a linear transformation \\(T\\) over a finite dimensional 
vector space \\(V\\).
It is possible to split the space \\(V\\) into a direct sum of smaller spaces
\\(V = V_1\oplus V_2\oplus \cdots\oplus V_k\\) s.t. \\( T(V_i) = V_i\\) and each
\\(V_i\\) can't be split into the direct sum of smaller subspaces.  
In some sense, \\(V_1\oplus\cdots\oplus V_k\\) is the finest way to split \\(V\\) into
a direct sum of smaller vector spaces while having \\(T(V_i) = V_i\\).

Consider \\(T\mid_{V_i}: V_i\to V_i\\), the linear transformation \\(T\\) restricted 
to \\(V_i\\).  By how the \\(V_i\\)'s are constructed, there must be some 
eigenvector \\(\vec{v}\\) and eigenvalue \\(\lambda_i\\) associated with \\(T\mid_{V_i}\\).

Now, I claim that \\(\exists N\\) for any linear transformation \\(T:V\to V\\) s.t. 
\\(Im(T^N)\oplus N(T^N) = V\\)

Proof:  
Consider the sequence \\(T, T^2, T^3,\ldots \\)
Notice that \\(N(T^m)\subset N(T^{m+1})\\), meaning that the 
dimension of the nullspaces of \\(T^n\\) form a non-decreasing sequence
bouded by the dimension of \\(V_i\\). 
Then, there must be some point in the sequence where the dimension of the nullspaces
are all constant, and thus must all coincide.  
Suppose that \\(T^n\\) and \\(T^{n+1}\\) have the same nullspace.
Then, \\(T(Im(T^n)) = Im(T^n)\\) and \\(T(N(T^n)) = N(T^n)\\).
i.e.  \\(Im(T^n)\oplus N(T^n) = V\\) and we prove the claim.


Now if we apply this lemma to \\(T\mid_{V_i}-\lambda_i I\\) from earlier, we see that 
\\(Im((T\mid_{V_i}-\lambda_i I)^N)\oplus N((T\mid_{V_i}-\lambda_i I)^N) = V_i\\).  
However, by how the \\(V_i\\)'s are constructed, this is only possible if either
\\(Im((T\mid_{V_i})-\lambda_i I)^N\\) or \\(N((T\mid_{V_i}-\lambda_i I)^N)\\) is 
only \\(\\{\vec{0}\\}\\).  
Since we know \\(\vec{v}\\) is an eigenvector of \\(T\mid_{V_i}\\), 
\\(Im((T\mid_{V_i})^N) = \\{\vec{0}\\}\\). 
Thus, for each \\(i\\), \\(T\mid_{V_i} - \lambda_i I\\) is a nilpotent map.


## Combining it all together.
Since \\(T\mid_{V_i}-\lambda_i I\\) is a nilpotent map, we can find a basis for
\\(V_i\\) in the form \\( \vec{v},\ T\vec{v},\ T^2\vec{v},\ \ldots,\ T^{n-1}\vec{v}\\).
If we set this as the basis for \\(V_i,\ T\mid_{V_i}\\) will look like
\\(\begin{bmatrix} 
\lambda_i & 1         & 0         & \cdots & 0 \\\
0         & \lambda_i & 1         & \cdots & 0\\\
0         & 0         & \lambda_i & \cdots & 0 \\\
\vdots    &  \vdots   & \vdots    & \ddots & \vdots\\\
0         & 0         &  0        & \cdots & \lambda_i  
\end{bmatrix}\\)  

This looks exactly like a jordan block in the jordan normal form of a matrix!  
Also note that the chosen basis vectors are all generalized eigenvectors, and 
each \\(V_i\\) is really a generalized eigenspace!

By choosing a basis for each \\(V_i\\) composed of the generalized eigenvectors,
we can construct a basis for \\(V\\) s.t. the linear transformation \\(T\\)
can be represented in matrix form as
\\(\begin{bmatrix}
J_1 & 0 & \cdots & 0 \\\
0   & J_2 & \cdots & 0\\\
\vdots & \vdots & \ddots & \vdots \\\
0      &   0    &   \cdots& J_k 
\end{bmatrix}\\)
which is the JNF of the linear transformation.

## Applying JNF to Cayley-Hamilton
The characteristic polynomial of a matrix \\(A\\) is 
\\(p_A(x) = \det(A - x I)\\).

The Cayley-Hamilton theorem states that \\(p_A(A) = 0\\)  
i.e.  Applying the characteristic polynomial of any matrix to the matrix
itself gives the zero map.

This can be explained rather easily with the JNF of any matrix \\(T_J\\).
If we express a linear transformation with its JNF matrix, the characteristic
polynomial becomes \\(\Pi_i (\lambda_i - x)^{n_i}\\).  
Since \\((\lambda_i - T_J)^{n_i}\\) is the zero map for some generalized eigenspace, 
the characteristic polynomial is the product of all the zero maps for all the 
generalized eigenspaces and must be the zero map overall.
Thus, \\(p_{T_J}(T_J) = 0\\)
