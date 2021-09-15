# CryptoBears repo
This is the repository for the cennznet grant => https://gitcoin.co/issue/cennznet/grants/9/100026471    
In this repo you will find the CryptoBears [artwork](https://github.com/ongmorel/CryptoBears/tree/main/100_bears_generated), the different [traits](https://github.com/ongmorel/CryptoBears/tree/main/differenttraitsbytype.md) possible, a presentation and an overview of the techniques used to create the CryptoBears ⬇below ⬇.   

# Presentation

__CryptoBears are 100 bears in pixelart generated randomly with python.__   
__They are all differents!__  
<img src="https://github.com/ongmorel/CryptoBears/tree/main/CryptoBearsGif.gif" alt="gif"/>

# Technical Overview

This is the technical overview of how the bears are generated , don't hesitate to fork this project !

The entire project is write in __python__ and use several library :  

* [NUMPY](https://numpy.org/) for the array
* [PIL](https://pillow.readthedocs.io/en/stable/) for the image render  
* __OS__ for the path
* __RANDOM__ for the pseudo random generation (we use seed)

Now lets dive in it!

All the bears are a numpy array with one word is equal to one pixel (bg = background, sk = skin...) :  

*for exemple this is the basicbearschema*
 <font size="0.04">
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
<img src="https://github.com/ongmorel/CryptoBears/blob/main/100_bears_generated/BearIndex5.png" alt="basicbear" width="200"/>
2. panda  
<img src="https://github.com/ongmorel/CryptoBears/blob/main/100_bears_generated/BearIndex34.png" alt="panda" width="200"/>
3. astrobear  
<img src="https://github.com/ongmorel/CryptoBears/blob/main/100_bears_generated/BearIndex28.png" alt="astrobear" width="200"/>
4. rainbowbear  
<img src="https://github.com/ongmorel/CryptoBears/blob/main/100_bears_generated/BearIndex48.png" alt="rainbowbear" width="200"/>

They have different traits but also common traits like background , cigarette...

All the traits are choosen pseudo randomly  
Why pseudo randomly ?  
Cause we use seed() of the RANDOM library for randomize traits  
Seed mean that if we do a randint(1, 1000) with the same seed the result will be the same.  
Exemple of how the typeofbear (bear schema) is choose :  

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

(The initial seed is the blocknumber when i have started the project + the index of the bear)  

__But like you can see , certain traits are more rare than other (the rainbow bear have only 4% instead of 70% for the basic bear!)__  
You can see all the different traits for all the bears plus an explanation of special traits [here](https://github.com/ongmorel/CryptoBears/blob/main/differenttraitsbytype.md)
We use the same process for all the traits (except astrobear background and skin color (border)) :  
*exemple of how the mouth size is choose*  

```python
    mouthprob = randint(1, 100)
    #cigprob is used after for choose if the bear generated have a cigare or not
    cigprob = randint(1, 200)
    if mouthprob == 100:
        mouthtype = "bigmouth"
        m1 = (0, 0, 0)
        m2 = (0, 0, 0)
        m3 = (0, 0, 0)
        m4 = (0, 0, 0)
        m5 = (0, 0, 0)
        print("bigmouth")
    elif mouthprob <= 80:
        if mouthprob <= 70:
            mouthtype = "mouth3"
            m1 = (0, 0, 0)
            m2 = (0, 0, 0)
            m3 = (0, 0, 0)
            m4 = (cx)
            m5 = (cx)
        else:
            mouthtype = "mouth2"
            m1 = (0, 0, 0)
            m2 = (0, 0, 0)
            m3 = (cx)
            m4 = (cx)
            m5 = (cx)
    elif mouthprob > 80:
            mouthtype = "nomouth"
            m1 = (cx)
            m2 = (cx)
            m3 = (cx)
            m4 = (cx)
            m5 = (cx)
```


After the schema is chosen and all the traits generated we use [PIL](https://pillow.readthedocs.io/en/stable/) for render and save the numpy array in a png image :  

```python
    #first choose the typeofbear array and resize it
    array = np.array(typeofbear, dtype=np.uint8)
    new_image = Image.fromarray(array)
    new_image = new_image.resize(dimensions, resample=0)
    
    #finally save the images in the bears_images directory
    imagename = dirname + '/bears_images/' + "BearIndex" + (str(index)) + '.png'
    new_image.save(imagename)
```

And wrap all the process in a :
```python
for loop in range(NumberYouWantToGenerated):
    #Put here the process explain above
```

Run the script and that's it !
The bears are generated with different traits choosen randomly and with rarity!!!!
You can see 100 hundreds of bears generated by my script in [BearsImage](https://github.com/ongmorel/CryptoBears/tree/main/100_bears_generated)  

Special thanks to : 

* HammerMikk#5766 for answer to me question about the grant  
* https://twitter.com/NFTBirds for inspiration and for make awesome opensource project  
* Cennznet for the opportunity  

Below i show you my top 10 CryptoBears in the 100 generated :  

1. An astrobear with a cross , look so rare !  
<img src="https://github.com/ongmorel/CryptoBears/blob/main/100_bears_generated/BearIndex89.png" alt="basicbear" width="300"/> 
2. Evidently the rainbow bear  
<img src="https://github.com/ongmorel/CryptoBears/blob/main/100_bears_generated/BearIndex48.png" alt="basicbear" width="300"/>
3. A panda with cigarette and smoke , awesome!  
<img src="https://github.com/ongmorel/CryptoBears/blob/main/100_bears_generated/BearIndex40.png" alt="basicbear" width="300"/>
4. Glasses look so fun  
<img src="https://github.com/ongmorel/CryptoBears/blob/main/100_bears_generated/BearIndex35.png" alt="basicbear" width="300"/>
5. The tail isnt the same color than the fur , a mutation!  
<img src="https://github.com/ongmorel/CryptoBears/blob/main/100_bears_generated/BearIndex93.png" alt="basicbear" width="300"/>
6. With the panda glasses he look like a real panda!  
<img src="https://github.com/ongmorel/CryptoBears/blob/main/100_bears_generated/BearIndex67.png" alt="basicbear" width="300"/>
7. He cross look so cool with this fur 
<img src="https://github.com/ongmorel/CryptoBears/blob/main/100_bears_generated/BearIndex24.png" alt="basicbear" width="300"/>
8. Sorry but i love so much the cross
<img src="https://github.com/ongmorel/CryptoBears/blob/main/100_bears_generated/BearIndex90.png" alt="basicbear" width="300"/>
9. White astrobear with a BIG smile!  
<img src="https://github.com/ongmorel/CryptoBears/blob/main/100_bears_generated/BearIndex28.png" alt="basicbear" width="300"/>
10. Love astrobear so much and extra he come from nederland  
<img src="https://github.com/ongmorel/CryptoBears/blob/main/100_bears_generated/BearIndex13.png" alt="basicbear" width="300"/>

If you want to support me follow me on [twitter](https://twitter.com/cryptotedybeir)