---
layout: post
title: " 第一百二十七节，JavaScript，JSON数据类型转换，数据转换成字符串，字符串转换成数据 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---

**第一百二十七节，JavaScript，JSON数据类型转换，数据转换成字符串，字符串转换成数据**



**学习要点：**

**1.JSON语法**

**2.解析和序列化**



**前两章我们探讨了XML的结构化数据，但开发人员还是觉得这种微型的数据结构还是过于烦琐、冗长。为了解决这个问题，JSON的结构化数据出现了。JSON是JavaScript的一个严格的子集，利用JavaScript中的一些模式来表示结构化数据。**



**一．** **JSON** **语法**

**JSON和XML类型，都是一种结构化的数据表示方式。所以，JSON并不是JavaScript独有的数据格式，其他很多语言都可以对JSON进行解析和序列化。**



**JSON的语法可以表示三种类型的值：**



**1.简单值：可以在JSON中表示字符串、数值、布尔值和null。但JSON不支持JavaScript中的特殊值undefined。**



**2.对象：顾名思义。**



**3.数组：顾名思义。**



**简单值 **JSON表示****

**100、"Lee"
这两个量就是JSON的表示方法，一个是JSON数值，一个是JSON字符串。布尔值和null也是有效的形式。但实际运用中要结合对象或数组。**

[code]

     //json简单值表示方式
    10 //数字类型
    "字符串" //字符串类型
    true //布尔值类型
    null //空
[/code]



**对象 ** **JSON表示******

[code]

     //对象
    //JavaScript对象字面量表示法：
    var box = {
        name: 'Lee',
        age: 100
    };
    
    //而JSON中的对象表示法需要加上双引号，并且不存在赋值运算和分号：
    '{"name":"Lee","age":100}' //使用双引号，否则转换会出错
[/code]



**数组 ** ** **JSON表示********

[code]

     // 数组
    // JavaScript数组字面量表示法：
    var box = [100, 'Lee', true];
    
    // 而JSON中的数组表示法同样没有变量赋值和分号：
    '[100, "Lee", true]'
[/code]



**一般比较常用的一种复杂形式是数组结合对象的形式 ** ** ** **JSON表示******** ：**

[code]

    //数组结合对象的形式
    [
        {
            "title" : "a",
            "num" : 1
        },
        {
            "title" : "b",
            "num" : 2
        },
        {
            "title" : "c",
            "num" : 3
        }
    ]
[/code]

**PS：一般情况下，我们可以把JSON结构数据保存到一个文本文件里，然后通过XMLHttpRequest对象去加载它，得到这串结构数据字符串(XMLHttpRequest对象将在Aajx章节中详细探讨)。所以，我们可以模拟这种过程。**



**模拟加载JSON文本文件的数据，并且赋值给变量。**

[code]

     var box = '[{"name" : "a","age" : 1},{"name" : "b","age" : 2}]';    
[/code]

**PS；上面这短代码模拟了var box =
load('demo.json');赋值过程。因为通过load加载的文本文件，不管内容是什么，都必须是字符串。所以两边要加上双引号。**



**其实JSON就是比普通数组多了两边的双引号，普通数组如下：**

[code]

     var box = [{name : 'a', age : 1},{name : 'b', age : 2}];    
[/code]



**二．解析和序列化**

**如果是载入的JSON文件，我们需要对其进行使用，那么就必须对JSON字符串解析成原生的JavaScript值。当然，如果是原生的JavaScript对象或数组，也可以转换成JSON字符串。**

**对于讲JSON字符串解析为JavaScript原生值，早期采用的是eval()函数。但这种方法既不安全，可能会执行一些恶意代码。**

**eval()函数，JSON字符串解析为JavaScript原生值，参数是要解析的字符串**  
 **使用方式：**  
 **eval(要解析的字符串)**

[code]

     //模拟加载JSON字符串
    var box = '[{"name" : "a","age" : 1},{"name" : "b","age" : 2}]';
    alert(box);                                //JSON字符串
    var json = eval(box);                    //使用eval()函数解析
    alert(json);                            //得到JavaScript原生值
[/code]



**JSON对象**

