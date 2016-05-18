### Python 생소한 기초문

#### while, else
```python
while:

else:
```

#### for index, item in list
```python
for index, item in list:
    print(index, item)

# 0 foo
# 1 bar
# ... 와 같은 형식으로 출력됨
```

#### dictionary
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
#### for key in d:
```python
for key in d:
    print d[key]
# dictionary에서 각 키에 해당하는 내용들 출력
```

#### Multiple lists
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

#### for else:
```python 
for i in item:
    
else:

# for문이 정상적으로 종료된 경우에 else문 내부가 실행됨
# for문 안에서 break으로 나갈 경우에 실행 안됨

```

#### for if:
```python
evens_to_50 = [i for i in range(51) if i % 2 == 0]

print evens_to_50
```

#### lamda
```python
lambda x: x % 3 == 0
# is the same es
# def by_three(x):
#         return x % 3 == 0
```
```python
my_list = range(16)

print filter(lambda x: x % 3 == 0, my_list)
```
```python
languages = ["HTML", "JavaScript", "Python", "Ruby"]

print filter(lambda x: x == "Python", languages)

```

#### Bitwise Operators

```python
print 5 >> 4  # Right Shift
print 5 << 1  # Left Shift
print 8 & 5   # Bitwise AND
print 9 | 4   # Bitwise OR
print 12 ^ 42 # Bitwise XOR
print ~88     # Bitwise NOT

```

- 2진법으로 표현하기
```python
one = 0b1
two = 0b10
three = 0b11
four = 0b100
five = 0b101
six = 0b110
seven = 0b111
eight = 0b1000
nine = 0b1001
ten = 0b1010
eleven = 0b1011
twelve = 0b1100
```
- 16진법으로 표현하기
```python
print(hex(1))
print(hex(2))
```

- int의 두번째 매개변수
```python
int("0b100", 2) # 두번째 매개변수: 매개변수로 들어온 숫자가 2진수라는뜻
```

#### Class

- super 키워드 사용하기
```python

def full_time_wage(self, hours):

    return super(PartTimeEmployee, self).method(args)
# super(자식 클래스, self).method(args)
```

#### File I/O

- file output
```python
sample_list = [i**2 for i in range(1,11)]
# Generates a list of squares of the numbers 1 - 10

f = open("output.txt", "w")

for item in my_list:
    f.write(str(item) + "\n")

f.close()
```

- auto closing of file stream
```python
with open("text.txt", "w") as test_file:
    test_file.write("hello, world!")
```
- f.closed : 파일 스트림이 닫혔으면 true, 열려있으면 false를 반환
