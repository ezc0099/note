# JavaScript数据结构与算法

## 栈

栈是一种遵循后进先出（LIFO）的有序集合。

### 实现栈(基于数组):

```javascript
class Stack {
    constructor(){
        this.items = [];
    }
    //向栈顶压入数据
    push(element){
        this.items.push(element);
    }
    //移除栈顶的元素，并且返回被移除的元素
    pop(){
        return this.items.pop();
    }
    //返回栈顶的元素
    peak(){
        return this.items[this.items.length-1];
    }
    //判断栈是否为空，为空返回true
    isEmpty(){
        return this.items.length === 0;
    }
    //返回栈内元素的数量
    size(){
        return this.items.length;
    }
    //移除栈里的所有元素
    clear(){
        this.items = [];
    }
    toString(){
        return this.items.toString();7
    }
}
```

### 实现栈(基于对象):

```javascript
class Stack {
    constructor(){
        this.count = 0;
        this.items = {};
    }
    push(element){
        this.items[this.count] = element;
        this.count++;
    }
    pop(){
        if(this.isEmpty())return undefined;
        this.count--;
        const result = this.items[this.count];
        delete this.items[this.count];
        return result;
    }
    peak(){
        if (this.isEmpty()) return undefined;
        return this.items[this.count-1];
    }
    isEmpty(){
        return this.count === 0;
    }
    size(){
        return this.count;
    }
    clear(){
        this.items = {};
        this.count = 0;
        //或者遵循LIFO的原则，一个一个的从栈顶移除元素
        // while(!this.isEmpty())this.pop();
    }
    toString(){
        if (this.isEmpty()) return "";
        let objString = `${this.items[0]}`;
        for(let i = 1;i<this.count;i++){
            objString = `${this.items[0]},${this.items[i]}`;
        }
        return objString;
    }
}
```

## 队列

队列（queue）是只允许在一端进行插入操作，而在另一端进行删除操作的线性表。

队列是一种先进先出（FIFO）的线性表，循序插入的一段称为队尾，允许删除的一端称为队头。

### 实现队列：

```javascript
class Queue {
    constructor() {
        this.count = 0;
        this.lowestCount = 0;
        this.items = {};
    }
    // 入队
    enqueue(element){
        this.items[this.count] = element;
        this.count++;
    }
    // 出队
    dequeue(){
        if(this.isEmpty())return undefined;
        let result = this.items[this.lowestCount];
        delete this.items[this.lowestCount];
        this.lowestCount++;
        return result;
    }
    // 输出队首
    peek(){
        if (this.isEmpty()) return undefined;
        return this.items[this.lowestCount];
    }
    //判断是否为空队列
    isEmpty(){
        return this.count === this.lowestCount;
    }
    // 元素数量
    size(){
        return this.count - this.lowestCount;
    }
    // 转字符串
    toString(){
        if(this.isEmpty())return '';
        let objString = `${this.items[this.lowestCount]}`;
        for(let i = this.lowestCount+1;i<this.count;i++){
            objString = `${objString},${this.items[i]}`;
        }
        return objString;
    }
}
```

### 实现双端队列：

前后都能进 都能出

顺序队列：会出现假溢出

循环队列：首位相接的顺序存贮结构

