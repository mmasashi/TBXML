TBXML (mmasashi)
============================

Added the following feature  to TBXML.

- parsing text element
 - Fixing http://stackoverflow.com/questions/6276235/tbxml-issue-when-parsing-textforelement



Example
--------------------

- sample1.xml

```<root>
  first text node text
  <child>first child node text</child>
  second text node text
  <child>second child node text</child>
  third text node text
</root>
```

- Sample Code

<pre><code>    TBXML *tbxml = [TBXML tbxmlWithXMLFile:@"sample1" fileExtension:@"xml"];
    TBXMLElement *root = tbxml.rootXMLElement;
    
    if (root) {
      TBXMLElement *element = root->firstChild;
      while (element) {
        NSLog(@"name->%s text->%s", element->name, element->text);
        element = element->nextSibling;
      }
      
      TBXMLElement *firstTextElement = [TBXML childElementNamed:TBXML_TEXT_ELEMENT_NAME
                                                  parentElement:root];
      if (firstTextElement) {
        NSLog(@"firstTextElement name->%s text->%s", firstTextElement->name, firstTextElement->text);
      }
    }
</code></pre>

- <code>textForElement:root </code> does'nt return the text that you want, because I don't know what is the best way to concat multiple child text elements. You can implement <code>textForElement:</code> method easily in your way, If you need the fixed method, .


- Result (console)

```2011-10-13 01:24:17.039 TBXMLDemo[4455:207] name-> text text->first text node text
2011-10-13 01:24:17.045 TBXMLDemo[4455:207] name->child text->first child node text
2011-10-13 01:24:17.047 TBXMLDemo[4455:207] name-> text text->second text node text
2011-10-13 01:24:17.048 TBXMLDemo[4455:207] name->child text->second child node text
2011-10-13 01:24:17.049 TBXMLDemo[4455:207] name-> text text->third text node text
2011-10-13 01:24:17.049 TBXMLDemo[4455:207] firstTextElement name-> text text->first text node text
```

License
--------------------

TBXML is a light-weight XML document parser written in Objective-C designed for use on Apple iPad, iPhone & iPod Touch devices. TBXML aims to provide the fastest possible XML parsing whilst utilising the fewest resources. This requirement for absolute efficiency is achieved at the expense of XML validation and modification. It is not possible to modify and generate valid XML from a TBXML object and no validation is performed whatsoever whilst importing and parsing an XML document.

http://www.tbxml.co.uk/TBXML/TBXML_Free.html

