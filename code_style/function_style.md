# Function Style

## context

- naming
- reuse code
- clear logic
- lines ~20
- avoid nested if/for/while

## naming

Keep it consistent!

1. Pascal Naming

```
public void SendMessage ();
public void CalculatePrice ();
```

Usually Used for:

- class
- attribute
- function

2. Camel-case

```
var sendMessage = function () {};
var calculatePrice = function () {};
```

Usually used for:

- local variable
- function argument

### Description what the function does

```
// 描述不够完整的函数名
var count = function addComment() {};

// 描述完整的函数名
var count = function addCommentAndReturnCount() {};
```

### Acurate Verb

提高词汇量，多阅读优秀代码。不要使用太过宽泛的词汇，比如不要什么都是get。

- get
- fetch
- load
- calculate
- find
- create
- build
- parse
- ....

个人和团队要使用同一规则！

## Function arguments

参数越多，易用性就越差,但也不是越少越好。减少对其他状态（比如全局变量）的dependency,
增加可测试性。

最好不超过7个，如果要使用很多变量，可以考虑将类似的参数构造成一个类。

### 尽量不要使用boolean作为参数

比如

```javascript
var getProduct = function(finished) {
    if(finished){
    }
    else{
    }
}

// 调用
getProduct(true); # very confusing
```

有两种方法可以优化:

- 拆分成两个函数`getFinishedProduct()` and `getUnFinishedProduct()`
- 将boolean换成有意义的`getProduct(productStatus)`

### 函数内不要修改参数

### 不要使用输出参数

使用输出参数说明函数不只做了一件事情，应该分解。

## Function body

### 相关操作放在一起

```javascript
var calculateTotalPrice = function()  {
    var roomCount = getRoomCount();
    var mealCount = getMealCount();

    var roomPrice = getRoomPrice(roomCount);
    var mealPrice = getMealPrice(mealCount);

    return roomPrice + mealPrice;
}
```

should be

```javascript
var calculateTotalPrice = function()  {
    var roomCount = getRoomCount();
    var roomPrice = getRoomPrice(roomCount);
    
    var mealCount = getMealCount();
    var mealPrice = getMealPrice(mealCount);

    return roomPrice + mealPrice;
}
```

### 尽量减少嵌套:if, switch, for

1. 尽早return

```javascript
if(condition1) {
    if(condition2){
        if(condition3){
        }
        else{
            return;
        }    
    }
    else{
        return;
    }    
}
else {
    return;
}
```

should 提取最后面的return到最前面

```javascript
if(!condition1){
    return;
}
if(!condition2){
    return;
}
if(!condition3){
    return;
}
```

### 表驱动法 in 代码大全

把if..elseif...elseif变成表

```javascript

var map = {
    "case1":1,
    "case2":2,
    "case3":3,
    "case4":4
}
return map[condition];
```

### 内层嵌套改为函数

### for循环

1. 最多两层for循环
2. 提取内层到新的函数
3. 多层循环时，不要简单的使用i, j, k等，要用具体的意思的变量

### complex logic -> meaningful function

```javascript
if (age > 18 && gender == "man") {
}
```

into

```javascript
var canDoSth = function (age, gender){
    return age > 18 && gender == "man";
}
...
...
...
if(canDoSth(age, gender)){
    //doSth
}
```
