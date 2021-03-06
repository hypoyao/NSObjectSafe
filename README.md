# NSObject-Safe


### Desciption
* Swizzle commonly used function of Foundation container to prevent nil crash
* Assert in Debug and log in Release

### Usage:
	
* involve NSObjectSafe.h/NSObjectSafe.m as build phases

### Warn: 
* NSObjectSafe must used in MRC, otherwise it will cause strange release error: [UIKeyboardLayoutStar release]: message sent to deallocated instance

### Object Literals

```
NSArray* item = nil;
NSArray * items = @[@"a",@"b", item ,@"c"];
NSLog(@"%@", items);

NSString* key = nil;
NSString* value = nil;
NSLog(@"%@", @{@"b":@"c",key:value, @"e":value});
```

### Swizzle Functions:

* NSObject(Swizzle):

```
+ (void)swizzleClassMethod:(SEL)origSelector withMethod:(SEL)newSelector;
- (void)swizzleInstanceMethod:(SEL)origSelector withMethod:(SEL)newSelector;
```
* NSObject(Safe)

```
- (void) addObserver:(NSObject *)observer forKeyPath:(NSString *)keyPath 
						options:(NSKeyValueObservingOptions)options context:(void *)context;
- (void) removeObserver:(NSObject *)observer forKeyPath:(NSString *)keyPath;
```
* NSString

```
+ (NSString*) stringWithUTF8String:(const char *)nullTerminatedCString;
+ (nullable instancetype) stringWithCString:(const char *)cString encoding:(NSStringEncoding)enc;
- (nullable instancetype) initWithCString:(const char *)nullTerminatedCString encoding:(NSStringEncoding)encoding;
- (NSString *)stringByAppendingString:(NSString *)aString;
```

* NSMutableString

```
- (nullable instancetype) safeInitWithCString:(const char *)nullTerminatedCString encoding:(NSStringEncoding)encoding;
- (void) appendString:(NSString *)aString;
- (void) insertString:(NSString *)aString atIndex:(NSUInteger)loc;
- (void) deleteCharactersInRange:(NSRange)range;
- (NSString *)stringByAppendingString:(NSString *)aString;
```

* NSArray

```
+ (instancetype) arrayWithObject:(id)anObject;
- (id) objectAtIndex:(NSUInteger)index;
```

* NSMutableArray

```
- (void) addObject:(id)anObject;
- (id) objectAtIndex:(NSUInteger)index;
- (void) insertObject:(id)anObject atIndex:(NSUInteger)index;
- (void) removeObjectAtIndex:(NSUInteger)index;
- (void) replaceObjectAtIndex:(NSUInteger)index withObject:(id)anObject;
- (void) removeObjectsInRange:(NSRange)range;
```

* NSDictionary

```
+ (instancetype) dictionaryWithObject:(id)object forKey:(id)key;
- (id) objectForKey:(id)aKey;
```

* NSMutableDictionary

```
- (id) objectForKey:(id)aKey;
- (void) setObject:(id)anObject forKey:(id)aKey;
- (void) removeObjectForKey:(id)aKey;
```
* NSSet

```
+ (instancetype)setWithObject:(id)object;
```
* NSMutableSet

```
- (void) addObject:(id)object;
- (void) removeObject:(id)object;
```
* NSOrderedSet

```
+ (instancetype)orderedSetWithObject:(id)object;
- (instancetype)initWithObject:(id)object;
- (id)objectAtIndex:(NSUInteger)idx;
```

* NSMutableOrderedSet

```
- (id)objectAtIndex:(NSUInteger)idx;
- (void)addObject:(id)object;
- (void)insertObject:(id)object atIndex:(NSUInteger)idx;
- (void)removeObjectAtIndex:(NSUInteger)idx;
- (void)replaceObjectAtIndex:(NSUInteger)idx withObject:(id)object;
```
* NSUserDefault

```
- (id) objectForKey:(NSString *)defaultName;
- (NSInteger) integerForKey:(NSString *)defaultName;
- (BOOL) boolForKey:(NSString *)defaultName;
- (void) setObject:(id)value forKey:(NSString*)aKey;
- (void) removeObjectForKey:(NSString*)aKey;
```











