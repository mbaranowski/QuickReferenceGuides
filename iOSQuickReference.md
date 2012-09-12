

# Objective-C

## References


[The Objective-C Programming Language]() 

## Class Declaration

in header file MyClass.h

```
// class inherits from NSObject, implements SomeProtocol
@interface MyClass : NSObject <SomeProtocol>
{
	id			data;                // id used for weak typing
	NSString*	name;                // strong typing, uses pointers
	BOOL        isHidden;
	int                 value;
	float                count;
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

[NSArray]()  is an immutable array. Objects stored using a weakly typed handle, id.

```
NSArray* array = [NSArray arrayWithObjects:@”one”, @”two”];
if ([array count] > 0)
	NSLog(@”first object %@”, [array objectAtIndex:0]);

// new[objective-c literal syntax in Xcode 4.4](http://clang.llvm.org/docs/ObjectiveCLiterals.html) 
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

### UIViewController subclass


## CoreData

## OpenGL

## Tools

 * [http://cocoapods.org](http://cocoapods.org/)  - manages library dependencies for objective-c projects

