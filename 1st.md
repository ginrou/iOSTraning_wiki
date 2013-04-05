1st 導入
# Objecticve-C の基本

[Objective-C プログラミング](https://developer.apple.com/jp/devcenter/ios/library/documentation/ObjC.pdf)
## object 生成
`NSObject *obj = [[NSObject alloc] init];`
## method
`[obj exeWithArg1:hoge arg2:fuga]`

Objective C にはメッソドにラベルがある。
## クラスの作成
MixiSampleClass.h, m を作成。

MixiSampleClass.h
```objective-c
#import <Foundation/Foundation.h>

@interface MixiSampleClass : NSObject

@property (nonatomic, strong) NSString *name; /// [1] property

-(id)initWithName:(NSString *)name; /// [2] instance method
+(NSString *) getClassName; /// [3] class method

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
        _name = name; /// [4]　access to ivar
    }
    return self;
}

+ (NSString *)getClassName
{
    return @"MixiSampleClass";
}
@end
```
### [1] property 宣言
- name というインスタンス変数を持っている（自動的に生成）
- nonatmic : 排他制御
- strong : オーナーシップをもっている
- -setName, -getName という getter, setter を自動的に生成。（getter=hoge, setter=fuga）と明示的に命名することも可能

### [2] instance method
インスタンスメソッドには - をつけて宣言

### [3] class method
クラスメソッドには + をつけて宣言

### [4] access to ivar
- 自クラス内のインスタンス変数を参照、代入するときは _name = hoge, fuga = _name (self.name も可)
- 他クラスのインスタンス変数の場合は obj.name

