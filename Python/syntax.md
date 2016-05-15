### Python 생소한 기초문법

- while, else
```python
while:

else:
```

- for index, item in list
```python
for index, item in list:
    print(index, item)

# 0 foo
# 1 bar
# ... 와 같은 형식으로 출력됨
```

- dictionary
```python
backpack = {
    
    'pocket1': ['item1', 'item2', 'item3'],

    'pocket2': ['item1', 'item2', 'item3', 'item4', 'item5'],

    'pocket3': ['item1']

}

for key in backpack:
    print(backpack[key])

# 과 같은 형식으로 내부 value에 얼마든지 접근 가능!

```
- for key in d:
```python
for key in d:
    print d[key]
# dictionary에서 각 키에 해당하는 내용들 출력
```

- Multiple lists
```python
list_a = [3, 9, 17, 15, 19]
list_b = [2, 4, 8, 10, 30, 40, 50, 60, 70, 80, 90]

# zip keyword!
for a, b in zip(list_a, list_b):

    if a >= b:
        print a

    else:
        print b
```

- for else:
```python 
for i in item:
    
else:

# for문이 정상적으로 종료된 경우에 else문 내부가 실행됨
# for문 안에서 break으로 나갈 경우에 실행 안됨

```

- for if:
```python
evens_to_50 = [i for i in range(51) if i % 2 == 0]

print evens_to_50
```
