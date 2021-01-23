---
title: Tutorial
description: NexT is a high quality elegant Jekyll theme ported from Hexo Next. It is crafted from scratch, with love.
categories:
 - tutorial
tags:
---

> NexT is a high quality elegant [Jekyll](https://jekyllrb.com) theme ported from [Hexo Next](https://github.com/iissnan/hexo-theme-next). It is crafted from scratch, with love.

<!-- more -->

[Live Preview](http://simpleyyt.github.io/jekyll-theme-next/)

# 1. Next Theme Tutorial 

## Screenshots

* Desktop
![Desktop Preview](http://iissnan.com/nexus/next/desktop-preview.png)

* Sidebar

![Desktop Sidebar Preview](http://iissnan.com/nexus/next/desktop-sidebar-preview.png)

* Sidebar (Post details page)

![Desktop Sidebar Preview](http://iissnan.com/nexus/next/desktop-sidebar-toc.png)

* Mobile

![Mobile Preview](http://iissnan.com/nexus/next/mobile.png)


## Installation

Check whether you have `Ruby 2.1.0` or higher installed:

```sh
ruby --version
```

Install `Bundler`:

```sh
gem install bundler
```

Clone Jacman theme:

```sh
git clone https://github.com/Simpleyyt/jekyll-theme-next.git
cd jekyll-theme-next
```

Install Jekyll and other dependencies from the GitHub Pages gem:

```sh
bundle install
```

Run your Jekyll site locally:

```sh
bundle exec jekyll server
```

More Details：[Setting up your GitHub Pages site locally with Jekyll](https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/)


## Features

### Multiple languages support, including: English / Russian / French / German / Simplified Chinese / Traditional Chinese.

Default language is English.

```yml
language: en
# language: zh-Hans
# language: fr-FR
# language: zh-hk
# language: zh-tw
# language: ru
# language: de
```

Set `language` field as following in site `_config.yml` to change to Chinese.

```yml
language: zh-Hans
```

### Comment support.

NexT has native support for `DuoShuo` and `Disqus` comment systems.

Add the following snippets to your `_config.yml`:

```yml
duoshuo:
  enable: true
  shortname: your-duoshuo-shortname
```

OR

```yml
disqus_shortname: your-disqus-shortname
```

### Social Media

NexT can automatically add links to your Social Media accounts:

```yml
social:
  GitHub: your-github-url
  Twitter: your-twitter-url
  Weibo: your-weibo-url
  DouBan: your-douban-url
  ZhiHu: your-zhihu-url
```

### Feed link.

> Show a feed link.

Set `rss` field in theme's `_config.yml`, as the following value:

1. `rss: false` will totally disable feed link.
2. `rss:  ` use sites' feed link. This is the default option.

    Follow the installation instruction in the plugin's README. After the configuration is done for this plugin, the feed link is ready too.

3. `rss: http://your-feed-url` set specific feed link.

### Up to 5 code highlight themes built-in.

NexT uses [Tomorrow Theme](https://github.com/chriskempson/tomorrow-theme) with 5 themes for you to choose from.
Next use `normal` by default. Have a preview about `normal` and `night`:

![Tomorrow Normal Preview](http://iissnan.com/nexus/next/tomorrow-normal.png)
![Tomorrow Night Preview](http://iissnan.com/nexus/next/tomorrow-night.png)

Head over to [Tomorrow Theme](https://github.com/chriskempson/tomorrow-theme) for more details.

## Configuration

NexT comes with few configurations.

```yml

# Menu configuration.
menu:
  home: /
  archives: /archives

# Favicon
favicon: /favicon.ico

# Avatar (put the image into next/source/images/)
# can be any image format supported by web browsers (JPEG,PNG,GIF,SVG,..)
avatar: /default_avatar.png

# Code highlight theme
# available: normal | night | night eighties | night blue | night bright
highlight_theme: normal

# Fancybox for image gallery
fancybox: true

# Specify the date when the site was setup
since: 2013

```

## Browser support

![Browser support](http://iissnan.com/nexus/next/browser-support.png)

</br>

</br>

---

</br>

</br>

```yml
title: Block
date: 2013-12-25 00:14:39
categories:
- tutorial
tags:
```

# 2. Block (block quote, code block)

This post is used for testing tag plugins. See [docs](http://zespia.tw/hexo/docs/tag-plugins.html) for more info.

## Block Quote

### Normal blockquote

> Praesent diam elit, interdum ut pulvinar placerat, imperdiet at magna.

## Code Block

### Inline code block

This is a inline code block: `python`, `print 'helloworld'`.

### Normal code block

```
alert('Hello World!');
```

    print "Hello world"

### Highlight code block

```python
print "Hello world"
```

{% highlight ruby %}
def foo
  puts 'foo'
end
{% endhighlight %}

{% highlight ruby linenos %}
def foo
  puts 'foo'
end
{% endhighlight %}

### Gist

{% gist 996818 %}

</br>

</br>

---

</br>

</br>

```yaml
title: Highlight Test
categories:
 - tutorial
tags:
```

# 3. highlight-test

This is a highlight test.

## Normal block

```
alert('Hello World!');
```

    print 'helloworld'

## Highlight block

```javascript
alert( 'Hello, world!' );
```

```python
print 'helloworld'
```

```ruby
def foo
  puts 'foo'
end
```

{% highlight ruby %}
def foo
  puts 'foo'
end
{% endhighlight %}

{% highlight ruby linenos %}
def foo
  puts 'foo'
end
{% endhighlight %}

```c++
#include <iostream>

using namespace std;

void foo(int arg1, int arg2)
{

}

int main()
{
  string str;
  foo(1, 2);
  cout << "Hello World" << endl;
  return 0;
}
```

</br>

</br>

---

</br>

</br>

```yaml
type: photo
title: Gallery Post
date: 2014-11-18 15:45:20
category: tutorial
photos:
- http://ww1.sinaimg.cn/mw690/81b78497jw1emfgwkasznj21hc0u0qb7.jpg
- http://ww3.sinaimg.cn/mw690/81b78497jw1emfgwjrh2pj21hc0u01g3.jpg
- http://ww2.sinaimg.cn/mw690/81b78497jw1emfgwil5xkj21hc0u0tpm.jpg
- http://ww3.sinaimg.cn/mw690/81b78497jw1emfgvcdn25j21hc0u0qpa.jpg
tags:
description: Gallery Post Test. 测试图片类文章的显示。
```

# 4. gallery-post

Nunc dignissim volutpat enim, non sollicitudin purus dignissim id. Nam sit amet urna eu velit lacinia eleifend. Proin auctor rhoncus ligula nec aliquet. Donec sodales molestie lacinia. Curabitur dictum faucibus urna at convallis. Aliquam in lectus at urna rutrum porta. In lacus arcu, molestie ut vestibulum ut, rhoncus sed eros. Sed et elit vitae risus pretium consectetur vel in mi. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Morbi tempus turpis quis lectus rhoncus adipiscing. Proin pulvinar placerat suscipit. Maecenas imperdiet, quam vitae varius auctor, enim mauris vulputate sapien, nec laoreet neque diam non quam.

<!-- more -->

![Wallbase - dgnfly (wallbase.cc/wallpaper/1384450)](http://ww1.sinaimg.cn/large/81b78497jw1emfgts2pt4j21hc0u0k1c.jpg)

Etiam luctus mauris at mi sollicitudin quis malesuada nibh porttitor. Vestibulum non dapibus magna. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Proin feugiat hendrerit viverra. Phasellus sit amet nunc mauris, eu ultricies tellus. Sed a mi tortor, eleifend varius erat. Proin consectetur molestie tortor eu gravida. Cras placerat orci id arcu tristique ut rutrum justo pulvinar. Maecenas lacinia fringilla diam non bibendum. Aenean vel viverra turpis. Integer ut leo nisi. Pellentesque vehicula quam ut sapien convallis consequat. Aliquam ut arcu purus, eget tempor purus. Integer eu tellus quis erat tristique gravida eu vel lorem.

</br>

</br>

---

</br>

</br>

```yaml
title: Elements
date: 2013-12-24 23:29:08
categories:
- tutorial
tags:
```

# 5. elements

The purpose of this post is to help you make sure all of HTML elements can display properly. If you use CSS reset, don't forget to redefine the style by yourself.

Heading 1 (index 때문에 생략. #Heading 1)

## Heading 2

### Heading 3

#### Heading 4

##### Heading 5

###### Heading 6

---

## Paragraph

Lorem ipsum dolor sit amet, [test link]() consectetur adipiscing elit. **Strong text** pellentesque ligula commodo viverra vehicula. *Italic text* at ullamcorper enim. Morbi a euismod nibh. <u>Underline text</u> non elit nisl. ~~Deleted text~~ tristique, sem id condimentum tempus, metus lectus venenatis mauris, sit amet semper lorem felis a eros. Fusce egestas nibh at sagittis auctor. Sed ultricies ac arcu quis molestie. Donec dapibus nunc in nibh egestas, vitae volutpat sem iaculis. Curabitur sem tellus, elementum nec quam id, fermentum laoreet mi. Ut mollis ullamcorper turpis, vitae facilisis velit ultricies sit amet. Etiam laoreet dui odio, id tempus justo tincidunt id. Phasellus scelerisque nunc sed nunc ultricies accumsan.

Interdum et malesuada fames ac ante ipsum primis in faucibus. `Sed erat diam`, blandit eget felis aliquam, rhoncus varius urna. Donec tellus sapien, sodales eget ante vitae, feugiat ullamcorper urna. Praesent auctor dui vitae dapibus eleifend. Proin viverra mollis neque, ut ullamcorper elit posuere eget.

> Praesent diam elit, interdum ut pulvinar placerat, imperdiet at magna.

Maecenas ornare arcu at mi suscipit, non molestie tortor ultrices. Aenean convallis, diam et congue ultricies, erat magna tincidunt orci, pulvinar posuere mi sapien ac magna. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia Curae; Praesent vitae placerat mauris. Nullam laoreet ante posuere tortor blandit auctor. Sed id ligula volutpat leo consequat placerat. Mauris fermentum dolor sed augue malesuada sollicitudin. Vivamus ultrices nunc felis, quis viverra orci eleifend ut. Donec et quam id urna cursus posuere. Donec elementum scelerisque laoreet.

## List Types

### Definition List (dl)

<dl><dt>Definition List Title</dt><dd>This is a definition list division.</dd></dl>

### Ordered List (ol)

1. List Item 1
2. List Item 2
3. List Item 3

### Unordered List (ul)

- List Item 1
- List Item 2
- List Item 3

## Table

| Table Header 1 | Table Header 2 | Table Header 3 |
| -------------- | -------------- | -------------- |
| Division 1     | Division 2     | Division 3     |
| Division 1     | Division 2     | Division 3     |
| Division 1     | Division 2     | Division 3     |

## Misc Stuff - abbr, acronym, sub, sup, etc.

Lorem <sup>superscript</sup> dolor <sub>subscript</sub> amet, consectetuer adipiscing elit. Nullam dignissim convallis est. Quisque aliquam. <cite>cite</cite>. Nunc iaculis suscipit dui. Nam sit amet sem. Aliquam libero nisi, imperdiet at, tincidunt nec, gravida vehicula, nisl. Praesent mattis, massa quis luctus fermentum, turpis mi volutpat justo, eu volutpat enim diam eget metus. Maecenas ornare tortor. Donec sed tellus eget sapien fringilla nonummy. <acronym title="National Basketball Association">NBA</acronym> Mauris a ante. Suspendisse quam sem, consequat at, commodo vitae, feugiat in, nunc. Morbi imperdiet augue quis tellus.  <abbr title="Avenue">AVE</abbr>

</br>

</br>

---

</br>

</br>

```yaml
title: Link Post
date: 2013-12-24 23:30:04
link: http://www.google.com/
categories:
- tutorial
```

# 6. Link Post 

This is a link post. Clicking on the link should open [Google](http://www.google.com/) in a new tab or window.

</br>

</br>

---

</br>

</br>

```yaml
title: Images
date: 2013-12-26 22:46:49
categories:
- tutorial
```

# 7. Images

This is a image test post.

![](http://ww1.sinaimg.cn/mw690/81b78497jw1emfgwkasznj21hc0u0qb7.jpg)

![Caption](http://ww3.sinaimg.cn/mw690/81b78497jw1emfgwjrh2pj21hc0u01g3.jpg)

![](http://ww2.sinaimg.cn/mw690/81b78497jw1emfgwil5xkj21hc0u0tpm.jpg)

![Small Picture](http://placehold.it/350x150.jpg)

</br>

</br>

---

</br>

</br>

```yaml
layout: post
title: "MathJax with Jekyll"
date: 2014-02-16
categories: tutorial
image: http://gastonsanchez.com/images/blog/mathjax_logo.png
```

# 8. Mathjax with jekyll

One of the rewards of switching my website to [Jekyll](http://jekyllrb.com/) is the
ability to support **MathJax**, which means I can write LaTeX-like equations that get
nicely displayed in a web browser, like this one \\( \sqrt{\frac{n!}{k!(n-k)!}} \\) or
this one \\( x^2 + y^2 = r^2 \\).

<!--more-->

<img class="centered" src="https://www.mathjax.org/badge/mj-logo.svg" />

### What's MathJax?

If you check MathJax website [(www.mathjax.org)](http://www.mathjax.org/) you'll see
that it *is an open source JavaScript display engine for mathematics that works in all
browsers*.


### How to implement MathJax with Jekyll

I followed the instructions described by Dason Kurkiewicz for
[using Jekyll and Mathjax](http://dasonk.github.io/blog/2012/10/09/Using-Jekyll-and-Mathjax/).

Here are some important details. I had to modify the Ruby library for Markdown in
my ```_config.yml``` file. Now I'm using redcarpet so the corresponding line in the
configuration file is: ```markdown: redcarpet```

To load the MathJax javascript, I added the following lines in my layout ```post.html```
(located in my folder ```_layouts```)

{% highlight r %}

<script type="text/javascript"
    src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>

{% endhighlight %}

Of course you can choose a different file location in your jekyll layouts. 

Note that by default, the **tex2jax** preprocessor defines the
LaTeX math delimiters, which are ```\\(...\\)``` for in-line math, and ```\\[...\\]``` for
displayed equations. It also defines the TeX delimiters ```$$...$$``` for displayed
equations, but it does not define ```$...$``` as in-line math delimiters. To enable in-line math delimiter with ```$...$```, please use the following configuration:

{% highlight r %}

<script type="text/x-mathjax-config">
MathJax.Hub.Config({
  tex2jax: {
    inlineMath: [['$','$'], ['\\(','\\)']],
    processEscapes: true
  }
});
</script>
<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

{% endhighlight %}


### A Couple of Examples

Here's a short list of examples. To know more about the details behind MathJax, you can
always checked the provided documentation available at
[http://docs.mathjax.org/en/latest/](http://docs.mathjax.org/en/latest/)

Let's try a first example. Here's a dummy equation:

$$a^2 + b^2 = c^2$$

How do you write such expression? Very simple: using **double dollar** signs

{% highlight r %}
$$a^2 + b^2 = c^2$$
{% endhighlight %}

To display inline math use ```\\( ... \\)``` like this ```\\( sin(x^2) \\)``` which gets
rendered as \\( sin(x^2) \\)


Here's another example using type ```\mathsf```

{% highlight r %}
$$ \mathsf{Data = PCs} \times \mathsf{Loadings} $$
{% endhighlight %}

which gets displayed as

$$ \mathsf{Data = PCs} \times \mathsf{Loadings} $$

Or even better:

{% highlight r %}
\\[ \mathbf{X} = \mathbf{Z} \mathbf{P^\mathsf{T}} \\]
{% endhighlight %}

is displayed as

\\[ \mathbf{X} = \mathbf{Z} \mathbf{P^\mathsf{T}} \\]

If you want to use subscripts like this \\( \mathbf{X}\_{n,p} \\) you need to scape the
underscores with a backslash like so ``` \mathbf{X}\_{n,p} ```:

{% highlight r %}
$$ \mathbf{X}\_{n,p} = \mathbf{A}\_{n,k} \mathbf{B}\_{k,p} $$
{% endhighlight %}

will be displayed as

\\[ \mathbf{X}\_{n,p} = \mathbf{A}\_{n,k} \mathbf{B}\_{k,p} \\]