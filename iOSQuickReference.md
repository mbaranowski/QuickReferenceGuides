# Objective-C

## References

## Test Changes

Making a lot of changes to test git rebase -i.

[The Objective-C Programming Language]() 

## Class Declaration

in header file MyClass.h

```
// class inherits from NSObject, implements SomeProtocol
@interface MyClass : NSObject <SomeProtocol>
{
	id			data;                // id used for weak typing
	NSString*	name;                // strong typing, uses pointers
	BOOL		isHidden;
	int			value;
	float		count;
}

// accessors, can be accessed with myClassInstance.value = 5
-(int)value;
-(void)setValue:(int)newValue;

// special case for bool, used as ‘instance.isHidden = TRUE’
-(BOOL)isHidden;
-(void)setHidden:(BOOL)newHidden;

// property declaration, shortcut for writing out accessors
@property float count;

// property attributes:
//         copy, readonly, strong, weak, assign, retain, nonatomic
@property (copy) NSString* name;

// instance method 
// called with [instance initWithString:@”string”]
- (id)initWithString:(NSString*)aName;

// cass method,
// called with [MyClass createMyClassWithString:@”string”]
+ (MyClass*)createMyClassWithString:(NSString*)aName;


@end
```


## Class implementation

(Changes all over the place!)
in source file MyClass.m


```
@implementation MyClass

// generates methods -(int)count; and -(void)setCount:(int)v
@synthesize count;
@synthesize name;

// implement accessors
-(int)value { return value; }
-(void)setValue:(int)newValue { value = newValue; -(BOOL)isHidden { return isHidden; }
-(void)setHidden:(BOOL)newHidden { isHidden = newHidden; }

-(id)initWithString:(NSString*)aName
{
        self = [super init];
        if (self) {
                name = [aName copy];
        }
        return self;
}

+ (MyClass*)createMyClassWithString:(NSString*)aName
{
        return [[[self alloc] initWithString:aName] autorelease];
}

@end
```

## []() [Property attributes]() 


**getter=getterName**- Specifies the name of the get accessor for the property.

**setter=setterName** - Specifies the name of the set accessor for the property.

**readwrite** - Indicates that the property should be treated as read/write. Default.

**readonly** - Indicates that the property is read-only.

**strong** - Specifies that there is a strong (owning) relationship to the destination object.

**weak** - Specifies that there is a weak (non-owning) relationship to the destination object.

