# slic

This is a playground for me to develop a Silly Lossless Image Codec (slic).

What problems am I interested in addressing? 

1. I need lossless compression. This is not negotiable.
2. I need an intrinsicaly *fast* algorithm.
3. I need OK compression ratios.
4. I need something that is straight-forward to implement, particularly by people who are not me
5. I need something that can reasonably be used on multi-channel images independent of the color spaces used in the image.
6. Progressive scan is desirable but not necessary
7. Support 1, 2, or 4 bytes per channel (integer pixels only)
8. Run on 64-bit architectures (to put this another way: supporting embedded targets on 8-bit micros is specifically not an
   objective)
9. Support *big* (~4billion pixels on a side) images.    

How does this work?

Encoding runs in several phases:

0. We write out headers / metadata / book-keeping information. 

1. We do integer-to-integer transformations that preserve the input signals but represent them in lower-entropy
forms. The exact details of this are still to be figured out, but my plan is to start with a Haar-like transform.

2. We compress the transformed blocks. This is where we get clever. Exactly how much more clever is still TBD. 
