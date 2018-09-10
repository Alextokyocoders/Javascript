# Javascript
___

Compare 2 code:
[code1](https://repl.it/@KenHoang/MasculineLinedInterface)
```JAVASCRIPT
let products = [
  1,
  2,
  3
];

let newproducts = products.map((product) => {
  if (product === 2) {
    product = product + 1;
    return product;
  } else {
    return product;
  }
})

console.log(newproducts);
console.log(products);
```
And [code2](https://repl.it/@KenHoang/LimegreenCloudyCharacterencoding-1)
```JAVASCRIPT
let products = [
  {
    id: 1,
    votes: 10,
  },
  {
    id: 2,
    votes: 15,
  },
  {
    id: 3,
    votes: 20,
  }
];

let newproducts = products.map((product) => {
  if (product.id === 2) {
    product.votes = product.votes + 1;
    return product;
  } else {
    return product;
  }
})

console.log(newproducts);
console.log(products);

console.log(products === newproducts);
```
We can see in code 1: `product = product + 1`
And in code 2: `product.votes = product.votes + 1`

Now look at [Polyfill](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map#Polyfill) of map

Inside map, it creates:
```JAVASCRIPT
 var kValue, mappedValue;

      // a. Let Pk be ToString(k).
      //   This is implicit for LHS operands of the in operator
      // b. Let kPresent be the result of calling the HasProperty internal 
      //    method of O with argument Pk.
      //   This step can be combined with c
      // c. If kPresent is true, then
      if (k in O) {

        // i. Let kValue be the result of calling the Get internal 
        //    method of O with argument Pk.
        kValue = O[k];

        // ii. Let mappedValue be the result of calling the Call internal 
        //     method of callback with T as the this value and argument 
        //     list containing kValue, k, and O.
        mappedValue = callback.call(T, kValue, k, O);

        // iii. Call the DefineOwnProperty internal method of A with arguments
        // Pk, Property Descriptor
        // { Value: mappedValue,
        //   Writable: true,
        //   Enumerable: true,
        //   Configurable: true },
        // and false.
        
        A[k] = mappedValue;
 ```
It means `kValue` is a clone of `product` and in code 1, we set `kValue = product` with a value is primitive value in code 2 product is an object and non-premitive value
can see more in here [Explaining Value vs. Reference in Javascript](https://codeburst.io/explaining-value-vs-reference-in-javascript-647a975e12a0)

We use [Spread syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax#Spread_in_object_literals)

```JAVASCRIPT
let products = [
  {
    id: 1,
    votes: 10,
  },
  {
    id: 2,
    votes: 15,
  },
  {
    id: 3,
    votes: 20,
  }
];


const newproducts = products.map((product) => {
  if (product.id === 2) {
    return {
      ...product,
      votes: product.votes + 1
    }
  } else return product;
});

console.log(newproducts);
console.log(products);

console.log(products === newproducts);

```












