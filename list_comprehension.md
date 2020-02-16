# list comprehension

```py
n = int(input())
name_numbers = [input().split() for _ in range(n)]
phone_book = {k: v for k,v in name_numbers}
while True:
    try:
        name = input()
        if name in phone_book:
            print('%s=%s' % (name, phone_book[name]))
        else:
            print('Not found')
    except:
        break
```

```py
li = [1,2,3,4,5]                                                        
x = list(''.join(str(i)+'s'*(i%2==1) for i,v in enumerate (li)))

```