**ECMAScript5对解析JSON的行为进行规范，定义了全局对象JSON。支持这个对象的浏览器有IE8+、Firefox3.5+、Safari4+、Chrome和Opera10.5+。不支持的浏览器也可以通过一个开源库json.js来模拟执行。JSON对象提供了两个方法，一个是将原生JavaScript值转换为JSON字符串：stringify()；另一个是将JSON字符串转换为JavaScript原生值：parse()。**

**如果浏览器版本太低不支持 **JSON对象， **通过一个开源库json2.js来模拟执行，如果支持 ** **JSON对象就用 **
**JSON对象**************

******json2.js **开源库********

[code]

     /*
        json2.js
        2012-10-08
    
        Public Domain.
    
        NO WARRANTY EXPRESSED OR IMPLIED. USE AT YOUR OWN RISK.
    
        See http://www.JSON.org/js.html
    
    
        This code should be minified before deployment.
        See http://javascript.crockford.com/jsmin.html
    
        USE YOUR OWN COPY. IT IS EXTREMELY UNWISE TO LOAD CODE FROM SERVERS YOU DO
        NOT CONTROL.
    
    
        This file creates a global JSON object containing two methods: stringify
        and parse.
    
            JSON.stringify(value, replacer, space)
                value       any JavaScript value, usually an object or array.
    
                replacer    an optional parameter that determines how object
                            values are stringified for objects. It can be a
                            function or an array of strings.
    
                space       an optional parameter that specifies the indentation
                            of nested structures. If it is omitted, the text will
                            be packed without extra whitespace. If it is a number,
                            it will specify the number of spaces to indent at each
                            level. If it is a string (such as '\t' or '&nbsp;'),
                            it contains the characters used to indent at each level.
    
                This method produces a JSON text from a JavaScript value.
    
                When an object value is found, if the object contains a toJSON
                method, its toJSON method will be called and the result will be
                stringified. A toJSON method does not serialize: it returns the
                value represented by the name/value pair that should be serialized,
                or undefined if nothing should be serialized. The toJSON method
                will be passed the key associated with the value, and this will be
                bound to the value
    
                For example, this would serialize Dates as ISO strings.
    
                    Date.prototype.toJSON = function (key) {
                        function f(n) {
                            // Format integers to have at least two digits.
                            return n < 10 ? '0' + n : n;
                        }
    
                        return this.getUTCFullYear()   + '-' +
                             f(this.getUTCMonth() + 1) + '-' +
                             f(this.getUTCDate())      + 'T' +
                             f(this.getUTCHours())     + ':' +
                             f(this.getUTCMinutes())   + ':' +
                             f(this.getUTCSeconds())   + 'Z';
                    };
    
                You can provide an optional replacer method. It will be passed the
                key and value of each member, with this bound to the containing
                object. The value that is returned from your method will be
                serialized. If your method returns undefined, then the member will
                be excluded from the serialization.
    
                If the replacer parameter is an array of strings, then it will be
                used to select the members to be serialized. It filters the results
                such that only members with keys listed in the replacer array are
                stringified.
    
                Values that do not have JSON representations, such as undefined or
                functions, will not be serialized. Such values in objects will be
                dropped; in arrays they will be replaced with null. You can use
                a replacer function to replace those with JSON values.
                JSON.stringify(undefined) returns undefined.
    
                The optional space parameter produces a stringification of the
                value that is filled with line breaks and indentation to make it
                easier to read.
    
                If the space parameter is a non-empty string, then that string will
                be used for indentation. If the space parameter is a number, then
                the indentation will be that many spaces.
    
                Example:
    
                text = JSON.stringify(['e', {pluribus: 'unum'}]);
                // text is '["e",{"pluribus":"unum"}]'
    
    
                text = JSON.stringify(['e', {pluribus: 'unum'}], null, '\t');
                // text is '[\n\t"e",\n\t{\n\t\t"pluribus": "unum"\n\t}\n]'
    
                text = JSON.stringify([new Date()], function (key, value) {
                    return this[key] instanceof Date ?
                        'Date(' + this[key] + ')' : value;
                });
                // text is '["Date(---current time---)"]'
    
    
            JSON.parse(text, reviver)
                This method parses a JSON text to produce an object or array.
                It can throw a SyntaxError exception.
    
                The optional reviver parameter is a function that can filter and
                transform the results. It receives each of the keys and values,
                and its return value is used instead of the original value.
                If it returns what it received, then the structure is not modified.
                If it returns undefined then the member is deleted.
    
                Example:
    
                // Parse the text. Values that look like ISO date strings will
                // be converted to Date objects.
    
                myData = JSON.parse(text, function (key, value) {
                    var a;
                    if (typeof value === 'string') {
                        a =
    /^(\d{4})-(\d{2})-(\d{2})T(\d{2}):(\d{2}):(\d{2}(?:\.\d*)?)Z$/.exec(value);
                        if (a) {
                            return new Date(Date.UTC(+a[1], +a[2] - 1, +a[3], +a[4],
                                +a[5], +a[6]));
                        }
                    }
                    return value;
                });
    
                myData = JSON.parse('["Date(09/09/2001)"]', function (key, value) {
                    var d;
                    if (typeof value === 'string' &&
                            value.slice(0, 5) === 'Date(' &&
                            value.slice(-1) === ')') {
                        d = new Date(value.slice(5, -1));
                        if (d) {
                            return d;
                        }
                    }
                    return value;
                });
    
    
        This is a reference implementation. You are free to copy, modify, or
        redistribute.
    */
    
    /*jslint evil: true, regexp: true */
    
    /*members "", "\b", "\t", "\n", "\f", "\r", "\"", JSON, "\\", apply,
        call, charCodeAt, getUTCDate, getUTCFullYear, getUTCHours,
        getUTCMinutes, getUTCMonth, getUTCSeconds, hasOwnProperty, join,
        lastIndex, length, parse, prototype, push, replace, slice, stringify,
        test, toJSON, toString, valueOf
    */
    
    
    // Create a JSON object only if one does not already exist. We create the
    // methods in a closure to avoid creating global variables.
    
    if (typeof JSON !== 'object') {
        JSON = {};
    }
    
    (function () {
        'use strict';
    
        function f(n) {
            // Format integers to have at least two digits.
            return n < 10 ? '0' + n : n;
        }
    
        if (typeof Date.prototype.toJSON !== 'function') {
    
            Date.prototype.toJSON = function (key) {
    
                return isFinite(this.valueOf())
                    ? this.getUTCFullYear()     + '-' +
                        f(this.getUTCMonth() + 1) + '-' +
                        f(this.getUTCDate())      + 'T' +
                        f(this.getUTCHours())     + ':' +
                        f(this.getUTCMinutes())   + ':' +
                        f(this.getUTCSeconds())   + 'Z'
                    : null;
            };
    
            String.prototype.toJSON      =
                Number.prototype.toJSON  =
                Boolean.prototype.toJSON = function (key) {
                    return this.valueOf();
                };
        }
    
        var cx = /[\u0000\u00ad\u0600-\u0604\u070f\u17b4\u17b5\u200c-\u200f\u2028-\u202f\u2060-\u206f\ufeff\ufff0-\uffff]/g,
            escapable = /[\\\"\x00-\x1f\x7f-\x9f\u00ad\u0600-\u0604\u070f\u17b4\u17b5\u200c-\u200f\u2028-\u202f\u2060-\u206f\ufeff\ufff0-\uffff]/g,
            gap,
            indent,
            meta = {    // table of character substitutions
                '\b': '\\b',
                '\t': '\\t',
                '\n': '\\n',
                '\f': '\\f',
                '\r': '\\r',
                '"' : '\\"',
                '\\': '\\\\'
            },
            rep;
    
    
        function quote(string) {
    
    // If the string contains no control characters, no quote characters, and no
    // backslash characters, then we can safely slap some quotes around it.
    // Otherwise we must also replace the offending characters with safe escape
    // sequences.
    
            escapable.lastIndex = 0;
            return escapable.test(string) ? '"' + string.replace(escapable, function (a) {
                var c = meta[a];
                return typeof c === 'string'
                    ? c
                    : '\\u' + ('0000' + a.charCodeAt(0).toString(16)).slice(-4);
            }) + '"' : '"' + string + '"';
        }
    
    
        function str(key, holder) {
    
    // Produce a string from holder[key].
    
            var i,          // The loop counter.
                k,          // The member key.
                v,          // The member value.
                length,
                mind = gap,
                partial,
                value = holder[key];
    
    // If the value has a toJSON method, call it to obtain a replacement value.
    
            if (value && typeof value === 'object' &&
                    typeof value.toJSON === 'function') {
                value = value.toJSON(key);
            }
    
    // If we were called with a replacer function, then call the replacer to
    // obtain a replacement value.
    
            if (typeof rep === 'function') {
                value = rep.call(holder, key, value);
            }
    
    // What happens next depends on the value's type.
    
            switch (typeof value) {
            case 'string':
                return quote(value);
    
            case 'number':
    
    // JSON numbers must be finite. Encode non-finite numbers as null.
    
                return isFinite(value) ? String(value) : 'null';
    
            case 'boolean':
            case 'null':
    
    // If the value is a boolean or null, convert it to a string. Note:
    // typeof null does not produce 'null'. The case is included here in
    // the remote chance that this gets fixed someday.
    
                return String(value);
    
    // If the type is 'object', we might be dealing with an object or an array or
    // null.
    
            case 'object':
    
    // Due to a specification blunder in ECMAScript, typeof null is 'object',
    // so watch out for that case.
    
                if (!value) {
                    return 'null';
                }
    
    // Make an array to hold the partial results of stringifying this object value.
    
                gap += indent;
                partial = [];
    
    // Is the value an array?
    
                if (Object.prototype.toString.apply(value) === '[object Array]') {
    
    // The value is an array. Stringify every element. Use null as a placeholder
    // for non-JSON values.
    
                    length = value.length;
                    for (i = 0; i < length; i += 1) {
                        partial[i] = str(i, value) || 'null';
                    }
    
    // Join all of the elements together, separated with commas, and wrap them in
    // brackets.
    
                    v = partial.length === 0
                        ? '[]'
                        : gap
                        ? '[\n' + gap + partial.join(',\n' + gap) + '\n' + mind + ']'
                        : '[' + partial.join(',') + ']';
                    gap = mind;
                    return v;
                }
    
    // If the replacer is an array, use it to select the members to be stringified.
    
                if (rep && typeof rep === 'object') {
                    length = rep.length;
                    for (i = 0; i < length; i += 1) {
                        if (typeof rep[i] === 'string') {
                            k = rep[i];
                            v = str(k, value);
                            if (v) {
                                partial.push(quote(k) + (gap ? ': ' : ':') + v);
                            }
                        }
                    }
                } else {
    
    // Otherwise, iterate through all of the keys in the object.
    
                    for (k in value) {
                        if (Object.prototype.hasOwnProperty.call(value, k)) {
                            v = str(k, value);
                            if (v) {
                                partial.push(quote(k) + (gap ? ': ' : ':') + v);
                            }
                        }
                    }
                }
    
    // Join all of the member texts together, separated with commas,
    // and wrap them in braces.
    
                v = partial.length === 0
                    ? '{}'
                    : gap
                    ? '{\n' + gap + partial.join(',\n' + gap) + '\n' + mind + '}'
                    : '{' + partial.join(',') + '}';
                gap = mind;
                return v;
            }
        }
    
    // If the JSON object does not yet have a stringify method, give it one.
    
        if (typeof JSON.stringify !== 'function') {
            JSON.stringify = function (value, replacer, space) {
    
    // The stringify method takes a value and an optional replacer, and an optional
    // space parameter, and returns a JSON text. The replacer can be a function
    // that can replace values, or an array of strings that will select the keys.
    // A default replacer method can be provided. Use of the space parameter can
    // produce text that is more easily readable.
    
                var i;
                gap = '';
                indent = '';
    
    // If the space parameter is a number, make an indent string containing that
    // many spaces.
    
                if (typeof space === 'number') {
                    for (i = 0; i < space; i += 1) {
                        indent += ' ';
                    }
    
    // If the space parameter is a string, it will be used as the indent string.
    
                } else if (typeof space === 'string') {
                    indent = space;
                }
    
    // If there is a replacer, it must be a function or an array.
    // Otherwise, throw an error.
    
                rep = replacer;
                if (replacer && typeof replacer !== 'function' &&
                        (typeof replacer !== 'object' ||
                        typeof replacer.length !== 'number')) {
                    throw new Error('JSON.stringify');
                }
    
    // Make a fake root object containing our value under the key of ''.
    // Return the result of stringifying the value.
    
                return str('', {'': value});
            };
        }
    
    
    // If the JSON object does not yet have a parse method, give it one.
    
        if (typeof JSON.parse !== 'function') {
            JSON.parse = function (text, reviver) {
    
    // The parse method takes a text and an optional reviver function, and returns
    // a JavaScript value if the text is a valid JSON text.
    
                var j;
    
                function walk(holder, key) {
    
    // The walk method is used to recursively walk the resulting structure so
    // that modifications can be made.
    
                    var k, v, value = holder[key];
                    if (value && typeof value === 'object') {
                        for (k in value) {
                            if (Object.prototype.hasOwnProperty.call(value, k)) {
                                v = walk(value, k);
                                if (v !== undefined) {
                                    value[k] = v;
                                } else {
                                    delete value[k];
                                }
                            }
                        }
                    }
                    return reviver.call(holder, key, value);
                }
    
    
    // Parsing happens in four stages. In the first stage, we replace certain
    // Unicode characters with escape sequences. JavaScript handles many characters
    // incorrectly, either silently deleting them, or treating them as line endings.
    
                text = String(text);
                cx.lastIndex = 0;
                if (cx.test(text)) {
                    text = text.replace(cx, function (a) {
                        return '\\u' +
                            ('0000' + a.charCodeAt(0).toString(16)).slice(-4);
                    });
                }
    
    // In the second stage, we run the text against regular expressions that look
    // for non-JSON patterns. We are especially concerned with '()' and 'new'
    // because they can cause invocation, and '=' because it can cause mutation.
    // But just to be safe, we want to reject all unexpected forms.
    
    // We split the second stage into 4 regexp operations in order to work around
    // crippling inefficiencies in IE's and Safari's regexp engines. First we
    // replace the JSON backslash pairs with '@' (a non-JSON character). Second, we
    // replace all simple value tokens with ']' characters. Third, we delete all
    // open brackets that follow a colon or comma or that begin the text. Finally,
    // we look to see that the remaining characters are only whitespace or ']' or
    // ',' or ':' or '{' or '}'. If that is so, then the text is safe for eval.
    
                if (/^[\],:{}\s]*$/
                        .test(text.replace(/\\(?:["\\\/bfnrt]|u[0-9a-fA-F]{4})/g, '@')
                            .replace(/"[^"\\\n\r]*"|true|false|null|-?\d+(?:\.\d*)?(?:[eE][+\-]?\d+)?/g, ']')
                            .replace(/(?:^|:|,)(?:\s*\[)+/g, ''))) {
    
    // In the third stage we use the eval function to compile the text into a
    // JavaScript structure. The '{' operator is subject to a syntactic ambiguity
    // in JavaScript: it can begin a block or an object literal. We wrap the text
    // in parens to eliminate the ambiguity.
    
                    j = eval('(' + text + ')');
    
    // In the optional fourth stage, we recursively walk the new structure, passing
    // each name/value pair to a reviver function for possible transformation.
    
                    return typeof reviver === 'function'
                        ? walk({'': j}, '')
                        : j;
                }
    
    // If the text is not JSON parseable, then a SyntaxError is thrown.
    
                throw new SyntaxError('JSON.parse');
            };
        }
    }());
[/code]



**无论是JSON对象，还是开源库json2.js来模拟执行，都有两个方法**

**JSON对象提供了两个方法，一个是将原生JavaScript值转换为JSON字符串：stringify()；另一个是将JSON字符串转换为JavaScript原生值：parse()。**

**parse()方法，将JSON字符串转换为JavaScript原生数据，参数是JSON字符串，第二个可选参数可以是函数**  
 **使用方式**  
 **JSON对象.parse(JSON字符串)**

[code]

     //注意：引入了开源库json2，如果浏览器版本太低不支持JSON对象，通过一个开源库json2.js来模拟执行，如果支持JSON对象就用JSON对象
    var box = '[{"name" : "a","age" : 1},{"name" : "b","age" : 2}]';    //JSON字符串,特别注意，键要用双引号
    alert(box);
    var json = JSON.parse(box);      //parse()方法，将JSON字符串转换为JavaScript原生数据，参数是JSON字符串
    alert(json);  //打印转换后的JavaScript原生数据
[/code]

****解析JSON字符串方法parse()也可以接受第二个参数，这样可以在还原出JavaScript值的时候替换成自己想要的值。****

[code]

     //注意：引入了开源库json2，如果浏览器版本太低不支持JSON对象，通过一个开源库json2.js来模拟执行，如果支持JSON对象就用JSON对象
    var box = '[{"name" : "a","age" : 1},{"name" : "b","age" : 2}]';  //json字符串
    var json = JSON.parse(box, function (key, value) {  //第二个参数为匿名函数，接受对象的键和值
        if (key == 'name') {  //判断对象的键等于name
            return 'Mr. ' + value;  //改变值
        } else {
            return value;  //返回值
        }
    });
    alert(json[0].name); //打印第一个对象的name值
[/code]



**stringify()方法，将JavaScript原生数据转换为JSON字符串，参数是JavaScript原生数据,[可选参数，第一个参数可以是一个数组，也可以是一个函数，用于过滤结果。第二个参数则表示是否在JSON字符串中保留缩进。]**  
 **使用方式**  
 **JSON对象.stringify(JavaScript原生数据)**

[code]

     //注意：引入了开源库json2，如果浏览器版本太低不支持JSON对象，通过一个开源库json2.js来模拟执行，如果支持JSON对象就用JSON对象
    var box = [{name : 'a', age : 1},{name : 'b', age : 2}];    //JavaScript原生数据
    alert(box);
    var json = JSON.stringify(box);                        //转换成JSON字符串
    alert(json);                                        //自动双引号
[/code]

**在序列化JSON的过程中，stringify()方法还提供了两个可选参数。第一个参数可以是一个数组，也可以是一个函数，用于过滤结果。第二个参数则表示是否在JSON字符串中保留缩进。**

[code]

     //注意：引入了开源库json2，如果浏览器版本太低不支持JSON对象，通过一个开源库json2.js来模拟执行，如果支持JSON对象就用JSON对象
    var box = [{name : 'a', age : 1, height : 177},{name : 'b', age : 2, height : 188}];  //JavaScript原生数据
    //stringify()方法还提供了两个可选参数。第一个参数可以是一个数组，也可以是一个函数，用于过滤结果。第二个参数则表示是否在JSON字符串中保留缩进。
    var json = JSON.stringify(box, ['name', 'age'], 4);  //只解析name和age，过滤掉height，保留缩进4
    alert(json); //打印JSON字符串
[/code]

**如果不需要保留缩进，则不填即可；如果不需要过滤结果，但又要保留缩进，则将过滤结果的参数设置为null。如果采用函数，可以进行复杂的过滤。**

[code]

     //注意：引入了开源库json2，如果浏览器版本太低不支持JSON对象，通过一个开源库json2.js来模拟执行，如果支持JSON对象就用JSON对象
    var box = [{name: 'a', age: 1, height: 177}, {name: 'b', age: 2, height: 188}];  //JavaScript原生数据
    //stringify()方法还提供了两个可选参数。第一个参数可以是一个数组，也可以是一个函数，用于过滤结果。第二个参数则表示是否在JSON字符串中保留缩进。
    var json = JSON.stringify(box, function (key, value) {  //设置一个匿名函数，分别接受对象的键和值
        switch (key) {  //多重判断key键
            case 'name' :  //如果键是name
                return 'Mr. ' + value;  //将name值改变成
            case 'age' :   //如果键是age
                return value + '岁';
            default :
                return value;
        }
    }, 4);
    alert(json);  //返回改变后的json字符串
[/code]

**PS：保留缩进除了是普通的数字，也可以是字符。**



**还有一种方法可以自定义过滤一些数据，使用toJSON()方法，可以将某一组对象里指定返回某个值。**

[code]

     //注意：引入了开源库json2，如果浏览器版本太低不支持JSON对象，通过一个开源库json2.js来模拟执行，如果支持JSON对象就用JSON对象
    var box = [{
        name: 'a', age: 1, height: 177, toJSON: function () {
            return this.name;  //返回当前对象的name
        }
    }, {
        name: 'b', age: 2, height: 188, toJSON: function () {
            return this.name;  //返回当前对象的name
        }
    }];
    var json = JSON.stringify(box);  //最后返回对象里的name值字符串
    alert(json);  
[/code]

**PS：由此可见序列化也有执行顺序，首先先执行toJSON()方法；如果应用了第二个过滤参数，则执行这个方法；然后执行序列化过程，比如将键值对组成合法的JSON字符串，比如加上双引号。如果提供了缩进，再执行缩进操作。**

**** ****

