---
layout: post
title:  "eslint-plugin-momentjs"
date:   2019-03-09 08:22:00 -0600
categories: projects
---

About a month ago, I was working on some stuff using Javascript and our favorite "make-dates-sane" library, [Moment.js](https://momentjs.com/). As you might expect, they have a number of suggestions on how to use Moment.js in such a way that reduces the potential for errors - strict mode parsing, etc. Unfortunately no automatic mechanism for enforcing those suggestions existed.

So, I took the suggestions that my company adopted specifically and created an ESLint plugin, named quite boringly, [eslint-plugin-momentjs](https://github.com/schnaser/eslint-plugin-momentjs). This plugin as well as installation instructions are also available on the [npm registry](https://www.npmjs.com/package/eslint-plugin-momentjs). Of course, the most up to date documentation for the rules can be found on the [project repository](https://github.com/schnaser/eslint-plugin-momentjs/tree/master/docs/rules), but for convenience I'll reproduce them here (there are only four):

### no-moment-constructor

When creating moment instances, use moment-timezone constructor over the moment only constructor.

{% highlight javascript %}
// Good
moment.tz('2019-01-01', 'YYYY-MM-DD', true, 'America/Chicago');
 
// Avoid
moment('2019-01-01', 'YYYY-MM-DD', true); // no timezone info
{% endhighlight %}

    
[Moment.js Documentation for this rule](https://momentjs.com/timezone/docs/#/using-timezones/parsing-in-zone/)

---

### require-format

Always specify the format of the date-time string, so moment does not have to guess the format.
{% highlight javascript %}
// Good
moment.tz('01/12/2018', 'MM/DD/YYYY', true, 'America/Chicago');
 
// Avoid
moment.tz('01/12/2018', 'America/Chicago');
{% endhighlight %}


[Moment.js Documentation for this rule](https://momentjs.com/docs/#/parsing/string-format/)

---
### require-strict-parsing

Prefer strict format check over loose format check.
{% highlight javascript %}
// Good
moment.tz('01/12/2018', 'MM/DD/YYYY', true, 'America/Chicago');
 
// Avoid
moment.tz('This has date 01/12/2018', 'MM/DD/YYYY', 'America/Chicago');
{% endhighlight %}
   
[Moment.js Documentation for this rule](https://momentjs.com/guides/#/parsing/strict-mode/)

---

### require-timezone

Require a time zone argument to calls to `moment.tz` 
{% highlight javascript %}
// Good
moment.tz('America/Chicago');
moment.tz(aTimeZone);
moment.tz(zone);
moment.tz(tz);
 
// Avoid
moment.tz(aString, 'MM/DD/YYYY');
{% endhighlight %}
   
[Moment.js Documentation for this rule](https://momentjs.com/timezone/docs/#/using-timezones/)

---

Feature requests (or better yet, pull requests!) are welcome at the [project home page](https://github.com/schnaser/eslint-plugin-momentjs).
