---
layout: post
title: "You're up and running!"
published: true
tags: 
  - uml
  - vernality
---


#Vernality
Vernality means early days or 'springtime' of some thing. That's really interesting to take part in the 'springtime' projects, to grow up something from the beginning. Since I've developed my own iOS apps I've faced a common issue: one man is no man. Design, marketing, user support - that really eats up tons of time and effort. 

>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor 
incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.


{% highlight swift %}
import Foundation

extension CALayer {
    var borderColorIB : UIColor {
        get {
            return UIColor(CGColor: self.borderColor)!
        }
        set {
            self.borderColor = newValue.CGColor
        }
    }
    
    var shadowColorIB : UIColor {
        get {
            return UIColor(CGColor: self.shadowColor)!
        }
        set {
            self.shadowColor = newValue.CGColor
        }
    }
}
{% endhighlight %}

![_config.yml]({{ site.baseurl }}/images/config.png)

The easiest way to make your first post is to edit this one. Go into /_posts/ and update the Hello World markdown file. For more instructions head over to the [Jekyll Now repository](https://github.com/barryclark/jekyll-now) on GitHub.
