# The-Golden-Ratio-project-documentation

#### * If you don't have experience with using VEX , don't miss the chance to learn and visit this link to give your self an idea how VEX works: https://github.com/kiryha/Houdini/wiki/vex-for-artists

* To have better understanding of what we are explaining in this project...you should have a good background about Golden Ratio
I suggest to start from here: https://en.wikipedia.org/wiki/Golden_ratio  


### But if you are Houdini user...without further ado let's get started !





#### after you start houdini :

* **First step**_______ Create   _**Geometry**_  node...dive inside of it , and create  _**Line**_  make sure you have reduced the length of the line and increased its points number:

![1](https://user-images.githubusercontent.com/53704509/81752765-dd8c2a80-94ba-11ea-9a07-69ab2e679bfc.jpg)

* **Second step**________ Create an   **_Attribute Wrangle_**  node and connect the first input of it to the previous line node's output , now...let's write some code !

A- create **PI**  and if you don't know what is PI value , just google it !
you will create it as float value ofcourse ,cause it is a decimal number :
`float  pi = 3.14159265359;`

B- create relative point position in [0,1] and call it r :
`float r = float(@ptnum) / float(@numpt - 1);`

C- now create  switch between two calculation methods( a , b ):
```
   int switch = chi('sw');
   float a = chf('a');
   float b = chf('b');

   float l = 1;
   float s = 1;
```
D- let's write some Logic here using If and else so we can create  logarithmic spiral :

* note :  ( l ) in ( if statement ) is length for (log spiral)
* note :  ( s ) is scale along r 
* note :  ( l ) in (else statement) is length for ramp
* note :  ( s ) int (else statement) is scale along r
```
    if (switch == 0)
    {
      l = chf('lenst');
      s = a * exp(b * r);
    } else
    {
      l = chf('lennd');
      s = chf('rs') * chramp('ramp',r);
    }


```
* note :  use ramp as function to modify spiral proportions

E- create Vectore call it Q to help us in what next :
`    vector Q;`
    

* note :  r --> Q(r)
* note : use l to modify the spiral windings
* note : use s to scale the circle

```
    Q[0] = s*cos(l*2*pi*r);
    Q[1] = s*sin(l*2*pi*r);
```
    
* note : another ramp to have control on the translation
* note :along the z-axis
```
    Q[2] = chf('distscale') * chramp('dist', r);
    
    @P = Q;
```

F-  You will end up with something like this :

![2](https://user-images.githubusercontent.com/53704509/81758954-fc46ed00-94cb-11ea-9dfe-0f14defb18cb.jpg)

*  **Third step**_______ change the PI value and set it to:
*  `float  pi = 4.14159265359;`  instead of float  `pi = 3.14159265359;
`

I am sure that you are wondering why , I changed PI value ! 

well , that's optional but for our project we will stick with `4,14159265359`...let me show you how it will be if we tried different numbers !

![4](https://user-images.githubusercontent.com/53704509/81958323-7f745a00-9616-11ea-87c0-d720a25c541c.jpg)

![5](https://user-images.githubusercontent.com/53704509/81958351-89965880-9616-11ea-9ac0-a6b2be95caf6.jpg)

![6](https://user-images.githubusercontent.com/53704509/81958388-961ab100-9616-11ea-8cd8-8dcbadb6f1e2.jpg)


did you notice that ?
the number of spirals increased in equal when you change **PI** value to higher number
by the way this is in 2d **Front** view ( make sure that you use the same parameters in the photo) 

* now , let's see how it looks in perspective view !
![collpers](https://user-images.githubusercontent.com/53704509/81959852-c06d6e00-9618-11ea-8bfa-aa3a37308dfb.jpg)

* **Fourth step**______ rotate it around Y axis 90 degrees using _**Transform**_ node

* **Fifth step**   _______connect **_Copy Stamp_** node to **_Transform_** node 
( make sure that you use the same parameters in the photo) 

![copystamp 1](https://user-images.githubusercontent.com/53704509/81961687-60c49200-961b-11ea-992d-751bfd63812f.jpg)

 * repeat it again and use **_Copy Stamp_** node but this time on different axis
( make sure that you use the same parameters in the photo) 

![copystamp2](https://user-images.githubusercontent.com/53704509/81962392-56ef5e80-961c-11ea-9aab-a937c5ccdc90.jpg)

* Now , we want to convert it to Bezier Surface by using **_Convert_** node 
( make sure that you use the same parameters in the photo) 

![Convert](https://user-images.githubusercontent.com/53704509/81963426-bc901a80-961d-11ea-911a-788d14e56363.jpg)
 
* So, we got what we want but we have 2 little problems now!
first one , our geometry is upside down !
second one ,the curves still there after we converted them and we don't want that   !

* let's fix the second one by connect **_Connectivity_** node  to our previous **_Convert_** node that will create an _Attribute_ for us called  _Class_
* then create **_Partition_** node and connect it to our previous **_Connectivity_** node
( make sure that you use the same parameters in the photo) 

![partition](https://user-images.githubusercontent.com/53704509/81966086-a2f0d200-9621-11ea-860f-8cb90710a017.jpg)

* drop down **_Delete_** node and connect it to our previous **_Partition_** node 
(make sure that you choose curves that you want to delete them)

![delete node](https://user-images.githubusercontent.com/53704509/81966959-e861cf00-9622-11ea-9138-54b816982a6f.jpg)


* Now that we have fixed the second one , let's  fix the First one by rotate our geo 180 degrees around X axis using **_Transform_** node :
![Both V](https://user-images.githubusercontent.com/53704509/81969271-56f45c00-9626-11ea-97d0-eac83d4752ce.jpg)

## Voila ! 
* if you have any question send it to my instagram page .
* Hope this Inspired you to create your own project using those techniques .



#### Instagram : https://www.instagram.com/ibrahimalrashd
#### Artstaion: https://www.artstation.com/ibrahimalrashd



