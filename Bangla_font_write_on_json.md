```py
dic ={"1":"সাইফুল"}
with open('t.json', 'w',encoding='utf8') as outfile:
  json.dump(dic, outfile,ensure_ascii=False)
```
