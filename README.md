- (void)CreateHoverball {
    HoverballView = [ShiSnGeWindow sharedInstance];
    HoverballView.autoresizingMask = UIViewAutoresizingFlexibleWidth | UIViewAutoresizingFlexibleHeight;
    /// 初始化悬浮球视图
    Button = [[UIButton alloc] initWithFrame:CGRectMake((SCREEN_WIDTH - 35) / 2, 0, 35, 35)];
    Button.backgroundColor = KClearColor;
    Button.layer.cornerRadius = Button.frame.size.width / 2;
    Button.clipsToBounds = YES;
    [Button setTitleColor:[UIColor whiteColor] forState:UIControlStateNormal];
    /// 按钮事件
    [Button addTarget:self action:@selector(StartAndStopMenu) forControlEvents:UIControlEventTouchUpInside];
    /// 按钮透明图
    NSData *imageData = [[NSData alloc] initWithBase64EncodedString: Transparentimage options:NSDataBase64DecodingIgnoreUnknownCharacters];
    dispatch_async(dispatch_get_global_queue(0, 0), ^{
        UIImage *decodedImage = [UIImage imageWithData:imageData];
        dispatch_async(dispatch_get_main_queue(), ^{
            Button.layer.contents = (id)decodedImage.CGImage;
        });
    });
    [HoverballView addSubview:Button];
    isFloating = YES;/// 标记悬浮球为 YES
}
