## Bonus: Explaining @IBOutlets

<p align="center"> <img src="/assets/tableview/P5/screenshot_bonus1.png" height="100px" align="center"> </p>

Xcode gives us some strange boilerplate when we create a storyboard connection. What do all of these keywords mean?

### @IBOutlet
This key word doesn't add any behavior to the code, and it would actually work fine without it. It's just an annotation for Xcode to give some added behavior to that line of code.

<p align="center"> <img src="/assets/tableview/P5/screenshot_bonus2.png" height="100px" align="center"> </p>

If you notice on the left of the line numbers (which you may or may not have enabled) there's a little dot. Mousing over it reveals which object in the Storyboard file is plugged up to that IBOutlet.

<p align="center"> <img src="/assets/tableview/P5/screenshot_bonus3.png" height="85" align="center"> </p>

If you take out `@IBOutlet` from the line, this functionality goes away. Useful, but not entirely necessary.

### weak

Now this is honestly some heavy stuff. This is a side effect of the way Objective-C works, and we're stuck with it considering Swift runs in the Objective-C runtime.

There's a whole concept called Object Retention that we don't have to worry about in Swift. An object must be `retained` by another object or it will just evaporate from existence. This basically means one object is claiming ownership over another in a **strong** reference.

To properly allocate and deallocate memory, references must be counted. When there are no longer any objects that reference a given object, then that object is deallocated. This used to be entirely up to the programmer before Apple introduced Automatic Reference Counting to Objective-C in 2011.

A **weak** reference tells the ARC system to *not* assume ownership of the object. This means that the ViewController isn't the object retaining the variable. That's handled somewhere in the mysterious inner workings of UIKit.

This prevents issues like retain cycles, which is when two objects `retain` each other. This creates a situation where neither will ever be deallocated.

**tl;dr** `weak` prevents weird stuff from happening because of the way Objective-C works.

### var and !
`var` and  `!` exist for the same reason, because of the life cycle of a UIView:

1. Allocate memory for the object.
2. Instantiate the object. At this point, all IBOutlets are **nil**.
3. Instantiate the subviews based on the Storyboard file and connect the references.

`!` is necessary because the variable starts as nil. It *could* be an `?` instead, but that adds all of the boilerplate of dealing with Optionals. `!` denotes an implicitly unwrapped optional. This means that, yes, it is possible for the object to be nil, but we are *assuming* that it is not nil, so we can treat it like a regular non-optional type. This works well because the reference is immediately set to an actual value. This just happens too late in the life cycle for a standard non-optional type to work 100% of the time.

`var` is necessary because we change the variable from nil to whatever it's supposed to be. If we used a `let`, then the variable would be immutable and could not change from nil at the appropriate point in the lifecycle, which is definitely not what we want.

Click here for <a href="#top" onclick="setTableViewTutorial(6)">Part 6</a>
