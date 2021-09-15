# Technical Overview

This is the technical overview of how the bears are generated , don't hesitate to fork this project !

The entire project is write in __python__ and use several library :

* [NUMPY](https://numpy.org/) for the array
* [PIL](https://pillow.readthedocs.io/en/stable/) for the image render  
* __OS__ for the path
* __RANDOM__ for the pseudo random generation (we use seed)

We say its pseudo random cause we use seed() for randomize traits:
*exemple of how the typeofbear is choose*

> typeofbearprob = randint(1, 1000)
>    if typeofbearprob <= 700:
>        schem = "basicbearschem"
>    elif typeofbearprob <= 900:
>        schem = "pandaschem"
>    elif typeofbearprob <= 960:
>        schem = "astrobearschem"
>    else:
>        schem = "rainbowbearschem"
>
>    seedb = randint(1, 1000)
>    seed(seedb)

The initial seed is the blocknumber when i have started the project.