**copy** - Specifies that a copy of the object should be used for assignment. The previous value is sent a [release](https://developer.apple.com/library/ios/documentation/Cocoa/Reference/Foundation/Protocols/NSObject_Protocol/Reference/NSObject.html#//apple_ref/occ/intfm/NSObject/release)  message. The copy is made by invoking the [copy](https://developer.apple.com/library/ios/documentation/Cocoa/Reference/Foundation/Classes/NSObject_Class/Reference/Reference.html#//apple_ref/occ/instm/NSObject/copy) method. This attribute is valid only for object types, which must implement the NSCopying  protocol.

**assign** -Specifies that the setter uses simple assignment. Default. You use this attribute for scalar types such as NSInteger and CGRect.

**retain** - Specifies that[ ](https://developer.apple.com/library/ios/documentation/Cocoa/Reference/Foundation/Protocols/NSObject_Protocol/Reference/NSObject.html#//apple_ref/occ/intfm/NSObject/retain) [retain](https://developer.apple.com/library/ios/documentation/Cocoa/Reference/Foundation/Protocols/NSObject_Protocol/Reference/NSObject.html#//apple_ref/occ/intfm/NSObject/retain)  should be invoked on the object upon assignment. The previous value is sent a[ ](https://developer.apple.com/library/ios/documentation/Cocoa/Reference/Foundation/Protocols/NSObject_Protocol/Reference/NSObject.html#//apple_ref/occ/intfm/NSObject/release) [release](https://developer.apple.com/library/ios/documentation/Cocoa/Reference/Foundation/Protocols/NSObject_Protocol/Reference/NSObject.html#//apple_ref/occ/intfm/NSObject/release)  message.

**nonatomic** - Specifies that accessors are nonatomic. By default, accessors are atomic.

## []() [Strings](https://developer.apple.com/library/mac/#documentation/Cocoa/Reference/Foundation/Classes/NSString_Class/Reference/NSString.html) 


NSString is an immuatable string of unicode characters:

```
// literal NSString startsw with @
NSString *myString = @"My String\n";

// useful string operations
NSString *anotherString = [NSString[stringWithFormat](https://developer.apple.com/library/mac/#documentation/Cocoa/Reference/Foundation/Classes/NSString_Class/Reference/NSString.html) :@"%d %@", 1, @"String"];

NSString *fromCString = [NSString stringWithCString:"A C string" encoding:NSASCIIStringEncoding];
```

## []() Arrays

[NSArray]()  is an immutable array. Objects stored using a weakly typed handle, id. Details about new [objective-c literal syntax in Xcode 4.4](http://clang.llvm.org/docs/ObjectiveCLiterals.html).

```
NSArray* array = [NSArray arrayWithObjects:@”one”, @”two”];
if ([array count] > 0)
	NSLog(@”first object %@”, [array objectAtIndex:0]);

// new objective-c literal syntax in Xcode 4.4 
NSArray* array = @[ @”one”, @”two”, @”three” ];

// works if building for iOS6
NSLog(@”first object %@”, array[0]);
```

Sorting an array:

```
NSArray *sortedArray = [array sortedArrayUsingSelector:@selector(compareFunc:)];
```

[NSMutableArray](http://developer.apple.com/library/ios/#DOCUMENTATION/Cocoa/Reference/Foundation/Classes/NSMutableArray_Class/Reference/Reference.html) , mutable, can append,

```
NSMutableArray* array = [NSMutableArray arrayWithCapacity: 10];
[array addObject:@”one”];
[array removeLastObject];
[array insertObject:@”two” atIndex:0];
[array removeObjectAtIndex:0];
```

Iterating:

```
for (NSString* str in array) {
        NSLog(str);
}
```

Saving

```
[array writeToFile:filePath atomically:YES];
```

## Dictionaries


## Protocols

```
@protocol MyProtocol
// method declarations
- (void)myProtocolMethod;
@end
```

## [Key Value Coding]() 


Key-value coding is a mechanism for accessing an object’s properties indirectly, using strings to identify properties. Implementing key-value coding compliant accessors allows integration with CoreData, Cocoa bindings, and scripting.

**valueForKey:** - returns the value for the specified key, relative to the receiver. If there is no accessor or instance variable for the specified key, then the receiver sends itself a valueForUndefinedKey: message. The default implementation of valueForUndefinedKey: raises an[ ](https://developer.apple.com/library/ios/documentation/Cocoa/Reference/Foundation/Protocols/NSKeyValueCoding_Protocol/Reference/Reference.html#//apple_ref/doc/c_ref/NSUndefinedKeyException) [NSUndefinedKeyException](https://developer.apple.com/library/ios/documentation/Cocoa/Reference/Foundation/Protocols/NSKeyValueCoding_Protocol/Reference/Reference.html#//apple_ref/doc/c_ref/NSUndefinedKeyException) ; subclasses can override this behavior.

**valueForKeyPath:** returns the value for the specified key path, relative to the receiver. Any object in the key path sequence that is not key-value coding compliant for the appropriate key receives a valueForUndefinedKey: message.

**dictionaryWithValuesForKeys:** retrieves the values for an array of keys relative to the receiver. The returned NSDictionary contains values for all the keys in the array.

## Automatic Reference Counting (ARC)

  * Do not call retain/release/autorelease (do not implement these)
  * No Object pointers in C-Structs. Use Objective-C classes
  * No casting between id and void*
  * Do not use NSAutorelease pool. Use @autorelease { } instead.

## Singletons

```
+ (SingletonClass *)sharedInstance
{
    static dispatch_once_t pred;
    static SingletonClass *sharedInstance = nil;
    
    dispatch_once(&pred, ^{
        sharedInstance = [[SingletonClass alloc] init];
        // .. any initialization
    });
    
    return sharedInstance;
}
```
## private methods

Idiom to implement private methods for SomeClass, in SomeClass.m

```
@interface SomeClass (PrivateMethods) <SomeDelegate>
- (void)someDelegateMethod:(id)param;
@end
```
# iOS SDK

## References

[iOS App Programming Guide]() 

## CocoaTouch



### Main function

```
objective-c

int main(int argc, char *argv[])
{
   @autoreleasepool {
   	 // creates a UIApplication object and connects it to UIApplicationDelegate implementations
   	 // calls applicationdidFinishLaunchingWithOptions on the delegate
   	 // (after main nib or storyboard has been loaded, if used)
     return UIApplicationMain(argc, argv, nil, @”AppDelegate”);
   }
}
```

### [UIApplicationDelegate](http://developer.apple.com/library/ios/#DOCUMENTATION/UIKit/Reference/UIApplicationDelegate_Protocol/Reference/Reference.	html) implementation

A delegate used by UIApplication, used to configure how the app responds to 

In AppDelegate.h

```
@interface AppDelegate : UIResponder <UIApplicationDelegate>
{
    UIWindow* window;
    MainViewController* mainViewController;
}
@property (strong, nonatomic) UIWindow *window;
@property (strong, nonatomic) MainViewController * mainViewController;
@end
```

In AppDelegate.m

```
@synthesize window;
@synthesize mainViewController;

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
	window = [[UIWindow alloc] initWithFrame:[[UIScreen mainScreen] bounds]];
	mainViewController = [[MainViewController alloc] init];
		
	[window addSubview:mainViewController.view];
	[window makeKeyAndVisible];
	return YES;
}

```


### UIViewController References

  * [View Controller Programming Guide for iOS](http://developer.apple.com/library/ios/#featuredarticles/ViewControllerPGforiPhoneOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40007457)
  * [View Controller Catalog for iOS](http://developer.apple.com/library/ios/#documentation/WindowsViews/Conceptual/ViewControllerCatalog/Introduction.html#//apple_ref/doc/uid/TP40011313)

  * loadView - override to programatically initialize a view

```
- (void)loadView {
	self.view = [[UIView alloc] initWithFrame:[[UIScreen mainScreen] bounds]];
```


---
### [UITableViewController](http://developer.apple.com/library/ios/#documentation/uikit/reference/UITableViewController_Class/Reference/Reference.html#//apple_ref/occ/cl/UITableViewController)

Used to display and edit a list of information grouped into sections and displayed as cells ([UITableViewCells](http://developer.apple.com/library/ios/#documentation/uikit/reference/UITableViewCell_Class/Reference/Reference.html#//apple_ref/occ/cl/UITableViewCell)).

implements [UITableViewDataSource](http://developer.apple.com/library/ios/#documentation/uikit/reference/UITableViewDataSource_Protocol/Reference/Reference.html#//apple_ref/occ/intf/UITableViewDataSource) to provie information about the table sections and cells.

* numberOfSectionsInTableView
* tableView:numberOfRowsInSection:
* tableView:cellForRowAtIndexPath:

implements [UITableViewDelegate](http://developer.apple.com/library/ios/#documentation/uikit/reference/UITableViewDelegate_Protocol/Reference/Reference.html#//apple_ref/occ/intf/UITableViewDelegate) to recieve cell selection, tap notification as well as to configure appearance and editing behavior.

  * tableView:accessoryButtonTappedForRowWithIndexPath:
  * tableView:didSelectRowAtIndexPath:
---

### [UINavigationController](http://developer.apple.com/library/ios/#documentation/UIKit/Reference/UINavigationController_Class/Reference/Reference.html#//apple_ref/occ/cl/UINavigationController)

Acts like a stack of View controllers that are useful to navigate a hierarchy of content. 

To create: 

```
- (void)applicationDidFinishLaunching:(UIApplication *)application
{
	// create custom controller visible inside the UINavigationController, for example a UITableViewController
    UIViewController *myViewController = [[MyViewController alloc] init];
    navigationController = [[UINavigationController alloc] initWithRootViewController:myViewController];
    window = [[UIWindow alloc] initWithFrame:[[UIScreen mainScreen] bounds]];
    window.rootViewController = navigationController;
    [window makeKeyAndVisible];
}
```

To controls and navigate:

  * [pushViewController:animated:](http://developer.apple.com/library/ios/#documentation/UIKit/Reference/UINavigationController_Class/Reference/Reference.html#//apple_ref/occ/instm/UINavigationController/pushViewController:animated:) - Pushes a view controller onto the receiver’s stack and updates the display
  * [popViewControllerAnimated:](http://developer.apple.com/library/ios/#documentation/UIKit/Reference/UINavigationController_Class/Reference/Reference.html#//apple_ref/occ/instm/UINavigationController/popViewControllerAnimated:) - Pops the top view controller from the navigation stack and updates the display. Usually handled by the Back button.
  * [setViewControllers:animated:](http://developer.apple.com/library/ios/#documentation/UIKit/Reference/UINavigationController_Class/Reference/Reference.html#//apple_ref/occ/instm/UINavigationController/setViewControllers:animated:) Replaces the view controllers currently managed by the navigation controller with the specified items. Used to restore navigation state to a saved one.

Components to modify:

  * navigationBar - [UINavigationBar](http://developer.apple.com/library/ios/#documentation/UIKit/Reference/UINavigationBar_Class/Reference/UINavigationBar.html#//apple_ref/doc/c_ref/UINavigationBar)  on top of screen holds navigation buttons and title.
    * backBarButtonItem 
    * leftBarButtonItem
    * titleView
    * rightBarButtonItem
  * toolbar - UIToolbar, 

---
  
### UITabBarController
### UISplitViewController 
### UIPopoverController
### Nibless Controls

For UIButton

```
    CGSize  size = [title sizeWithFont:font];
    UIButton* button = [[UIButton alloc] initWithFrame:CGRectMake(0,0,size.width+24, size.height+16)];
    button.titleLabel.font = font;
    [button setTitleColor:[UIColor greenColor] forState:UIControlStateHighlighted];
    [button setTitleColor:[UIColor whiteColor] forState:UIControlStateNormal];     
    [button setTitle:title forState:UIControlStateNormal];
    [button addTarget:self
               action:@selector(eventHandlerMethod:)
     forControlEvents:UIControlEventTouchUpInside];
    [self.view addSubview:button];
```

For UILabel

```
    CGSize  size = [title sizeWithFont:font];
    label = [[UILabel alloc] initWithFrame:CGRectMake(0, 0, size.width, size.height)];
    label.backgroundColor = [UIColor clearColor];
    label.textAlignment = UITextAlignmentCenter;
    label.font = logoFont;
    label.textColor = [UIColor whiteColor];
    label.text = title;
    label.center = CGPointMake(frame.size.height/2, frame.size.height/2);
    [self.view addSubview:label];
```


## CoreData
### Reference

  * [Open GL Guide](http://developer.apple.com/library/ios/#documentation/3DDrawing/Conceptual/OpenGLES_ProgrammingGuide/Introduction/Introduction.html)

### CoreGraphics

```
    UIGraphicsBeginImageContext(size);
    CGContextRef context = UIGraphicsGetCurrentContext();
    
    // use CGContext commands to draw stuff, ex. draw a circle
    CGContextSetRGBFillColor(context, 1.0f, 1.0f, 1.0f, 1.0f);
    CGContextFillEllipseInRect(context, CGRectMake(0,0,size.width,size.height));
    
    UIImage *image = UIGraphicsGetImageFromCurrentImageContext();
    UIGraphicsEndImageContext();
``` 

## OpenGL

## Game Center



## Tools

 * [cocoapods.org](http://cocoapods.org/)  - manages library dependencies for objective-c projects
 * [Nimbus](http://docs.nimbuskit.info/index.html)
 * [AFNetworking](https://github.com/AFNetworking/AFNetworking)

http://www.reddit.com/r/iosprogramming
http://www.reddit.com/r/iphonedev

## Another Section Header

section text goes here
