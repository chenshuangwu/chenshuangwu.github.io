---
title: IOS开发笔记
date: 2021-05-17 14:27:55
tags: OC UIKit
---

### UILable
- 设置文字颜色
label.textColor = [UIColor redColor];

### UIButton
- 设置圆角
btn.layer.cornerRadius = 10;

- 设置image
btn setImage:nullable UIImage *) forState:UIControlState)

### 动画
```objective-C
[UIView animateWithDuration:(NSTimeInterval) animations:^(void)animations]
[UIView animateWithDuration:(NSTimeInterval) animations:^(void)animations completion:^(BOOL finished)completion]
[UIView animateWithDuration:(NSTimeInterval) delay:(NSTimeInterval) options:(UIViewAnimationOptions) animations:^(void)animations completion:^(BOOL finished)completion]
```

### 改变状态栏
改变颜色
- (UIStatusBarStyle)preferredStatusBarStyle {
    return UIStatusBarStyleLightContent;
}

隐藏状态栏
- (BOOL)prefersStatusBarHidden {
    return YES;
}

### 计时器
```objective-C
NSTimer *timer = [NSTimer scheduledTimerWithTimeInterval:(NSTimeInterval) target:(nonnull id) selector:(nonnull SEL) userInfo:(nullable id) repeats:(BOOL)]
```


### 通知
- 监听通知

【NSNotificationCenter defaultCenter] addObserer:(id) selector:(SEL) name:(NSString *) object:(id)


### UIView
当一个view被添加到父控件中,就会调用

\- (void)didMoveToSuperview


### 约束
NSLayoutConstraint *layout = [NSLayoutConstraint constraintWithItem:(nonnull id) attribute:(NSLayoutAttribute) relatedBy:(NSLayoutRelation) toItem:(nullable id) attribute:(NSLayoutAttribute) multiplier:(CGFloat) constant:(CGFloat)]


### IOS 13 自定义控制器
IOS 13 之后在SceneDelegate.m文件中设置

```objective-C
- (void)scene:(UIScene *)scene willConnectToSession:(UISceneSession *)session options:(UISceneConnectionOptions *)connectionOptions {
    DHHomeViewController *hmVc = [[DHHomeViewController alloc] init];
    UIWindowScene *windowScene = (UIWindowScene *)scene;
    self.window = [[UIWindow alloc] initWithWindowScene:windowScene];
    self.window.rootViewController = hmVc;
    [self.window makeKeyAndVisible];
}
```