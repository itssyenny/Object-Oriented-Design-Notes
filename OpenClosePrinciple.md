# 开闭原则
	- 实体如类， 模块和函数对扩展放开， 对修改关闭。
	- 有抽象构建框架， 用实现扩展细节
	- 如果要满足新的要求， 需要先从抽象类（接口）开始改动。
	* 增加了程序的可扩展性； 



## 不好的设计
Course类声明（declare）了最初在线课程所需要包含的数据：

```objective-c
@interface Course: NSObject 

@property (nonatomic, copy) NSString *courseTitle;
@property (nonatomic, copy) NSString *courseIntroduction;
@property (nonatomic, copy) NSString *teacherName;
@property (nonatomic, copy) NSString *content;

// 新需求： 视频课程
@property (nonatomic, copy) NSString *videoUrl;

// 新需求： 音频课程
@property (nonatomic, copy) NSString *audioUrl;

// 新需求： 直播课程
@property (nonatomic, copy) NSString *liveUrl;

@end

```

原因： 因为该设计没有遵循对修改关闭， 对扩展开闭原则。 而反其道而行 （opposite）：开放修改， 而且不给扩展提供便利
	1. 随着需求的增加， 需要反复修改之前已创建的类。
    2. 给新增的类造成了不必要的冗余 （redundancy）

## 好的设计

```objective-c
@interface CourseAbstraction: NSObject 

@property (nonatomic, copy) NSString *courseTitle;
@property (nonatomic, copy) NSString *courseIntroduction;
@property (nonatomic, copy) NSString *teacherName;

@end

// 文字课程类
@interface TextCourse: CourseAbstraction

@property (nonatomic, copy) NSString *content;

@end

// 视频课程类
@interface VideoCourse: CourseAbstraction

@property (nonatomic, copy) NSString *videoUrl;

@end

// 音频课程类
@interface AudioCourse: CourseAbstraction

@property (nonatomic, copy) NSString *audioUrl;

@end

// 直播课程类：
@interface LiveCourse : Course

@property (nonatomic, copy) NSString *liveUrl;

@end
```



