# Grid

### 1. Intro - define  - set cols & rows

```html
  .container>.item{$}*10
```

```css
 .container {
    display: grid;
    /*3 column* */
    grid-template-columns: 100px 100px 100px;
    grid-gap: 20px;
  }
```

another option

```css
grid-template-columns:repeat(5, 100px);
```

we can combine :

```css
    grid-template-columns: 200px 500px;
    grid-template-rows: 200px 100px 400px;
```

---

### 2 Grid implicit vs explicit tracks

```html
    display: grid;
    grid-template-columns: 200px 400px;
    grid-gap: 20px;
```

implicit - **what we have not created **

explicitly - we defined columns

implicit - rows 

how to size implic ones  --- auto

```css
.container {
  display:grid;
  grid-gap: 20px;
  grid-template-columns: 200px 400px;
  grid-template-rows:50px 100px;
  grid-auto-rows:100px;
  grid-auto-columns: 100px;
}
```

## 

###  3. Grid auto-flow

what to do with extra element ? 

Determine whether add another row or column 

by default it will add to row 

```css
  .container {
    display: grid;
    grid-template-columns: 400px 200px;
    grid-gap: 20px;
  }
```

when we change to col : 

```css
    grid-auto-flow: column;
```

we can can control size : 

```css
    grid-auto-columns: 200px;
```

### 4. Sizing tracks 

container style : 

```css
   display: grid;
    border: 10px solid var(--yellow);
    grid-template-columns: 1fr 2fr 1fr;
    grid-gap: 20px;
```

default element height - height as element

default width - as viewport

we can set explicit height : 

```css
.container {
display: grid;
      height: 600px;
    width:400px;
      grid-gap: 20px;
      border: 10px solid var(--yellow);
      grid-template-columns: auto 1fr auto 1fr;

}
```

### 5. Grid repeat function 



```css
  .container {
    display: grid;
    grid-gap: 20px;
    grid-template-columns: repeat(4, 1fr 2fr);
  }
```

if we give width to one column - it will expand rest : 

```css
  .container {
    display: grid;
    grid-gap: 20px;
    grid-template-columns: repeat(5, 1fr);
  }
```

the same when we give a lot of content 

**we need to use spanning**

```css
  .item9 {
    grid-column: span 2;
    background: aqua;
  }
```

we can give :

```css  .item9 {
    grid-column: span 4;
```



```css
  .item9 {
    grid-column: span 2;
    grid-row:span 2;
```

### 6. Placing grid elements



```html
.container>.item *30
```

```css
.container {
  display:grid;
  grid-gap:20px;
  grid-template-columns:repeat(5,1fr);
  grid-template-rows: repeat(5, 1fr);
}
.poop {
  background:#bada55;
  grid-column:span 2;
  grid-row:1/-1;
}

```

### 7. Spanning elements 

1.make grid 10 col width  - second element take twice free space : 

make grid 10 explicit rows (50px high each)

```css
.container {
  display: grid;
      grid-gap: 20px;
  grid-template-columns: repeat(5, 1fr 2fr);
   grid-template-rows: repeat(10, 50px);
}
```



item1 - start at col3 and go til 5 

```css
  .item1 {
    grid-column: 3 / 5;
  }
```

Item 2-  start at col 5 and go to the end 

```css
  .item2 {
    grid-column: 5 / -1;
  }
```

item5 - double span (2 cols and rows)

```css
  .item5 {
    grid-column: span 2;
    grid-row: span 2;
  }
```

item15 - span entire width :

```css
  .item15 {
    grid-column: 1/-1;
  }
```

### 8. Auto-fit  & auto-fill 

content of item can be wider or bigger 

 we just say : figure out - how many you can fill there 

```html
  <div class="container">
    <div class="item item1">Item 01</div>
    <div class="item item2">Item 02</div>
    <div class="item item3">Item 03</div>
    <div class="item item4">Item 04</div>
  </div>

```

```css
.container {
  display:grid;
  grid-gap:20px;
  border:10px solid var(--yellow);
  grid-template-columns:repeat(auto-fill , 150px);
}

```

### 9.Min max



