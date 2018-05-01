```js
const getMaxProfit = (stockPricesYesterday) => {
  let minPrice = stockPricesYesterday[0];
  let maxProfit = stockPricesYesterday[1]-stockPricesYesterday[0];
  if (stockPricesYesterday.length < 2) throw new Error('Not enough data')
  for (let i = 1; i < stockPricesYesterday.length; i++) {
    const currentPrice = stockPricesYesterday[i];
    const potentialProfit = currentPrice - minPrice;
    // ensure minPrice is the lowest price we've seen so far
    minPrice = Math.min(minPrice, currentPrice);
  
    // see what our profit would be if we bought at the
    // min price and sold at the current price
    
  
    // update maxProfit if we can do better
    maxProfit = Math.max(maxProfit, potentialProfit);
  }
  
  return maxProfit;
}




// Tests

let desc = 'price goes up then down';
let actual = getMaxProfit([1, 5, 3, 2]);
let expected = 4;
assertEqual(actual, expected, desc);

desc = 'price goes down then up';
actual = getMaxProfit([7, 2, 8, 9]);
expected = 7;
assertEqual(actual, expected, desc);

desc = 'price goes up all day';
actual = getMaxProfit([1, 6, 7, 9]);
expected = 8;
assertEqual(actual, expected, desc);

desc = 'price goes down all day';
actual = getMaxProfit([9, 7, 4, 1]);
expected = -2;
assertEqual(actual, expected, desc);

desc = 'price stays the same all day';
actual = getMaxProfit([1, 1, 1, 1]);
expected = 0;
assertEqual(actual, expected, desc);

desc = 'one price throws error';
const onePrice = () => (getMaxProfit([1]));
assertThrowsError(onePrice, desc);

desc = 'empty array throws error';
const emptyArray = () => (getMaxProfit([]));
assertThrowsError(emptyArray, desc);

function assertEqual(a, b, desc) {
  if (a === b) {
    console.log(`${desc} ... PASS`);
  } else {
    console.log(`${desc} ... FAIL: ${a} != ${b}`)
  }
}

function assertThrowsError(func, desc) {
  try {
    func();
    console.log(`${desc} ... FAIL`);
  } catch (e) {
    console.log(`${desc} ... PASS`);
  }
}
```