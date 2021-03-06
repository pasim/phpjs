---
layout: page
title: "JavaScript inet_ntop function"
comments: true
sharing: true
footer: true
alias:
- /functions/view/inet_ntop:882
- /functions/view/inet_ntop
- /functions/view/882
- /functions/inet_ntop:882
- /functions/882
---
<!-- Generated by Rakefile:build -->
A JavaScript equivalent of PHP's inet_ntop

{% codeblock network/inet_ntop.js lang:js https://raw.github.com/kvz/phpjs/master/functions/network/inet_ntop.js raw on github %}
function inet_ntop (a) {
  // From: http://phpjs.org/functions
  // +   original by: Theriault
  // *     example 1: inet_ntop('\x7F\x00\x00\x01');
  // *     returns 1: '127.0.0.1'
  // *     example 2: inet_ntop('\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\1');
  // *     returns 2: '::1'
  var i = 0,
    m = '',
    c = [];
  a += '';
  if (a.length === 4) { // IPv4
    return [
    a.charCodeAt(0), a.charCodeAt(1), a.charCodeAt(2), a.charCodeAt(3)].join('.');
  } else if (a.length === 16) { // IPv6
    for (i = 0; i < 16; i++) {
      c.push(((a.charCodeAt(i++) << 8) + a.charCodeAt(i)).toString(16));
    }
    return c.join(':').replace(/((^|:)0(?=:|$))+:?/g, function (t) {
      m = (t.length > m.length) ? t : m;
      return t;
    }).replace(m || ' ', '::');
  } else { // Invalid length
    return false;
  }
}
{% endcodeblock %}

 - [Raw function on GitHub](https://github.com/kvz/phpjs/blob/master/functions/network/inet_ntop.js)

Please note that php.js uses JavaScript objects as substitutes for PHP arrays, they are 
the closest match to this hashtable-like data structure. 

Please also note that php.js offers community built functions and goes by the 
[McDonald's Theory](https://medium.com/what-i-learned-building/9216e1c9da7d). We'll put online 
functions that are far from perfect, in the hopes to spark better contributions. 
Do you have one? Then please just: 

 - [Edit on GitHub](https://github.com/kvz/phpjs/edit/master/functions/network/inet_ntop.js)

### Example 1
This code
{% codeblock lang:js example %}
inet_ntop('\x7F\x00\x00\x01');
{% endcodeblock %}

Should return
{% codeblock lang:js returns %}
'127.0.0.1'
{% endcodeblock %}

### Example 2
This code
{% codeblock lang:js example %}
inet_ntop('\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\1');
{% endcodeblock %}

Should return
{% codeblock lang:js returns %}
'::1'
{% endcodeblock %}


### Other PHP functions in the network extension
{% render_partial _includes/custom/network.html %}
