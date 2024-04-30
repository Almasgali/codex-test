# codex-test

## 1

### 1.1
```SQL
SELECT id FROM departments dp
WHERE NOT EXISTS (
	SELECT 1 FROM dep_names dn WHERE dn.department_id = dp.id 
);
```

### 1.2
```SQL
SELECT dp.id FROM departments dp
INNER JOIN dep_names dn ON dp.id = dn.department_id
GROUP BY dp.id
HAVING COUNT(dn.id) >= 2;
```

## 2
Что то вроде:
```
table object {
  id,
  timestamp,
  parent_id
}

table contact {
  id,
  object_id,
  server,
  email
}

table user {
  id,
  contact_id,
  name
}

table address {
  id,
  object_id,
  addr
}
```
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
  return [];
}
```
Если мапа реализована на хеш-таблице, то за линию складываем в нее все числа, и за O(1) для каждого числа проверяем, можно ли составить с ним нужную пару.

## 5
Интересный способ посортировать массив положительных целых чисел. Мы число n добавляем в результирующий массив с таймаутом n, то есть чем больше число, тем позже мы его добавим, и получим массив отсортированный по возрастанию.

## 5*

```javascript
function func(arr, call_back) {
	
  if (!Array.isArray(arr) || arr.some(it => parseInt(it) != it || it < 0)) {
    call_back(null, "Неверный формат входящих данных, должен быть массив положительных чисел");
  }
  
  const delay = (ms) => new Promise(resolve => setTimeout(resolve, ms));
  
  let res = [];
  for (let i = 0; i < arr.length; i++) {
    delay(arr[i]).then(() => {
      res.push(arr[i]);
      if (res.length === arr.length) {
        call_back(res, null)
      }
    });
  }
}
```
