I tried to remove duplicates with Array items in JS today. 
I could make an unique array with comparing each other and add another array. 
But i would like to use "new Set()". Because i thought it could be easy to code and read.

So i coded like this
```javascript
let objectArray = [	
	{ id: 1 , text: "a"}, 
	{ id: 1 , text: "a"}, 
	{ id: 2 , text: "b"}, 
	{ id: 3 , text: "c"}, 
	{ id: 4 , text: "d"}, 
	{ id: 2 , text: "b"}
];
let setData = new Set(objectArray);
let setToArray = Array.from(setData);
console.log(setData);

```

#### log
It supposed to show only 4 items of Array but 6.  When i google to remove duplicates from Array , they said use set object. So i found another way. 

```javascript
let objectArray = [	
	{ id: 1 , text: "a"}, 
	{ id: 1 , text: "a"}, 
	{ id: 2 , text: "b"}, 
	{ id: 3 , text: "c"}, 
	{ id: 4 , text: "d"}, 
	{ id: 2 , text: "b"}
];
var jsonObject = objectArray.map(JSON.stringify);
var uniqueSet = new Set(jsonObject);
var uniqueArr = Array.from(uniqueSet).map(JSON.parse);

console.log(uniqueArr);
```

It worked and i realized that "new Set()" remove duplicates when it is just Arrray. 
I wanted to know the reason. And there is reason below

>[!important]
>Set compares object data with address not as attributes


Oh it's about Java not javascript :(