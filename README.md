# lxml-html

a html parser based lxml

Element is a wrapper of lxml.html.HtmlElement

Element implement a proxy of HtmlElement

## install
```
pip install lxmlHtml
```

## quick start
```python
from lxmlHtml import Element

text = """
<div>
    <span></span>
    <span></span>
    <span></span>
</div>
"""
element = Element.fragment_fromstring(text)

# add some attribute
first_span = element.cssselect('span')[0]
print(first_span)

first_span.set('width', '200px')
first_span.styles.set('font-size', '20px')
first_span.styles.set('max-width', '200px')
first_span.classes.add('red')
first_span.classes.add('green')

# remove element
element.xpath_first('//span[2]').drop_tag()

# # get children
print(element.getchildren())

# # add element
last_span = element.xpath_first("//span[last()]")
print(last_span)

ele = element.makeelement("p")
c = element.makecomment("p")
last_span.append(ele)
last_span.append(c)

# serialize
print(element.tostring(pretty_print=True))
"""
<div>
    <span width="200px" style="font-size: 20px; max-width: 200px;" class="red green"></span>
    
    <span><p></p>
<!--p--></span>
</div>
"""

```

