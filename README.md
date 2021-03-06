MotionCpp is a boilerplate Xcode project to create Objective-c wrappers arround C++ libraries, in order to use them with RubyMotion.


Today I learn that RubyMotion can't directly interact with C++ classes/objects.

Even tho BridgeSupport *can* parse c++ header files, only pure C types will be handled correctly.

At the end, it was made clear to me that the only solution is an Objective-c wrapper around those c++ libraries.

It might sound as a trivial task, since Obj-c is a superset of C just like c++. But as anything involving Xcode, it isn't.


Comments are written throughout the code to help you in the task of writing the wrapper.

Once you have our wrapper all setup, simply add it to the vendor directory of your RubyMotion project and add this line to your Rakefile:

```ruby
  app.vendor_project( "vendor/MotionCpp", :xcode,
    :xcodeproj => "MotionCpp.xcodeproj", :target => "MotionCpp", :products => ["libMotionCpp.a"],
    :headers_dir => "MotionCpp")
```

Now you can access your C++ code like this:

```ruby
@motionCpp = MotionCpp.alloc.init
@motionCpp.myWrapperMethod
```

NOTE: You might need to modify "C Language Dialect", "C++ Language Dialect" and "C++ Standard Library" configurations under Build Settings.