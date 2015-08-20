---
layout: post
title: "You're up and running!"
published: true
---


Next you can update your site name, avatar and other options using the _config.yml file in the root of your repository (shown below).

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
