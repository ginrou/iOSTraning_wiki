1st
# 導入

### object 生成
`NSObject *obj = [[NSObject alloc] init];`
### method
`[obj exeWithArg1:hoge arg2:fuga]`

Objective C にはメッソドにラベルがある。
### クラスの作成
MixiSampleClass.h, m を作成。

MixiSampleClass.h
```objective-c
#import <Foundation/Foundation.h>

@interface MixiSampleClass : NSObject

@property (nonatomic, strong) NSString *name;

-(id)initWithName:(NSString *)name;
+(NSString *) getClassName;

@end
```

MixiSampleClass.m
```objective-c
#import "MixiSampleClass.h"

@implementation MixiSampleClass

-(id)initWithName:(NSString *)name
{
    self = [super init];
    if(self){
        _name = name;
    }
    return self;
}

+ (NSString *)getClassName
{
    return @"MixiSampleClass";
}
@end
```