```javascript
class Deque {
  constructor() {
    this.count = 0;
    this.lowestCount = 0;
    this.items = {};
  }
  //前加
  addFront(element) {
    if (this.isEmpty()) {
      addBack(element);
    } else if (this.lowestCount > 0) {
      this.lowestCount--;
      this.items[this.lowestCount] = element;
    } else {
        for(let i = this.count;i>0;i--){
            this.items[i] = this.items[i-1];
        }
        this.items[0] = element;
        this.count++;
    }
  }
  // 后加
  addBack(element){
    this.items[this.count] = element;
    this.count++;
  }
  // 前删
  removeFront(){
    if(this.isEmpty())return undefined;
    let result = this.items[this.lowestCount];
    delete this.items[this.lowestCount];
    this.lowestCount++;
    return result;
  }
  //后删
  removeBack(){
    if (this.isEmpty()) return undefined;
    this.count--;
    let result = this.items[this.count];
    delete this.items[this.count];
    return result;
  }
  //首个元素
  peekFront(){
    if (this.isEmpty()) return undefined;
    return this.items[this.lowestCount];
  }
  //最后一个元素
  pekkBack(){
    if (this.isEmpty()) return undefined;
    return this.items[this.count-1];
  }
  //判断是否为空
  isEmpty(){
    return this.count === this.lowestCount;
  }
  //大小
  size(){
    return this.count - this.lowestCount;
  }
  //清空
  clear(){
    this.lowestCount = 0;
    this.count = 0;
    this.items = {}
    //或者一个一个删除直到为空
    // if(!this.isEmpty())removeBack();
  }
  //转字符串
  toString(){
    if (this.isEmpty()) return "";
    let objString = `${this.items[this.lowestCount]}`
    for(let i = this.lowestCount+1;i<this.count;i++){
        objString = `${objString},${this.items[i]}`
    }
    return objString;
  }
}
```

## 链表

### 实现链表：

### 题目：

#### 1.反转链表

第一种方法：迭代

```javascript
let reverseList = function(head) {
        let pre = null;
        let cur = head;
        while(cur){
            const next = cur.next;
            cur.next = pre;
            pre = cur;
            cur = next;
        }
        return pre;
};

```

第二种方法：递归

```javascript
let reverseList = function(head){
  if(head==null||head.next==null)return head;
  let newHead = reverseList(head.next);
  head.next.next = head;
  head.next = null;
  return newHead;
};
```

#### 2.环形链表

leetcode 141

第一种方法：快慢指针

```javascript
var hasCycle = function(head) {
    let slow = head,fast = head;
    while(fast && fast.next){
        slow = slow.next;
        fast = fast.next.next;
        if(slow==fast)return true;
    }
    return false;
};
```

第二种方法：添加标记

```javascript
var hasCycle = function(head) {
    while(head){
        if(head.flag)return true;
        head.flag = true;
        head = head.next
    }
    return false;
};
```

## 树

### 二叉树

#### 二叉树的遍历

中序遍历：

1.递归

```javascript
let inorderTraversal = function (root) {
  let result = [];
  let inorder = (root) => {
    if (root) {
      inorder(root.left);
      result.push(root.val);
      inorder(root.right);
    }
  };
  inorder(root);
  return result;
};
```

2.迭代

```javascript
```



## 排序与搜索

### 八大排序

#### 冒泡排序

```javascript
function bubbleSort(arr){
  for(let i = 0;i<arr.length;i++){
    for(let j = 0;j<arr.length-1-i;j++){
      if(arr[j]>arr[j+1])[arr[j],arr[j+1]] = [arr[j+1],arr[j]];
    }
  }
  return arr;
}
```

#### 选择排序

```javascript
function selectionSort(arr){
  for(let i = 0;i<arr.length;i++){
    for(let j = i;j<arr.length;j++){
      if(arr[i]>arr[j+1])[arr[i],arr[j+1]] = [arr[j+1],arr[i]];
    }
  }
  return arr;
}
```

#### 插入排序

```javascript
function insertSort(arr) {
  for (let i = 0; i < arr.length; i++) {
    let j = i - 1;
    let min = i;
    while (j >= 0 && arr[min] < arr[j]) {
      [arr[min], arr[j]] = [arr[j], arr[min]];
      j--;
      min--;
    }
  }
  return arr;
}
```

#### 归并排序

```javascript
 function mergeSort(arr){
  if(arr.length>1){
    let mid = Math.floor(arr.length/2);
    let left = mergeSort(arr.slice(0,mid));
    let right = mergeSort(arr.slice(mid,arr.length));
    arr =  merge(left,right); 
  }
  return arr;
  function merge(left,right){
    let i = 0,j = 0,result = [];
    while(i<left.length && j<right.length){
      result.push(left[i]<right[j] ? left[i++] : right[j++]);
    }
    result = result.concat(i<left.length ?
     left.slice(i,left.length) : right.slice(j,right.length))
    return result;
  }
 }
```

#### 快速排序

