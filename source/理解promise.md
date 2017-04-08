title: "理解promise"
date: 2017-04-03 10:00:00 +0800
update: 2017-04-03 10:00:00 +0800
author: zhengwei
cover: "-/images/bower-logo.svg"
tags:
    - js理论知识
preview: 理解promise

---

# 如果不用promise


```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
  <style>
    .ball{
      width: 40px;
      height: 40px;
      border-radius: 20px;
    }
    .ball1{
      background: red;
    }
    .ball2{
      background: yellow;
    }
    .ball3{
      background: green;
    }
  </style>
</head>
<body>
  <div class="ball ball1"></div>
  <div class="ball ball2"></div>
  <div class="ball ball3"></div>
  <script>
    var ball1 = document.querySelector('.ball1');
    var ball2 = document.querySelector('.ball2');
    var ball3 = document.querySelector('.ball3');
    function animate(ball,distance,callback){
      setTimeout(function(){
        var marginLeft = parseInt(getComputedStyle(ball).marginLeft);
        // console.log(marginLeft,distance);
        if(marginLeft === distance){
          callback();
        }else{
          if(marginLeft < distance){
            marginLeft ++;
          }else{
            marginLeft--;
          }
          ball.style.marginLeft = marginLeft + "px";
          animate(ball,distance,callback);
        }

      },13);
    }
    animate(ball1,100,function(){
      animate(ball2,200,function(){
        animate(ball3,300,function(){
          animate(ball3,150,function(){
            animate(ball2,150,function(){
              animate(ball1,150,function(){

              })
            })
          })
        })
      })
    });
  </script>
</body>
</html>

```

## 用了promise
```javascript
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
  <style>
    .ball{
      width: 40px;
      height: 40px;
      border-radius: 20px;
    }
    .ball1{
      background: red;
    }
    .ball2{
      background: yellow;
    }
    .ball3{
      background: green;
    }
  </style>
  <script src="./node_modules/bluebird/js/browser/bluebird.js"></script>
</head>
<body>
  <div class="ball ball1"></div>
  <div class="ball ball2"></div>
  <div class="ball ball3"></div>
  <script>
    var ball1 = document.querySelector('.ball1');
    var ball2 = document.querySelector('.ball2');
    var ball3 = document.querySelector('.ball3');
    function promiseAnimate(ball,distance){
    //构造函数声明模式，它在用来包裹非 promise API 
      return new Promise(function(resolve,reject){
        function animate(){
          setTimeout(function(){
            var marginLeft = parseInt(getComputedStyle(ball).marginLeft);
            if(marginLeft === distance){
              resolve();
            }else{
              if(marginLeft < distance){
                marginLeft ++;
              }else{
                marginLeft--;
              }
              ball.style.marginLeft = marginLeft + "px";
              animate();
            }

          },13);
        }
        animate()
      });
    }

    promiseAnimate(ball1,100)
      .then(function(){
        console.log(111);
        return promiseAnimate(ball2,200);
      })
      .then(function(){
        return promiseAnimate(ball3,300);
      })
      .then(function(){
        return promiseAnimate(ball3,150);
      })
      .then(function(){
        return promiseAnimate(ball2,150);
      })
      .then(function(){
        return promiseAnimate(ball1,150);
      })
  </script>
</body>
</html>

```

# jQuery中的promise

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>
<body>
  <script src="node_modules/jquery/dist/jquery.js"></script>
  <script>
    var loadData = function(){
      return $.ajax({
        url:"./a.json",
        type:"get"
      })
    }
    loadData().then(function(data){
      console.log(data);
    });
  </script>
</body>
```
##  生成器
```javascript
function* inc () {
 let number = 0
 while (true)
 yield number++
}

let test = inc()

console.log(test.next().value) // -> 0
console.log(test.next().value) // -> 1
console.log(test.next().value) // -> 2
console.log(test.next().value) // -> 2
console.log(test.next().value) // -> 2
console.log(test.next().value) // -> 2
console.log(test.next().value) // -> 2
console.log(test.next().value) // -> 2

```