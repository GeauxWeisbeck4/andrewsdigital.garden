---
{"dg-publish":true,"permalink":"/500-catalog-of-notes/513-web-dev/css/flexbox/flexbox-fundamentals/"}
---

- ## Using flex-direction to layout content horizontally and vertically
	- ![Pasted image 20230109190736.png](/img/user/1100%20Images/Pasted%20image%2020230109190736.png)
```
body {

  background: white;

  font-family: 'Open Sans', sans-serif;

}

.main-nav li {

  width: 100px;

}

.main-nav a {

  text-decoration: none;

  color: black;

  font-size: 21px;

  font-weight: 600;

  color: #00a9d9;

}

.main-nav a:hover {

  text-decoration: underline;

}

  

.main-nav ul {

  list-style: none;

  display: flex;

  flex-direction: row-reverse;

}
```
- # Rearranging the order in flexbox
- ![Pasted image 20230109191329.png](/img/user/1100%20Images/Pasted%20image%2020230109191329.png)

```
body {

  background: white;

  font-family: 'Open Sans', sans-serif;

}

.main-nav li {

  width: 100px;

}

.main-nav a {

  text-decoration: none;

  color: black;

  font-size: 21px;

  font-weight: 600;

  color: #00a9d9;

}

.main-nav a:hover {

  text-decoration: underline;

}

  

.main-nav ul {

  list-style: none;

  display: flex;

}

  

.main-header {

  background: #B61E32;

  padding: 10px;

}

.main-content{

  background: #F7CE2B;

  min-height: 40vh;

  padding: 10px;

}

.main-footer{

  background: #ABC999;

  padding: 10px;

  order: 1;

}

  

body {

  display: flex;

  flex-direction: column;

}

  

.main-nav {

  order: -1;

}
```

- # Demistyfing alignment in the flexbox
- ![Pasted image 20230109192025.png](/img/user/1100%20Images/Pasted%20image%2020230109192025.png)
```
:root {

  height: 100%;

}

body {

  font-family: 'Open Sans', sans-serif;

  margin: 0;

  min-height: 100%;

  background: #333;

}

h1 {

  font-weight: 600;

  margin: 0 0 5px 0;

}

p {

  margin: 5px 0;

}

article {

  box-sizing: border-box;

  background: #FFF;

  margin: 5px;

  flex: 1;

}

body {

  display: flex;

  flex-direction: row;

  align-items: baseline;

}

.not-real {

  align-self: flex-end;

}
```
- # Defining dimensions on flexbox children using flex-basis
- ![Pasted image 20230109192508.png](/img/user/1100%20Images/Pasted%20image%2020230109192508.png)
```
body {

  margin: 0;

  font-family: 'Open Sans', sans-serif;

  margin: 0;

  color: #eec965;

  display: flex;

}

  

.title-1 {

  background: #dd5f40;

  width: 220px;

  flex-basis: 150px;

}

  

.title-2 {

  background: #3d483a;

}

  

.title-3 {

  background: #468e5d;

}

  

h1 {

}
```
- # Using flex-shrink and flex-grow to make flexbox children resize correctly
- # Combining the flexbox sizing properties using the flex shorthand
- ![Pasted image 20230109194720.png](/img/user/1100%20Images/Pasted%20image%2020230109194720.png)
- 
```
body {

  margin: 0;

  display: flex;

  font-family: 'Open Sans', sans-serif;

  margin: 0;

  color: #eec965;

}

  

.title-1 {

  background: #dd5f40;

  flex: 1;

    /* flex-grow: 1;

       flex-shrink: 1;

       flex-basis: 0;

    */

}

  

.title-2 {

  background: #3d483a;

  flex: 20px;

    /* flex-grow: 1;

       flex-shrink: 1;

       flex-basis: 20px;

    */

}

  

.title-3 {

  background: #468e5d;

  flex: 0 80px;

    /* flex-grow: 0;

       flex-shrink: 1;

       flex-basis: 80px;

    */

}

  

h1 {

  flex-basis: 0;

}
```
- # Turning a flexbox into a grid using flex-wrap and align-content
- ![Pasted image 20230109195432.png](/img/user/1100%20Images/Pasted%20image%2020230109195432.png)
```
html{

  height: 100%;

}

body {

  margin: 0;

  font-family: 'Open Sans', sans-serif;

  margin: 0;

  height: 100%;

}

figure {

  margin: 0;

  display: block;

  height: 150px;

  flex: 0 150px;

  position: relative;

}

figcaption {

  background: rgba(0,0,0,0.5);

  display: block;

  position: absolute;

  bottom: 0px;

  width: 100%;

  text-align: center;

  color: white;

  padding: 4px;

  box-sizing: border-box;

}

body {

  display: flex;

  flex-wrap: wrap;

  justify-content: space-around;

  align-content: space-around;

}
```
- # Using Flexbox in Websites and Applications
	- https://codepen.io/joelhooks/pen/KMGrNz


-  