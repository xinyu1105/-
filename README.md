1. 字典转模型
========================================
1.1 字典转模型的好处：
1> 降低代码的耦合度
2> 所有字典转模型部分的代码统一集中在一处处理，降低代码出错的几率
3> 在程序中直接使用模型的属性操作，提高编码效率

模型应该提供一个可以传入字典参数的构造方法
- (instancetype)initWithDict:(NSDictionary *)dict;
+ (instancetype)xxxWithDict:(NSDictionary *)dict;

1.2 instancetype & id
1> instancetype在类型表示上，跟id一样，可以表示任何对象类型
2> instancetype只能用在返回值类型上，不能像id一样用在参数类型上
3> instancetype比id多一个好处：编译器会检测instancetype的真实类型

1.3 在模型中添加readonly属性
// 定义属性时，会生成getter&setter方法，还会生成一个带下划线的成员变量
// 而如果是readonly属性，则只会生成getter方法，同时没有成员变量
@property (nonatomic, strong, readonly) UIImage *tapImage;

@interface AppListModel()
{
    UIImage *_tapImage;
}
- (UIImage *)tapImage
{
    if (!_tapImage) {
        _tapImage = [UIImage imageNamed:self.icon];
    }
    return _tapImage;
}
在模型中合理地使用只读属性，可以进一步降低代码的耦合度。

1.4 使用数据模型的好处：
*** 调用方不用关心模型内部的任何处理细节！
