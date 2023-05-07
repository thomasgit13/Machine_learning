# Kernels 
**Briefly speaking**, a kernel is a shortcut that helps us do certain calculation faster which otherwise would involve computations in higher dimensional space.

**Mathematical definition**: K(x, y) = <f(x), f(y)>. Here K is the kernel function, x, y are n dimensional inputs. f is a map from n-dimension to m-dimension space. < x,y> denotes the dot product. usually m is much larger than n.

**Intuition**: normally calculating <f(x), f(y)> requires us to calculate f(x), f(y) first, and then do the dot product. These two computation steps can be quite expensive as they involve manipulations in m dimensional space, where m can be a large number. But after all the trouble of going to the high dimensional space, the result of the dot product is really a scalar: we come back to one-dimensional space again! Now, the question we have is: do we really need to go through all the trouble to get this one number? do we really have to go to the m-dimensional space? The answer is no, if you find a clever kernel.

**Simple Example:** x = (x1, x2, x3); y = (y1, y2, y3). Then for the function f(x) = (x1x1, x1x2, x1x3, x2x1, x2x2, x2x3, x3x1, x3x2, x3x3), the kernel is K(x, y ) = (<x, y>)^2.

Let's plug in some numbers to make this more intuitive: suppose x = (1, 2, 3); y = (4, 5, 6). 

f(x) = (1, 2, 3, 2, 4, 6, 3, 6, 9)

f(y) = (16, 20, 24, 20, 25, 30, 24, 30, 36)

<f(x), f(y)> = 16 + 40 + 72 + 40 + 100+ 180 + 72 + 180 + 324 = 1024

A lot of algebra. Mainly because f is a mapping from 3-dimensional to 9 dimensional space.

Now let us use the kernel instead

K(x, y) = (4 + 10 + 18 ) ^2 = 32^2 = 1024

Same result, but this calculation is so much easier.

**Additional beauty of Kernel:** kernels allow us to do stuff in infinite dimensions! Sometimes going to higher dimension is not just computationally expensive, but also impossible. f(x) can be a mapping from n dimension to infinite dimension which we may have little idea of how to deal with. Then kernel gives us a wonderful shortcut.

**Relation to SVM:** now how is related to SVM? The idea of SVM is that y = w phi(x) +b, where w is the weight, phi is the feature vector, and b is the bias. if y> 0, then we classify datum to class 1, else to class 0. We want to find a set of weight and bias such that the margin is maximized. Previous answers mention that kernel makes data linearly separable for SVM. I think a more precise way to put this is, *kernels do not make the data linearly separable. The feature vector phi(x) makes the data linearly separable*. Kernel is to make the calculation process faster and easier, especially when the feature vector phi is of very high dimension (for example, x1, x2, x3, ..., x_D^n, x1^2, x2^2, ...., x_D^2).

**Why it can also be understood as a measure of similarity:** if we put the definition of kernel above, <f(x), f(y)>, in the context of SVM and feature vectors, it becomes <phi(x), phi(y)>. The inner product means the projection of phi(x) onto phi(y). or colloquially, how much overlap do x and y have in their feature space. In other words, how similar they are.

In machine learning, a kernel refers to a method that allows us to **apply linear classifiers to non-linear problems by mapping non-linear data into a higher-dimensional space without the need to visit or understand that higher-dimensional space.**