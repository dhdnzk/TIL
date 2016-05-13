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
