---
layout:     post
title:      The Magic of Python and Unicode
date:       2015-06-22 00:53:29
summary:    Unicode and python, an endless joyride.
categories: rants string formats unicode python
---

### A Quickie
Python is wonderful, but when it comes to handling unicode strings it can be a hassle. Recently, I have been using python to parse X.509 certificates and some of the fields, like commonName, have unicode string encodings varying from latin, utf8, to cjk ideograph. The issues arise when trying to write to a file. Using the regular *open()* function in python will raise errors. The best thing to do is to use the codecs library:

{% highlight python %}
import codecs
fout=codecs.open('myfile.txt','w',encoding='utf-8')
fout.write("This is my horse, my horse is amazing!".encode('utf-8))
fout.close()
{% endhighlight %}

Now this great, but it doesn't really solve my problem because of the varying encodings found in the thousands of certificates I'm parsing. To properly handle this issue, I used the following code. 

__Note:__ *this doesn't require you to use the codecs open function, but I used it above to demonstrate that you can if you know what your encoding ahead of time.*

{% highlight python %}
fout=open("myfile.txt",'w')
fout.write("Give it a lick, it tastes like raisins".decode('unicode-escape'))
fout.close
{% endhighlight %}

Thats it! it's pretty straight forward, but now I know so I don't have to look it up anymore.