```javascript
function quickSort(arr,left=0,right=arr.length-1) {
  let { length } = arr;
  if (length > 1) {
    i = left;
    j = right;
    let mid = arr[Math.floor((i + j) / 2)];
    while (i <= j) {
      while (arr[i] < mid) {
        i++;
      }
      while (arr[j] > mid) {
        j--;
      }
      if (i <= j) {
        [arr[i], arr[j]] = [arr[j], arr[i]];
        i++;
        j--;
      }
    }
    if(i>left+1)quickSort(arr,left,i-1);
    if(i<right)quickSort(arr,i,right);
  }
  return arr;
}
```

#### 计数排序

```javascript
function countingSort(arr){
  let max=arr[0],min=arr[0];
  arr.forEach(item=>{
    if(item>max)max=item;
    if(item<min)min=item;
  })
  let counting = new Array(max-min+1);
  arr.forEach(item=>{
    if(!counting[item - min])counting[item - min] = 0;
    counting[item - min]++;
  })
  let newArr=[];
  counting.forEach((item,index)=>{
      while(item){
        newArr.push(index+min)
        item--;
      }
  })
  return newArr;
}
```

数据范围大时不建议（max-min太大时），需要的计数数组空间过大。

数据中有小数时不支持。

#### 桶排序



#### 基数排序



### 搜索算法

#### 线性/顺序搜索

一项一项对比。

```javascript
let sequentialSearch = function(arr,searchValue){
    for(let i = 0;i<arr.length;i++){
        if(arr[i]==searchValue)return i;
    }
    return -1;
}
```

#### 二分搜索

1.递归版本-数组无重复

```javascript
let binarySearch = function(arr, searchValue,left=0,right=arr.length) {
    let mid = Math.floor((left+right)/2);
    if(searchValue>arr[arr.length-1]||searchValue<arr[0])return -1;
    else if(searchValue==arr[mid])return mid;
    else if(searchValue>arr[mid])return binarySearch(arr, searchValue,mid+1, arr.length);
    else if(searchValue<arr[mid])return binarySearch(arr.slice(0, mid), searchValue);
};
```

2.递归版本-数组有重复时获取第一个值的索引

```javascript
let binarySearch = function(arr,searchValue){
    let mid = Math.floor(arr.length/2);
    if(searchValue>arr[arr.length-1||searchValue<arr[0]])return -1;
    else if(searchValue==arr[mid]){
        for(let i = 0;i<mid;i++){
            if(arr[i]==arr[mid])return i;
        }
        return mid;
    }
    else if(searchValue>arr[mid])return binarySearch(arr.slice(mid+1, arr.length), searchValue);
    else if(searchValue<arr[mid])return binarySearch(arr.slice(0, mid), searchValue);
}
```

3.普通版本

```javascript
let binarySearch = function(arr,searchValue){
    let left = 0;
    let right = arr.length - 1;
    let mid;
    while(left<right){
        mid = Math.floor((left+right)/2);
        if(searchValue==arr[mid])return mid;
        else if(searchValue<arr[mid])right = mid-1;
        else if(searchValue>arr[mid])left = mid + 1;
    }
    return -1;
}
```

4.普通版本-数组有重复时获取第一个值的索引

```javascript
let binarySearch = function (arr, searchValue) {
  let left = 0;
  let right = arr.length - 1;
  let mid;
  while (left < right) {
    mid = Math.floor((left + right) / 2);
    if (searchValue == arr[mid]) {
      for (let i = 0; i < mid; i++) {
        if (arr[i] == arr[mid]) return i;
      }
      return mid;
    } else if (searchValue < arr[mid]) right = mid - 1;
    else if (searchValue > arr[mid]) left = mid + 1;
  }
  return -1;
};
```

#### 内插搜索

```javascript
let interpolationSearch = function(arr,searchValue){
    let left = 0;
    let right = arr.length-1;
    if(searchValue<arr[left]||searchValue>arr[right])return -1;
    let mid;
    while(left<right){
        mid = Math.floor((searchValue - arr[left])/(arr[right]-arr[left]) * (right-left)) + left ;
        if(searchValue == arr[mid])return mid;
        else if(searchValue<arr[mid])right = mid-1;
        else if(searchValue>arr[mid])left = mid+1;
    }
}
```
