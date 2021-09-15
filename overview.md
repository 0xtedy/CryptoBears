# Technical Overview

This is the technical overview of how the bears are generated , don't hesitate to fork this project !

The entire project is write in __python__ and use several library :  

* [NUMPY](https://numpy.org/) for the array
* [PIL](https://pillow.readthedocs.io/en/stable/) for the image render  
* __OS__ for the path
* __RANDOM__ for the pseudo random generation (we use seed)

So lets dive in it!

All the bears are a numpy array with one word is equal to one pixel (bg = background, sk = skin...) :  

*for exemple this is the basicbearschema*
 <font size="1">
```python

        [bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg,],
        [bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg,],
        [bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg,],
        [bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg,],
        [bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg,],
        [bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg,],
        [bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg,],
        [bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg,],
        [bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg,],
        [bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, sk, sk, bg, bg, sk, sk, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg,],
        [bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, sk, sk, sk, sk, sk, bg, bg, bg, sk, cx, sk, sk, sk, cx, cx, sk, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg,],
        [bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, sk, sk, sk, cx, cx, cx, cx, cx, sk, sk, sk, cx, hr, cx, cx, cx, cx, hr, sk, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg,],
        [bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, sk, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cr, cx, cx, cx, cx, cx, cx, sk, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg,],
        [bg, bg, bg, bg, bg, bg, bg, bg, bg, sk, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cr, cr, cr, gl, cx, cx, cx, gl, sk, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg,],
        [bg, bg, bg, bg, bg, bg, bg, bg, bg, sk, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cr, gl, e1, gl, gl, gl, e2, gl, sk, bg, bg, bg, bg, sm, bg, bg, bg, bg,],
        [bg, bg, bg, bg, bg, bg, bg, bg, sk, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cr, cx, gl, cx, ns, ns, gl, cx, cx, sk, bg, bg, sm, bg, bg, bg, bg, bg,],
        [bg, bg, bg, bg, bg, bg, bg, tl, sk, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, sk, bg, bg, sm, bg, bg, bg, bg, bg,],
        [bg, bg, bg, bg, bg, bg, bg, tl, sk, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, m1, cx, cx, cx, m5, cx, cx, sk, bg, sm, bg, bg, bg, bg, bg, bg,],
        [bg, bg, bg, bg, bg, bg, bg, bg, sk, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, m2, m3, m4, cg, cg, c2, c3, c4, bg, bg, bg, bg, bg, bg, bg,],
        [bg, bg, bg, bg, bg, bg, bg, bg, bg, sk, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, cx, sk, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg,],
        [bg, bg, bg, bg, bg, bg, bg, bg, bg, sk, cx, cx, cx, sk, cx, cx, cx, cx, cx, cx, cx, cx, cx, sk, cx, cx, cx, sk, sk, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg,],
        [bg, bg, bg, bg, bg, bg, bg, bg, bg, sk, cx, cx, cx, sk, sk, sk, sk, sk, sk, sk, cx, cx, cx, sk, sk, sk, sk, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg,],
        [bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, sk, cx, cx, sk, cx, cx, sk, bg, bg, sk, cx, cx, sk, cx, cx, sk, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg,],
        [bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, sk, cx, cx, sk, cx, cx, sk, bg, bg, sk, cx, cx, sk, cx, cx, sk, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg,],
        [bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, sk, sk, bg, sk, sk, bg, bg, bg, sk, sk, sk, bg, sk, sk, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg,],
        [bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg,],
        [bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg,],
        [bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg,],
        [bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg,],
        [bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg,],
        [bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg,],
        [bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg,],
        [bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg,],
        [bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg, bg,]
```
</font>

But certain traits override other traits , so it's more simple to just create several schema.  
That's why we create 4 schema :  

1. basicbear  
<img src="https://github.com/ongmorel/crypto-bears-cennznet/blob/main/100_bears_generated/BearIndex5.png" alt="basicbear" width="200"/>
2. panda  
<img src="https://github.com/ongmorel/crypto-bears-cennznet/blob/main/100_bears_generated/BearIndex34.png" alt="panda" width="200"/>
3. astrobear  
<img src="https://github.com/ongmorel/crypto-bears-cennznet/blob/main/100_bears_generated/BearIndex28.png" alt="astrobear" width="200"/>
4. rainbowbear  
<img src="https://github.com/ongmorel/crypto-bears-cennznet/blob/main/100_bears_generated/BearIndex48.png" alt="rainbowbear" width="200"/>




We say its pseudo random cause we use seed() for randomize traits :  
*exemple of how the typeofbear is choose*

```python
 typeofbearprob = randint(1, 1000)  
    if typeofbearprob <= 700:
        schem = "basicbearschem"
    elif typeofbearprob <= 900:
        schem = "pandaschem"
    elif typeofbearprob <= 960:
        schem = "astrobearschem"
    else:
        schem = "rainbowbearschem"
    seedb = randint(1, 1000)
    seed(seedb)
```

The initial seed is the blocknumber when i have started the project.

Like you see above they are 4 different bear schema :

1. basicbear
2. panda
3. astrobear
4. rainbowbear

The schemas are a numpy array with one word is equal to one pixel (bg = background, sk = skin...) :  


After the schema is chosen we use [PIL](https://pillow.readthedocs.io/en/stable/) for render and save the numpy array in a png image :  

```python
    array = np.array(typeofbear, dtype=np.uint8)
    new_image = Image.fromarray(array)
    new_image = new_image.resize(dimensions, resample=0)

    //choose the typeofbear array and resize it

    imagename = dirname + '/bears_images/' + "BearIndex" + (str(index)) + '.png'
    new_image.save(imagename)
    //save the images in the bears_images directory
```


