# codex-test

## 3
```javascript
function isSquare(x) {
  if (!(Number.isInteger(x))) {
    throw new Error('Integer expected.');
  }
  if (x <= 0) {
    return false;
  }
  let i = 1;
  while (i * i < x) {
    ++i;
  }
  if (i * i === x) {
    return true;
  }
  return false;
}
```
Можно искать не за корень, а за логарифм бин. поиском, однако гугл сказал, что в js нет целочисленного деления, а пользоваться математическими функциями запрещено...

## 4
```javascript
function findPairWithGivenSum(arr, targetSum) {
  if (!Number.isInteger(targetSum)) {
    throw new Error('Target sum should be integer.');
  }
  arr.forEach(function(i) {
    if (!Number.isInteger(i)) {
      throw new Error('Expected array of integers');
    } 
  });
  let m = new Map();
  arr.forEach(function(i) {
    if (m.has(i)) {
      m.set(i, m.get(i) + 1);
    } else {
      m.set(i, 1);
    }
  });
  for (let i of arr) {
    let need = targetSum - i;
    if (m.has(need)) {
      if (need !== i || m.get(need) > 1) {
        console.log(i + " " + need);
        return [i, need];
      }
    }
  }
}
```
Если мапа реализована на хеш-таблице, то за линию складываем все числа, и за O(1) для каждого числа проверяем, можно ли составить с ним нужную пару.

## 5
Интересный способ посортировать массив положительных целых чисел. Мы число n добавляем в результирующий массив с таймаутом n, то есть чем больше число, тем позже мы его добавим, и получим массив отсортированный по возрастанию.++