- we tell min and max track will be 

  ```css
   grid-template-columns:repeat(auto-fit, minmax(150px, 1fr));
  ```

  ```css
    grid-template-columns:fit-content(100px) 150px 150px 150px;
  ```

  

---

### 10. Grid template areas

```html
  <div class="container">
      <div class="item item1">Sidebar #1</div>
      <div class="item item2">Lorem ipsum dolor sit amet consectetur, adipisicing elit. Delectus itaque, quibusdam odio quos sunt fuga doloremque praesentium nemo consequatur, amet optio rerum nam quod iure voluptatibus culpa. Reprehenderit, eveniet, necessitatibus?</div>
      <div class="item item3">Sidebar #2</div>
      <div class="item item4">Footer</div>
  </div>
```

```css
  .container {
    display: grid;
    grid-gap: 20px;
    grid-template-columns: 1fr 500px 1fr;
    grid-template-rows: 150px 150px 100px;
    grid-template-areas:
          "sidebar-1 content sidebar-2"
          "sidebar-1 content sidebar-2"
          "footer footer footer";
  }
```

now we can place items into those areas : 

```css
  .item1 {grid-area:sidebar-1;}
  .item2 {grid-area:content;}
  .item3 {grid-area:sidebar-2;}
  .item4 {grid-area:footer;}
```

then we can style media quries

```css
    @media (max-width: 700px) {
      .container {
        grid-template-areas:
          "content    content     content"
          "sidebar-1  sidebar-1   sidebar-2"
          "footer     footer      footer"
      }
    }
```

### 11. Grid Lines 



```html
.container > .item*30
```

```css
.container {
  display:grid;
  grid-gap:20px;
  grid-template-columns: [sidebar-start site-left] 1fr [sidebar-end content-start] 500px [content-end] 1fr [site-right];  
  grid-template-rows: [content-top] repeat(10, auto) [content-bottom];
}
.item3 {
  background:slateblue;
  grid-column:content-start;
  grid-row:content-top / content-bottom;
}
```



---

### 12. Auto-flow dense block fitting

if we have more items - that are not fitted into grid - are moved into another row (implicitly )

we have 70 items 

every 6th item will have span of 6 

```css
grid-auto-flow:dense /*make sure that we will have 10 columns*/
```

```css
.container {
  display:grid;
  grid-gap:20px;
  grid-template-columns: repeat(10, 1fr);
  grid-auto-flow:dense;
}
.item:nth-child(6n) {
  background:cornflowerblue;
  grid-column:span 6;
}
```



---

### 13. Grid Alignment + centering

justify-  x axis 

align - y axis 

**They do not switch like in flexbox**

```css
.container {
  display:grid;
  grid-gap:20px;
  height:500px;
  border:10px solid var(--yellow);
  grid-template-columns:repeat(5, 130px);
/* justify-items: center; */
/*   align-items:center; */
  place-items:flex-end stretch;
        justify-content: space-between;
/*       align-content: space-between; */

}
```


### 13. Simple Grid system with pictures
```html
<div class="wrapper">
        <div class="album">
          <img class="album__artwork" src="https://source.unsplash.com/random/300x300?v=1">
          <div class="album__details">
            <h2>Album Title</h2>
            <p class="album__artist">Artist Name</p>
            <p class="album__desc">Lorem ipsum dolor sit amet consectetur adipisicing elit. Ipsum sed sint doloremque repellat, iste debitis.</p>
            <p class="album__desc">Lorem ipsum dolor sit amet consectetur, adipisicing elit. Facilis, excepturi!</p>
          </div>
        </div>
  ...
  
```

```css
   .wrapper {
            display: grid;
            grid-template-columns:repeat(auto-fit, minmax(600px, 1fr));
            grid-gap: 20px;
        }
        .album {
            background: rgba(74, 79, 71, 0.2);
            box-shadow: 0 0 5px rgba(0,0,0, 0.1);
            padding:20px;
            display: grid;
            grid-template-columns: 200px 1fr;
            grid-gap: 10px;
            align-items: center;
        }
        img { width: 100%;  }
        .album__artwork {
            width:100%;
        }
```
