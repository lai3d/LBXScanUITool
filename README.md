# LBXScanUITool


[LBXScan](https://github.com/MxABC/LBXScan)和([swiftscan](https://github.com/MxABC/swiftScan))扫码界面DIY工具及辅助对参数的理解

LBXScanViewStyle 界面参数，通过mac app展示出来，通过界面上的操作，方便大家理解及找到自己需要的参数值。

请看工具gif图

![image](https://github.com/MxABC/Resource/blob/master/LBXScanUITool.gif)

***
定义代码

```
@interface LBXScanViewStyle : NSObject


#pragma mark -中心位置矩形框
/**
 @brief  是否需要绘制扫码矩形框，默认YES
 */
@property (nonatomic, assign) BOOL isNeedShowRetangle;


/**
 *  默认扫码区域为正方形，如果扫码区域不是正方形，设置宽高比
 */
@property (nonatomic, assign) CGFloat whRatio;


/**
 @brief  矩形框(视频显示透明区)域向上移动偏移量，0表示扫码透明区域在当前视图中心位置，< 0 表示扫码区域下移, >0 表示扫码区域上移
 */
@property (nonatomic, assign) CGFloat centerUpOffset;

/**
 *  矩形框(视频显示透明区)域离界面左边及右边距离，默认60
 */
@property (nonatomic, assign) CGFloat xScanRetangleOffset;

/**
 @brief  矩形框线条颜色
 */
@property (nonatomic, strong) NSColor *colorRetangleLine;



#pragma mark -矩形框(扫码区域)周围4个角
/**
 @brief  扫码区域的4个角类型
 */
@property (nonatomic, assign) LBXScanViewPhotoframeAngleStyle photoframeAngleStyle;

//4个角的颜色
@property (nonatomic, strong) NSColor* colorAngle;

//扫码区域4个角的宽度和高度
@property (nonatomic, assign) CGFloat photoframeAngleW;
@property (nonatomic, assign) CGFloat photoframeAngleH;
/**
 @brief  扫码区域4个角的线条宽度,默认6，建议8到4之间
 */
@property (nonatomic, assign) CGFloat photoframeLineW;




#pragma mark --动画效果
/**
 @brief  扫码动画效果:线条或网格
 */
@property (nonatomic, assign) LBXScanViewAnimationStyle anmiationStyle;

/**
 *  动画效果的图像，如线条或网格的图像，如果为nil，表示不需要动画效果
 */
@property (nonatomic,strong,nullable) NSImage *animationImage;



#pragma mark -非识别区域颜色,默认 RGBA (0,0,0,0.5)

/**
 must be create by [UIColor colorWithRed: green: blue: alpha:]
 */
//notRecognitionArea
@property (nonatomic, strong) NSColor *notRecoginitonArea;


@end

```

*** 
调用代码

```obj-c
- (LBXScanViewStyle*)DIY
{
//设置扫码区域参数
LBXScanViewStyle *style = [[LBXScanViewStyle alloc]init];

//扫码框中心位置与View中心位置上移偏移像素(一般扫码框在视图中心位置上方一点)
style.centerUpOffset = 44;



//扫码框周围4个角的类型设置为在框的上面,可自行修改查看效果
style.photoframeAngleStyle = LBXScanViewPhotoframeAngleStyle_On;

//扫码框周围4个角绘制线段宽度
style.photoframeLineW = 6;

//扫码框周围4个角水平长度
style.photoframeAngleW = 24;

//扫码框周围4个角垂直高度
style.photoframeAngleH = 24;


//动画类型：网格形式，模仿支付宝
style.anmiationStyle = LBXScanViewAnimationStyle_NetGrid;

//动画图片:网格图片
style.animationImage = [UIImage imageNamed:@"CodeScan.bundle/qrcode_scan_part_net"];;

//扫码框周围4个角的颜色
style.colorAngle = [UIColor colorWithRed:65./255. green:174./255. blue:57./255. alpha:1.0];

//是否显示扫码框
style.isNeedShowRetangle = YES;
//扫码框颜色
style.colorRetangleLine = [UIColor colorWithRed:247/255. green:202./255. blue:15./255. alpha:1.0];

//非扫码框区域颜色(扫码框周围颜色，一般颜色略暗)
//必须通过[UIColor colorWithRed: green: blue: alpha:]来创建，内部需要解析成RGBA
style.notRecoginitonArea = [UIColor colorWithRed:0 green:0 blue:0 alpha:0.6];

return style;
}
```
