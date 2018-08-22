
#自定义相机无法使用的问题描述及解决方案

##描述:
    使用AVCaptureSession等相关自定义相机类的时候,遇到了,无法开始录像,结束录像,代理方法统统不走
##解决方案:使用的时候需要手动调用 [_captureSession startRunning];

#修改UIDatePickerView的文字颜色和背景色
	//设置成白色
	[selectionDatePicker setValue:[UIColor whiteColor] forKey:@"textColor"];
	
用KVC 强行给它设置成了白色,感觉已经解决需求,但是突然又发现了一个问题:每次滑到今天的日期,文字颜色又TM变成了黑色,不要慌,这时候方法混淆又可以登场了 首先我们找到需要混淆的方法  setHighlightsToday,就是它 然后强制混淆这个方法.给他设置一个NO,这样就完成了:

	SEL selector = NSSelectorFromString(@"setHighlightsToday:");
        	NSInvocation *invocation = [NSInvocation invocationWithMethodSignature:[UIDatePicker instanceMethodSignatureForSelector:selector]];
        	BOOL no = NO;
    		[invocation setSelector:selector];
      	 [invocation setArgument:&no atIndex:2];
        [invocation invokeWithTarget:selectionDatePicker];


