# iOS学习：iOS代码规范

---

### 目录
- [作者感言](#作者感言)
- [阅读前言](#阅读前言)
- [iOS代码规范](#iOS代码规范)
	- [#Import规范](#Import规范)
	- [#Define规范](#Define规范)
	- [#Paragma Mark 规范](#Paragma Mark 规范)
	- [@Interface规范](@Interface规范)
	- [@implementation规范](@implementation规范)
	- [实例规范](实例规范)
	- [NSDictionary规范](NSDictionary规范)
	- [NSArray规范](NSArray规范)
	- [函数规范](函数规范)
	- [If-Else规范](If-Else规范)
	- [For-In & For 规范](For-In & For 规范)
	- [Block规范](Block规范)
	- [运算符规范](运算符规范)
- [命名规范](#命名规范)
	- [实例命名规范](实例命名规范)
	- [@Property命名规范](@Property命名规范)
	- [@Interface->class命名规范](@Interface->class命名规范)
	- [#Define命名规范](#Define命名规范)
	- [Block命名规范](Block命名规范)
	- [For-In命名规范](For-In命名规范)
- [布局框架](#布局框架)
- [文件夹层次结构](#文件夹层次结构)

# 作者感言

> 这篇文章, 部分是收集了网上的iOS开发爱好者的代码规范, 以及我自己的理解, 不一定完全满足所有人, 希望多多见谅, 也同样感谢支持我完成这篇文章的朋友.
>
> 刚开始写这篇文章的时候, 我无从下手, 直到我朋友给了我一份JAVA的开发文档规范, 我才慢慢有了清晰的思路, 中间迭代了许多版本, 一次次的修改文章的排版, 关键字的高亮, 以及代码的高亮.
>
> 一点点的编写, 一次次的修改, 让我对代码规范有了更深刻的理解, 曾经有人说过, 印度人写代码, 100个人所写的, 看起来像一个人所写的, 不是说印度阿三开挂了, 是他们遵循了一个规范, 无规矩不成方圆, 也就是这个道理.



> **最后:**
> **如果你有更好的建议或者对这篇文章有不满的地方, 请联系我, 我会参考你们的意见再进行修改, 联系我时, 请备注`iOS代码规范文档`, 祝大家学习愉快~谢谢~**

联系方式:

* **Cain(罗家辉)**


* **联系方式:** zhebushimengfei@qq.com


* **腾讯QQ:** 350116542

---
# 阅读前言

* 在阅读代码规范之前，必须先去下载两个插件<**[XAlign](https://github.com/qfish/XAlign)**, **[VVDocumenter](https://github.com/onevcat/VVDocumenter-Xcode)**>。
* 文档的目的是描述一些关于iOS编程的标准和惯例，并指导编写稳定的iOS代码。这些都是基于健全的、充分证明过的软件工程基础上的，并使得代码容易理解、维护和增。更重要的是，遵循这些规则，iOS开发人员的编程效率将会显著的得到提高。因为不必花费时间来重新编写代码，而是更容易的在开发过程中，对代码进行修改。最后，遵循这些规则，可以保持代码的连续性和粘性，提升开发组的效率。

---
# iOS代码规范



## #Import规范

1. 当一个**`Controller`**或者一个**`Class`**中需要用到不同的类和**`Define`**时, 我们应当把**`#import`**划分.

* **划分原则:** 哪个**`Controller`**或者**`Class`**是本**`Controller`**或者**`Class`**的次级就放在一起, 公共**`Controller`**或**`Class`**就与之前的空一行, 紧跟着下面.

比如:
```objective-c
#import "AspManageServicePasswordViewController.h"
#import "AspResetServicePasswordViewController.h"
#import "AspServicePasswordView.h"
	
#import "NorNavShareView.h"

#import "AppDelegate.h"
#import "BCTabBarView.h"

#import "ModifyPwdViewController.h"
#import "AspLoginVC.h"
```
---

## #Define规范

* 使用**`#define`**时, 必须要以数值对齐.

比如:
```objective-c
#define kLabelSize     20
#define kLabelMargins  20

#define kConfirmBottom 63
```

错误写法:
```objective-c
#define kLabelSize 20
#define kLabelMargins 20

#define kConfirmBottom 63
```
---

* 在代码中尽量减少在代码中直接使用数字敞亮, 而使用**`#define`**来进行声明常量或运算.

比如:
```objectivec
#define kTableViewHeight 	 300
#define kTableViewCellHeight label.height + view.height
```

错误写法:
```objectivec
- (void)viewDidLoad {
    [super viewDidLoad];
    
    self.tableView.frame = CGRectMake(0, 64, 320, 660);
}
```
* 尽量代码中得重复计算, 比如在代码中很多地方需要使用到屏幕的宽度, 然后再进行计算, 我们就可以把屏幕的宽度进行抽取封装成**`#define`**.

比如:
```objective-c
#define AspScreenWidth   ([[UIScreen mainScreen] bounds].size.width)
#define kTableViewHeight 300
#define NAV_VIEW_HEIGHT  64

- (void)viewDidLoad {
    [super viewDidLoad];
    
    self.tableView.frame = CGRectMake(0, NAV_VIEW_HEIGHT, AspScreenWidth, kTableViewHeight);
}
```
错误写法:
```objective-c
- (void)viewDidLoad {
    [super viewDidLoad];
    
    self.tableView.frame = CGRectMake(0, 64, 320, 660);
}
```
---
## #Paragma Mark 规范

* 使用**`#pragma mark`**时紧挨着方法名, 且与上一个方法的间距为1空行.

比如:
``` objective-c
- (void)mineViewModel {

	// Code Body
}

#pragma mark - TableViewRefresh
- (void)pulldownRefresh:(AspTableView *)tableView {
	    
	[self.mineViewModel requestDataWithSuccess:nil failure:nil];
}
```
错误写法:
``` objective-c
- (void)mineViewModel {

	// Code Body
}

#pragma mark - TableViewRefresh

- (void)pulldownRefresh:(AspTableView *)tableView {
	    
	[self.mineViewModel requestDataWithSuccess:nil failure:nil];
}
```
``` objective-c
- (void)mineViewModel {

	// Code Body
}

#pragma mark - TableViewRefresh
- (void)pulldownRefresh:(AspTableView *)tableView {
	    
	[self.mineViewModel requestDataWithSuccess:nil failure:nil];
}
```
---
* 当两个方法相近或者都是同一个模块里的方法, 使用**`#pragma mark`**加注释来导航代码.

比如:

``` objective-c
#pragma mark - Some Mothed
- (void)someMothedOne;
- (void)someMothedTwo;
- (void)someMothedThree;
```
错误写法:
``` objective-c
#pragma mark - 
- (void)someMothedOne;
- (void)someMothedTwo;
- (void)someMothedThree;
```
``` objective-c

- (void)someMothedOne;
- (void)someMothedTwo;
- (void)someMothedThree;
```
---
## @Interface规范

* 当**`@interface`**里声明了许多**`Delegate`**, **`DataSource`**, **`Protocol`**方法时, 我们需要在**`“Class Name()”`**及**`“,”`**后空一格, 且以第一个**`Delegate(DataSource或Protocol)`**方法名对齐, 建议在4~5个之后就换行.

比如:

```objective-c
interface AspEasyOwnResetPasswordViewController()<UITextFieldDelegate, MBAlertViewDelegate, UITableViewDelegate, UITableViewDataSource, 
UITextViewDelegate>
```


错误写法:
```objective-c
interface AspEasyOwnResetPasswordViewController()<UITextFieldDelegate,MBAlertViewDelegate>
```
---
* 当我们在**`@interface`**里声明变量时, 我们应该根据内存管理关键字来划分模块, 且以 **`“*”`** 分类对齐(基础数据类型除外).

比如:
```objective-c
@interface AspResetServicePasswordViewController () <UITextFieldDelegate, MBAlertViewDelegate>

@property (nonatomic, strong) AspRetrievePasswordView *retrievePassword;
@property (nonatomic, strong) UITextField             *foucsTextField;

@property (nonatomic, copy  ) NSString *brandName;
@property (nonatomic, copy  ) NSString *brandType;

@property (nonatomic, assign) NSTimer *timer;

@property (nonatomic, assign) NSInteger zeroCount;
@property (nonatomic, assign) NSInteger verificationCode;

@end
```
错误写法:
```objective-c
@property (nonatomic, strong) NSDictionary *everyDataDic;
@property (nonatomic, copy) NSString *timeStr;
@property (nonatomic, strong) UILabel *timeLabel;
@property (nonatomic, strong) UILabel *titleLabel;
@property (nonatomic, strong) SHLineGraphView *lineGraph;
```

---
* 在**`@interface`**里声明**`@property`**需要把**`nonatomic`**放在前**`(使用xib的除外)`**, **`strong`**等内存关键字放在后, 且**`“()”`**前后各空一格.

比如:
```objective-c
@property (nonatomic, strong) UILabel        *unitLabel;
@property (nonatomic, strong) UIImageView    *bgView;
@property (nonatomic, strong) NSMutableArray *dayDataObjects;
```
错误写法:
```objective-c
@property ( nonatomic, retain ) UIScrollView*   navScrollView;
@property ( nonatomic, retain ) NSMutableArray* ItemBtns;
```

---
## @implementation规范

* 禁止使用**`@synthesize`**关键字, **`@property`**已经自动帮我们声明了**`Setter`**和**`Getter`**方法, 如有特殊需求可重写**`Setter`**方法, 所以不需要再使用**`@synthesize`**.

错误写法:
```objective-c
@implementation FreeExperienceView
@synthesize segment    = _segment;
@synthesize dataInfo   = _dataInfo;
@synthesize delegate   = _delegate;
@synthesize MyEXPView  = _MyEXPView
@synthesize canEXPView = _canEXPView;
@synthesize isRefresh  = _isRefresh;
```

---
## 实例规范

* 一个实例变量出现属性赋值时, 如果是以**`“=”`**赋值, 必须以**`“=”`**对齐, 如果以**`“[]”`**赋值, 必须以开头第一个**`“[”`**对齐.

比如:
```objective-c
- (void)setTextFieldDelegate:(id<UITextFieldDelegate>)textFieldDelegate {
    
    self.phoneTextFieldOne.delegate   = textFieldDelegate;
	self.phoneTextFieldTwo.delegate   = textFieldDelegate;
    self.phoneTextFieldThree.delegate = textFieldDelegate;
    self.reviewPassword.delegate      = textFieldDelegate;
    self.confirmPassword.delegate     = textFieldDelegate;
}
```
错误写法:
```objective-c
- (id) initWithFrame:(CGRect)frame {
    
    self = [super initWithFrame:frame];
   	if ( self )
   	{
  	   [self setBackgroundColor:TRAFFICDETAILBACGROUNDCOLOR];
        
		if ( !_ItemBtns ) {
   	       _ItemBtns = [[NSMutableArray alloc] init] ;
   	    }
   	    _mnScrollViewWidth = kWidthToFit(94); 
  	    self.colorNoSel = UIColorFromRGB(0xdee6ea) ;
   	    self.colorSel = UIColorFromRGB(0xcdd0d2) ;
        
   	    [self addSubview:self.navScrollView];
	}
    
	return self;
}
```

---
* 当出现多个实例变量时, 应该使用代码块的思想**`(特殊情况除外)`**, 把它们组成一个模块一个模块.

比如:

```objective-c
- (void)someMethod {
  
	Person *person = [[Person alloc] init];
  	person.name    = @"xiaoming";
  	person.age	   = 17;
  
	Car *newCar = [[Car alloc] init];
    newCar.name = @"保时捷";
}
```

错误写法:

```objective-c
- (void)someMethod {
  
	Person *person = [[Person alloc] init];
  	person.name    = @"xiaoming";
  	person.age	   = 17;
	Car *newCar = [[Car alloc] init];
    newCar.name = @"保时捷";
}
```



---
* 禁止在实例对象, 赋值, 调用方法后的**`“;”`**与前面代码空格.

比如:
```objective-c
- (void)itemBtnSel:(NSInteger)nIndex {
    
	self.nCurrentIndex = nIndex;
    
	[_delegate itemDidSelectedWithIndex:_nCurrentIndex];
}
```

错误写法:
```objective-c
- (void) ItemBtnSel:(NSInteger) nIndex {
	self.nCurrentIndex = nIndex ;
	[_delegate itemDidSelectedWithIndex:_nCurrentIndex] ;
}
```

---

* 在制类型转换时, 函数与函数之间不放置空格.

比如:
```objective-c
NSString *userName = (NSString*)student;
```
错误写法:
```objective-c
NSString *userName = (NSString *) student;
```
---
## NSDictionary规范

* 当**`NSDictionary`**里的**`Key`** : **`Value`**过多时, 应拆分为多行显示, 并以 **`":"`** 对齐.

比如:
```objective-c
NSDictionary *people = @{@"xiaoming" : 18,
                         @"xiaohong" : 19,
                         @"xiaowang" : 20};         
```
错误写法:
```objective-c
NSDictionary *people = @{@"xiaoming":18,@"xiaohong":19,@"xiaowang":20};         
```

---
## NSArray规范

* 当**`NSArray`**里的元素过多时, 应拆分为多行显示, 并以第一个元素对齐.

比如:
```objective-c
NSArray *nameArray = @[@"小明", 
					   @"小红, 
        	           @"小王"];         
```
错误写法:
```objective-c
NSArray *nameArray = @[@"小明",@"小红",@"小王"];         
```

---
## 函数规范

* 在声明函数时**`“-”`**与**`“(type)”`**必须空一格, 且后面的参数类型与**`“*”`**也必须空一格.

比如:
```objective-c
- (void)ItemBtnSel:(NSInteger)nIndex {
    
	self.nCurrentIndex = nIndex;
    
	[_delegate itemDidSelectedWithIndex:_nCurrentIndex];
}
```
错误写法:
```objective-c
-(void) ItemBtnAction:(UIButton*)button {
    
	self.nCurrentIndex = [_ItemBtns indexOfObject:button];
    
	[_delegate itemDidSelectedWithIndex:_nCurrentIndex];
}
```

---
* 方法与方法之间相隔一行的间距, 禁止不空行或多空行. 

比如:
```objective-c
- (instancetype)initWithFrame:(CGRect)frame {
    
    if (self = [super initWithFrame:frame]) {
		//Code Body
	}    
	return self;
}

- (void)someMethod {
	//Code Body
}
```
错误写法:
```objective-c
- (instancetype)initWithFrame:(CGRect)frame {
    
    if (self = [super initWithFrame:frame]) {
		//Code Body
	}    
	return self;
}
- (void)someMethod {
	//Code Body
}
```
```objective-c
- (instancetype)initWithFrame:(CGRect)frame {
    
    if (self = [super initWithFrame:frame]) {
		//Code Body
	}    
	return self;
}



- (void)someMethod {
	//Code Body
}
```
---
* 在每个方法定义前需要留白一行, 也就是每个方法之间留空一行, 如果是系统的方法则可以不留空.

比如:
```objective-c
- (void)viewDidLoad {
	[super viewDidLoad];

	// Code Body
}
```
错误写法:
```objective-c
- (void)someMethod {}

	[self someMethod];
}
```

---
* 在函数体内, 如果第一句调用的是系统方法, 可不换行, 如果是自定义的方法**`(包括if-else和for-in)`**, 必须换行.

比如:
```objective-c
- (void *)mineViewModel {

	//Custom Function
}

- (void)didReceiveMemoryWarning {
	[super didReceiveMemoryWarning];
}
```
错误写法:
```objective-c
- (void *)mineViewModel {
	//Custom Function
}

- (void)didReceiveMemoryWarning {
	[super didReceiveMemoryWarning];
}
```
---
* 在函数体里, 无论是什么结束, 都无需换行, 直接与**`“}”`**紧挨.

比如:
``` objective-c
- (NSString *)iconImageName {
	
	    return @"icon_nav5";
}
```

错误写法:
``` objective-c
- (NSString *)iconImageName {	
	    return @"icon_nav5";
}
```
---
* 任意行代码不能超过80个字符, 如果超过80个字符, 可以考虑多行显示, 比如有多个参数时, 可以每个参数放一行.

比如: 
``` objective-c
- (void)replaceObjectsInRange:(NSRange)range 
		 withObjectsFromArray:(NSArray<ObjectType> *)otherArray 
					    range:(NSRange)otherRange; 
```
---
## If-Else规范

* 如果在方法中出现**`if-else`**判断, 我们应该使用结构清晰的排版方式, **`if-else`**语句与方法名空行, 与**`return`**语句可以不用空行.

比如:

``` objective-c
- (instancetype)initWithFrame:(CGRect)frame {
	  
	if (self = [super initWithFrame:frame]) {
		// code body
	}
	return self;
}
```
错误写法:
``` objective-c
- (instancetype)initWithFrame:(CGRect)frame {
	if (self = [super initWithFrame:frame]) {
		// code body
	}
	return self;
}
```
* **`if-else`**内部也必须跟着空行, 在**`else`**之后的**`"}"`**可不空行.

比如:
```objective-c
- (void)viewDidLoad {
    [super viewDidLoad];
    
	if (age < 0) {
	
		// Code Body		
	}
}
```
错误写法:
```objective-c
- (void)viewDidLoad {
    [super viewDidLoad];
    
	if (age < 0) {
		// Code Body
	}
}
```
* **`if-else`**超过四层的时候, 就要考虑重构, 多层的**`if-else`**结构很难维护.

比如:
```objective-c
- (void)viewDidLoad {
    [super viewDidLoad];

	if (condition) {
	
		// Code Body
		
	} else if (condition){
	
		// Code Body
		
	} else if (condition){
	
		// Code Body
		
	} else if (condition){
	
		// Code Body
		
	} else if (condition){
	
		// Code Body
		
	} else if (condition){
	
		// Code Body
		
	} else {
	
		// Code Body
	}
}
```

* 合理使用**`if-else`**, 当某个场景只需满足一个条件才能进入**`if-else`**时, 应该把**`if-else`**抽成一个模块.

比如:
```objective-c
- (void)viewDidLoad {
    [super viewDidLoad];
    
	if (age < 0) {
	
		NSLog(@"这是错误的年龄");
		
		return;
	}

	NSLog(@"现在时%ld岁", (long)age):
}
```
错误写法:
```objective-c
- (void)viewDidLoad {
    [super viewDidLoad];
    
	if (age < 0) {
	
		NSLog(@"这是错误的年龄");
		
	} else {
	
		NSLog(@"现在时%ld岁", (long)age):
	}
}
```
---
* 在使用**`if-else`**时必须加`"{}"`符号, 哪怕是一行判断.

比如:
```objective-c
- (void)someMethod {
	
	if (Condition) {
	
		// Code Body
	} else {
	
		// Code Body
	}
}
```
错误写法:
```objective-c
- (void)someMethod {
	
	if (Condition) // Code Body
	else // Code Body
}
```
```objective-c
- (void)someMethod {
	
	if (Condition) // Code Body
	
	// Code Body
}
```
---
## For-In & For 规范

* 在**`"for(for-in)"`**中, 里面的参数必须严格按照上文所示的**`实例规范`**来声明, 且是兼容64位的类型.

比如:
``` objective-c
- (void)viewDidLoad {
    [super viewDidLoad];
    
	for (NSInteger i = 0; i < 10; i++) {
		// code body
	}
}
```
错误写法:
``` objective-c
- (void)viewDidLoad {
    [super viewDidLoad];
    
	for (NSInteger i=0;i<10;i++) {
		// code body
	}
}
```
---
* 当函数中需要使用到**`"for(for-in)"`**, 如果该**`"for(for-in)"`**是在函数的第一句, 必须和上文的**`"if-else"`**一样空行, 与**`return`**语句可不空行.

比如:
``` objective-c
- (void)someMethod {
	  
	for (NSInteger i = 0; i < 10; i++) {
		// code body
	}
}
```
 错误写法:
``` objective-c
- (void)someMethod {
	for (NSInteger i = 0; i < 10; i++) {
		// code body
	}
}
```
---
## Block规范
* 在函数中使用到**`Block`**时, 与**`if-else`**或者**`for-in`**不太一样, **`Block`**第一行与代码块必须得空行, 无论方法是否是系统自带的.

比如:
```objective-c
- (void)someMethod {
        
    [className blockName:^(parameter) {
        
        // Code Body
    }];
}
```
错误写法:
```objective-c
- (void)someMethod {
        
    [className blockName:^(parameter) {
        // Code Body
    }];
}
```
---
## 运算符规范

* 一元运算符和参数之间不放置空格, 比如**`"!"`**非运算符, **`"&"`**安位与, **`"|"`**安位或.

比如: 
``` objective-c
BOOL isOpen  = true;
BOOL isClose = !isOpen;
```
错误写法:
``` objective-c
BOOL isOpen  = true;
BOOL isClose = ! isOpen;
```
<dr>
``` objective-c
BOOL isOpen=true;
BOOL isClose=!isOpen;
```
---

* 二元运算符和参数之间要有空格, 如赋值号**`"="`**左右各留一个空格.

比如: 
``` objective-c
self.myString = @“mySring”;
```

错误写法:
``` objective-c
self.myString=@"myString";
```
---
* 三目运算符和参数之间必须得有空格, 如判断符**`"?"`**结果符**`":"`**

比如:
``` objective-c
NSInteger userAge = @"Man" ? 18 : 19;
```
错误写法:	
``` objective-c
NSInteger userAge = @"Man"?18:19;
```
---
# 命名规范



## 实例命名规范

* 使用完整的英文描述来准确描述**`Variable /Class /Define /Notes`**, 禁止使用拼音命名, 不建议建议使用缩写.

比如:
``` objective-c
NSString *userName = @"小明";
```
错误写法:
``` objective-c
NSString *uName = @"小明";
```
---
* 使用本行业的专业术语, 如果是消费者的话就要使用消费者对应的名词, 用户的话就使用用户对应的名词, 并且以**`“=”`**对齐, 禁止夸域命名. 

比如:
``` objective-c
NSString *userName = @"小明";
NSInteger userAge  = 18;
CGFloat userHeight = 170.0f;
```
错误写法:
``` objective-c
NSString *uName = @"小明";
NSInteger uAge  = 18;
CGFloat uHeight = 170.5f;
```
---
* 使用**`Apple`**推荐的驼峰命名方式来编写代码, 方法开头第一个字母必须小写(特殊命名除外), 禁止使用随性的命名方式.

比如:
``` objective-c
- (CGPoint)convertPoint:(CGPoint)point toView:(nullable UIView *)view;
```

错误写法:
``` objective-c
- (CGPoint)ConverTPoint:(CGPoint)POINT ToView:(nullable UIView *)view;
```
---
## @Property命名规范

* 尽量少用缩写, 使用**`Apple`**推荐的短句命名法命名且第一个字母必须小写, 这样子做, 可以省略再注释处理.

比如:
``` objective-c
@property (readonly, copy) NSString *decomposedStringWithCanonicalMapping;
@property (readonly, copy) NSString *precomposedStringWithCanonicalMapping;
@property (readonly, copy) NSString *decomposedStringWithCompatibilityMapping;
@property (readonly, copy) NSString *precomposedStringWithCompatibilityMapping;
```
错误写法:
``` objective-c
@property (readonly, copy) NSString *uName;
@property (readonly, assign) NSInteger *uAge;
@property (readonly, assign) CGFloat *uHeight;
```
---
## @Interface->class命名规范

* 尽量使用有意义的英文名字命名, 拒绝使用**`"i"`**,  **`"j"`**等无意义的字符命名, 类的命名首字母大写,  其他变量的命名首字符小写.

比如:
```objective-c
@interface People : SuperClassName
@end
```
错误写法:
```objective-c
@interface people : SuperClassName
@end
```


```objective-c
@interface ren : SuperClassName
@end
```



---
## #Define命名规范

* 使用**`#define`**定义预编译宏时, 应当把宏定义成全部大写字母, 且与**`“_”`**分隔, 此方法是苹果官方所推荐.

比如:

```objective-c
#define NS_AVAILABLE(_mac, _ios) CF_AVAILABLE(_mac, _ios)
#define NS_AVAILABLE_MAC(_mac) CF_AVAILABLE_MAC(_mac)
#define NS_AVAILABLE_IOS(_ios) CF_AVAILABLE_IOS(_ios)
```

错误写法:

```objective-c
#define kCancelBottom  25
#define kCancelHeight  44
#define kCancelMargins 25
```

---

## Block命名规范

* 尽量使用有意义的命名方法, 禁止使用简称去命名.

比如:
```objective-c
@property (nonatomic, copy) void(^AspWebNavigationRightBtnBlock)(parameter);
```
错误写法:
```objective-c
@property (nonatomic, copy) void(^AspWNRBBlock)(parameter);
```
---
## For-In命名规范

* 在使用快速遍历**`for-in`**时, 其中的参数需要根据对应的元素进行一一对应来命名.

比如:
```objective-c
NSArray *numberArray = @[@1, @2, @3, @4, @5 , @6, @7, @8, @9];
    
for (id number in numberArray) {

	NSLog(@"%@", number);
}
```

错误写法:
```objective-c
NSArray *numberArray = @[@1, @2, @3, @4, @5 , @6, @7, @8, @9];
    
for (id item in numberArray) {
        
	NSLog(@"%@", item);
}
```
```objective-c
NSArray *numberArray = @[@1, @2, @3, @4, @5 , @6, @7, @8, @9];
    
for (id abc in numberArray) {
        
	NSLog(@"%@", item);
}
```
---
# 布局框架



---
* 在项目开发中,  我们经常会遇到`View`需要布局的情况, 通常我们会使用`frame`, `size`, `center`, `bounds`等属性去给`View`布局, 而且还需要我们给每个设备的屏幕一一对应的适配计算, 界面布局所花的代码量等同于业务的三分之一, 而且还不容易理解.

* 但这个问题在2011之后就已经被解决了, 当时`Apple`引用了`Cassowary constraint-solving`算法, 并将这个算法命名为`AutoLayout`, 可以在绝大多数的情况下, 完美的解决屏幕适配的问题, 而且`AutoLayout`的黑魔法还不止于此, 想知道更多的同学可以去查查资料**[AutoLayout](http://www.starming.com/index.php?v=index&view=84)**, 了解更多的黑魔法.

* 随着`Apple`逐渐的完善, 许多iOS开发者纷纷推出了自己封装的`AutoLayout`库, 其中**[Masonry](https://github.com/SnapKit/Masonry)**就是众多AutoLayout库之一, 为什么这里只推荐`Masonry`, 同学们自己去百度一下就明白了, 在GitHub里英文的使用手册, 如果你需要中文使用手册的话, 这里也可以提供**[Masonry中文使用手册](http://www.cocoachina.com/ios/20141219/10702.html)**

> **注意: 在工程中禁止使用`Xib`, 禁止在`StoryBoard`拖入任何控件, 且`StoryBoard`只可作为项目架构所使用.**

---
# 文件夹层次结构


## MVC架构

`MVC`是一种使用`MVC(Model View Controller 模型-视图-控制器)`, 有几大优点：

> * **耦合性低:** 视图层和业务层分离，这样就允许更改视图层代码而不用重新编译模型和控制器代码，同样，一个应用的业务流程或者业务规则的改变只需要改动`MVC`的模型层即可。因为模型与控制器和视图相分离，所以很容易改变应用程序的数据层和业务规则。
> * **重用性高:** 随着技术的不断进步，需要用越来越多的方式来访问应用程序。而`MVC`则可以在同一个模块下, 多个应用去访问, 不需要再去重写。
> * **生命周期成本低:** MVC使开发和维护用户接口的技术含量降低。
> * **部署快:**  使用MVC模式使开发时间得到相当大的缩减，它使程序员集中精力于业务逻辑，界面程序员集中精力于表现形式上。
> * **可维护性高:** 分离视图层和业务逻辑层也使得应用更易于维护和修改。
> * **有利软件工程化管理:** 由于不同的层各司其职，每一层不同的应用具有某些相同的特征，有利于通过工程化、工具化管理程序代码。 


当然`MVC`也有它的缺点:

> * **没有明确的定义:**完全理解`MVC`并不是很容易。使用`MVC`需要精心的计划，由于它的内部原理比较复杂，所以需要花费一些时间去思考。同时由于模型和视图要严格的分离，这样也给调试应用程序带来了一定的困难。每个构件在使用之前都需要经过彻底的测试。
> * **不适合小型，中等规模的应用程序:** 花费大量时间将MVC应用到规模并不是很大的应用程序通常会得不偿失。
> * **增加系统结构和实现的复杂性:** 对于简单的界面，严格遵循`MVC`，使模型、视图与控制器分离，会增加结构的复杂性，并可能产生过多的更新操作，降低运行效率。
> * **视图与控制器间的过于紧密的连接:** 视图与控制器是相互分离，但却是联系紧密的部件，视图没有控制器的存在，其应用是很有限的，反之亦然，这样就妨碍了他们的独立重用。
> * **视图对模型数据的低效率访问:** 依据模型操作接口的不同，视图可能需要多次调用才能获得足够的显示数据。对未变化数据的不必要的频繁访问，也将损害操作性能。
> * **一般高级的界面工具或构造器不支持模式:** 改造这些工具以适应`MVC`需要和建立分离的部件的代价是很高的，会造成`MVC`使用的困难。

---
## MVVM架构

`MVVM`模式和`MVC`模式一样，主要目的是分离视图`View`和模型`Model`，有几大优点

> * **低耦合**。视图`View`可以独立于`Model`变化和修改，一个`ViewModel`可以绑定到不同的`View`上，当`View`变化的时候`Model`可以不变，当`Model`变化的时候`View`也可以不变。
> * **可重用性**。你可以把一些视图逻辑放在一个`ViewModel`里面，让很多`View`重用这段视图逻辑。
> * **独立开发**。开发人员可以专注于业务逻辑和数据的开发`ViewModel`，设计人员可以专注于页面设计，使用`Expression Blend`可以很容易设计界面并生成`XAML`代码。
> * **可测试**。界面素来是比较难于测试的，而现在测试可以针对`ViewModel`来写。
> * **结构**。通常`MVVM`架构图如图所示, 且开头首字母为大写



