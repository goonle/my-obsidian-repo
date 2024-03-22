## 동적 Argument
---
동적으로 html테그의 특성(attribute)을 연결하는 문법
### v-bind
```html
<tagName v-bind:[attrName] = "[attrValue]"></tagName>
<tagName :[attrName] = "[attrValue]"></tagName> //줄임말
```

### v-on
```html
<tagName v-on:[eventName] = "[function code]"></tagName>
<tagName @[eventName] = "[function code]"></tagName> //줄임말 (ex click 등)
```

#v-bind
#v-on
