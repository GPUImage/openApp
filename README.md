# openApp
20种ios滤镜都是基于GPUImage的，有3种滤镜是GPUImage库中包含的，还有17种是Instagram中的经典滤镜

#  自定义GPUImageFilter的例子
>* FWNashvilleFilter
```

https://github.com/GPUImage/openApp/tree/master/FWMeituApp/FWMeituApp/Custom%20Filters
```
>* FWNashvilleFilter.h
```
<!-- FWNashvilleFilter -->

https://github.com/forrestwoo/openApp/blob/6104814d070f6d7fd63bb01a06d20d0046a8a05c/FWLifeApp/FWLifeApp/Custom%20Filters/FWNashvilleFilter.h


#import "GPUImageTwoInputFilter.h"

//创建滤镜效果 ，该类主要实现滤镜的效果，包含一个片段着色程序。它是滤镜效果的具体实现

@interface FWFilter1 : GPUImageTwoInputFilter


@end


//所有滤镜类都继承自GPUImageFilterGroup类.它允许我们所创建的类混合其他滤镜。

//它其实是向FWFilter1类中添加需要的输入纹理图片
@interface FWNashvilleFilter : GPUImageFilterGroup
{
    GPUImagePicture *imageSource ;
}

@end
```

>* FWNashvilleFilter.m
```
<!-- https://github.com/forrestwoo/openApp/blob/6104814d070f6d7fd63bb01a06d20d0046a8a05c/FWLifeApp/FWMeituApp/FWMeituApp/Custom%20Filters/FWNashvilleFilter.m -->

```

>* FWApplyFilter
```
<!-- 应用例子：https://github.com/forrestwoo/openApp/blob/6104814d070f6d7fd63bb01a06d20d0046a8a05c/FWMeituApp/FWMeituApp/Utilies/FWApplyFilter.m -->


+ (UIImage *)applyNashvilleFilter:(UIImage *)image
{
    FWNashvilleFilter *filter = [[FWNashvilleFilter alloc] init];//自定义滤镜

    [filter forceProcessingAtSize:image.size];

    GPUImagePicture *pic = [[GPUImagePicture alloc] initWithImage:image];

    [pic addTarget:filter];// 往GPUImagePicture 添加GPUImageFilterGroup的子类
    
    [pic processImage];// -[GPUImagePicture processImage]:

    [filter useNextFrameForImageCapture];//-[GPUImageFilter useNextFrameForImageCapture]:

    return [filter imageFromCurrentFramebuffer];
}

```

