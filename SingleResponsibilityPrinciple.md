# 单一职责原则
  - 一个类只充许有一个职责， 即只有一个导致该类变更的原因
  - 如果单前类的职责不仅仅有一个， 就应该将本来不属于该类真正的职责分离出去
  - 不仅仅是类， 函数（方法） 也要遵循单一职责原则， 即： 一个函数（方法） 只做一件事情
  
该类会导致清晰的代码， 会让bugs无处藏身， 也有利于bugs的追踪， 也就是降低了程序的维护成本。

## 不好的设计
```objective-c
@interface Employee: NSObject

@property (nonatomic, copy) NSString *name;
@property (nonatomic, copy) NSString *address;
@property (nonatomic, copy) NSString *employeeID;

// 新需求： 计算薪水
- (double)calculateSalary;

// 今年是否晋升(get a promotion)
- (BOOL)willGetPromotionThisYear;

@end
```
该设计违反了单一职责原则， 本来该类只负责保留员工的信息而已
原因： 因为这两个方法并不是员工本身的职责
  - calculateSalary       ： 这个方法的职责（计算薪水）是属于会计部门的
  - willPromotionThisYear ： 这个方法的职责（考核与晋升机制）是属于人事部门的
  
 ## 较好的设计
 
```objective-c
//================== Employee.h ==================

@interface Employee: NSObject

// 初始需求
@property (nonatomic, copy) NSString *name;
@property (nonatomic, copy) NSString *address;
@property (nonatomic, copy) NSString *employeeID;

@end
```

```objective-c
//================== FinancialApartment.h ==================

#import "Employee.h"
// 会计部门类
@interface FinancialApartment: NSObject

//计算薪水
- (double)calculateSalary;

@end

```

```objective-c
//================== HRApartment.h ==================

#import "Employee.h"

// 人事部门类
@interface HRApartment: NSObject

// 今年是否晋升
- (BOOL)willGetPromotionThisYear;

@end
```

## UML 类图对比

PS: 虚线箭头表示依赖关系， 常用在方法参数等， 由【依赖方】指向【被依赖方】
