# Few drops of Javascript

## var vs let vs const

### var

```js
function hello_var() {
  for (var i = 0; i < 5; i++) {
    console.log(i);
  }

  console.log("value of i = " + i);
}
```

*Result*

```js
0
1
2
3
4
value of i = 5
```

### let

```js
function hello_let() {
  for (let i = 0; i < 5; i++) {
    console.log(i);
  }

  console.log("value of i " + i);
}
```

*Result*

```js
0
1
2
3
4
ReferenceError: i is not defined
```

### Another usage of const & let

```js
const apple = "🍎";
apple = "🍍";
// TypeError: Assignment to constant variable

let egg = "🥚";
egg = "🍕";
// '🍕'
```

## String literals

```js
const chocolate = "🍫";
const iceCream = "🍨";

const textOld = chocolate + " & " + iceCream + " are delicious!!!";

const text = `${chocolate} & ${iceCream} are delicious!!!`;
// '🍫 & 🍨 are delicious!!!'

```

## Rest and Spread operators

### Rest operator - array

```js
const LOTR = ["Gandalf", "Legolas", "Gollum", "Saruman", "Arwen"];
const [wizard, ...rest] = LOTR;

console.log(`wizard is ${wizard}`);
console.log(`${rest} is here...`);

// "wizard is Gandalf"
// "Legolas,Gollum,Saruman,Arwen is here..."

```

```js
function youShallNotPass(wizard, ...rest) {
  console.log(`${wizard} says you shall not pass 🧙`);
  console.log(`${rest} is confused 😒`);
} // variadic function (variable numbers of argument)

youShallNotPass("Gandalf", "Legolas", "Gollum", "Saruman", "Arwen");

// or

youShallNotPass(...LOTR);

// 'Gandalf says you shall not pass 🧙'
// 'Legolas,Gollum,Saruman,Arwen is confused 😒'

// 'wizard is Gandalf'
// 'Legolas,Gollum,Saruman,Arwen is here...'

```

```js
const newLotr = [...LOTR, "Sauron", "Merry", "Pippin"];
// [
//  'Gandalf', 'Legolas',
//  'Gollum',  'Saruman',
//  'Arwen',   'Sauron',
//  'Merry',   'Pippin'
// ]
```

### Spread operator - object


```js
const anakinSkywalker = {
  name: "Anakin Skywalker",
  homePlanet: "Tatooine",
  dislikes: "Sand"
};


const darthVadar = {
  ...anakinSkywalker,
  name: 'Darth Vadar',
  isSith: true
};

// {
//   name: 'Darth Vadar',
//   homePlanet: 'Tatooine',
//   dislikes: 'Sand',
//   isSith: true
// }
```

## Array destructuring

```js
const tribes = ["🔥", "🌊", "🌀", "🌎"];
const [fireNation, waterTribe, airNormads, earthKingdom] = tribes;

const intro = `Water. Earth. Fire. Air.
  My grandmother used to tell me stories about the old days,
  a time of peace when the Avatar kept balance between the
  ${waterTribe}, ${earthKingdom}, ${fireNation}, and ${airNormads}.
`;

// 'Water. Earth. Fire. Air.
// My grandmother used to tell me stories about the old days,
// a time of peace when the Avatar kept balance between the
// 🌊, 🌎, 🔥, and 🌀.'
```

### Another usage of array destructuring

```js
// React
const [counter, setCounter] = useState(0)
```

## Object destructuring

```js
const hermione = {
  fullName: "Hermione Granger 👩",
  bloodStatus: "Muggle-born",
  knownAs: "Little Miss Perfect",
  hairColour: "Brown",
};

// const { fullName, knownAs } = hermione;
const { fullName: fName, knownAs } = hermione;

const details = `${fName} is also known as ${knownAs} 😍`;

// 'Hermione Granger 👩 is also known as Little Miss Perfect 😍'
```

```js
const movies = [
  {
    movieName: `Zack Snyder's Justice League`,
    releaseDate: "3/18/2021",
  },
  {
    movieName: `Avengers: Endgame`,
    releaseDate: "4/26/2019",
  },
  {
    movieName: `Wonder Woman`,
    releaseDate: "6/1/2017",
  },
  {
    movieName: `Man of Steel`,
    releaseDate: "6/14/2013",
  },
];

for (let { movieName, releaseDate } of movies) {
  console.log(`${movieName} released on ${releaseDate}`);
}

// "Zack Snyder's Justice League released on 3/18/2021"
// "Avengers: Endgame released on 4/26/2019"
// "Wonder Woman released on 6/1/2017"
// "Man of Steel released on 6/14/2013"
```

```js

function printMovie({ movieName, releaseDate }) {
  console.log(`${movieName} released on ${releaseDate}`);
}

printMovie(movies[0]);

// "Zack Snyder's Justice League released on 3/18/2021"

```

## Array Helpers

```js
const foods = ["🍿", "🍩", "🍪", "🌰", "🥜", "🍯"];
```

### Filter

```js
const selectedFoods = foods.filter((food, index) => index > 2);

// [ '🌰', '🥜', '🍯' ]
```

### Map

```js
const foodThoughts = foods.map((food) => `${food} is awesome!`);

// [
//   "🍿 is awesome!",
//   "🍩 is awesome!",
//   "🍪 is awesome!",
//   "🌰 is awesome!",
//   "🥜 is awesome!",
//   "🍯 is awesome!",
// ]
```

### For Each

```js
foods.forEach((food) => console.log(`${food} is tasty!`));

// '🍿 is tasty!'
// '🍩 is tasty!'
// '🍪 is tasty!'
// '🌰 is tasty!'
// '🥜 is tasty!'
// '🍯 is tasty!'
```

```js
const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

numbers.reduce((acc, curr) => curr + acc, 0);

// 55
```

### Reduce

```js
const foodThoughtsWithReduce = foods.reduce((result, currentFood) => {
  result = [...result, `${currentFood} is yummy!!!`];
  return result;
}, []);

// [
//   '🍿 is yummy!!!',
//   '🍩 is yummy!!!',
//   '🍪 is yummy!!!',
//   '🌰 is yummy!!!',
//   '🥜 is yummy!!!',
//   '🍯 is yummy!!!'
// ]
```

```js
const foodObjectsWithReduce = foods.reduce((result, currentFood, index) => {
  result[index] = currentFood;
  return result;
}, {});

// { '0': '🍿', '1': '🍩', '2': '🍪', '3': '🌰', '4': '🥜', '5': '🍯' }
```
