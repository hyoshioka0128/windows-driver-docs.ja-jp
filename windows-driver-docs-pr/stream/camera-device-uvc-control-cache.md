---
title: Uvc コントロールキャッシュのドライバーサポート
description: デバイスのカメラコントロールキャッシュを明示的に利用する方法について説明します。
ms.date: 08/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 37b39543f8000d5cf4256dfa22d0f975ad0f457b
ms.sourcegitcommit: dff3834724bd5204c4a47204540fe8125dd37b20
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2019
ms.locfileid: "70775186"
---
# <a name="driver-support-for-camera-uvc-control-cache"></a>カメラ UVC コントロールキャッシュのドライバーサポート

UVC コントロールは、フレームサーバーがシャットダウンしたときにデバイスに対してスティックを維持します。 UVC コントロールとの間に白いバランスを設定してアプリをシャットダウンするアプリを使用する場合、カメラの白いバランスはリセットされません。 ホワイトバランスを変更せずに他のアプリを開くと、以前の設定が継承されます。

1つの例外として、コンピューターが S3 に入る場合があります。 カメラデバイスが D3 と D3 のどちらになっているかによって、UVC コントロールがそれぞれスティックに表示されるかどうかによって異なります。 この動作は、D3 コールドによってカメラから電力が削除されるためです。

キャッシュ UVC 制御プロトコルを利用することは、アプリケーションセッション、S3、コンピューターのシャットダウン間で一貫した動作を実現するための手段です。
  
MS OS 2.0 記述子またはカスタム INF ファイルの古い方法によってデバイス HW レジストリキーの構成キー "CacheUVCControl" を DWORD 値1に設定すると、カメラは S3 またはコンピューターの再起動の間にユーザーが設定した UVC コントロールの値を保持します。 保存および再適用される特定の UVC コントロール値の一覧を次に示します。

## <a name="uvc-controls-affected"></a>影響を受ける UVC コントロール

次に、再起動によってキャッシュおよび再適用される UVC コントロールの一覧を示します。

- KSPROPERTY_VIDEOPROCAMP_BRIGHTNESS
- KSPROPERTY_VIDEOPROCAMP_CONTRAST
- KSPROPERTY_VIDEOPROCAMP_GAIN
- KSPROPERTY_VIDEOPROCAMP_GAMMA
- KSPROPERTY_VIDEOPROCAMP_HUE (+ AUTO)
- KSPROPERTY_VIDEOPROCAMP_SATURATION
- KSPROPERTY_VIDEOPROCAMP_SHARPNESS
- KSPROPERTY_VIDEOPROCAMP_WHITEBALANCE (+ AUTO)

## <a name="inf-example"></a>INF の例

```cpp
[Device.AddReg.HW]
HKR,,"CacheUVCControl",0x00010001,1
```

## <a name="ms-os-20-descriptor-example"></a>MS OS 2.0 記述子の例

```cpp
UCHAR Example_MSOS20DescriptorSet_CacheUVCControl[0x38] =
{
    //
    // Microsoft OS 2.0 Descriptor Set Header
    //
    0x0A, 0x00,               // wLength - 10 bytes
    0x00, 0x00,               // MSOS20_SET_HEADER_DESCRIPTOR
    0x00, 0x00, 0x0?, 0x06,   // dwWindowsVersion – 0x060?0000 for future Windows version
    0x3C, 0x00,               // wTotalLength – 60 bytes

    //
    // Microsoft OS 2.0 Registry Value Feature Descriptor
    //
    0x32, 0x00,               // wLength 0x32 (50) in bytes of this descriptor  
    0x04, 0x00,               // wDescriptorType – MSOS20_FEATURE_REG_PROPERTY  
    0x04, 0x00,               // wPropertyDataType - REG_DWORD  
    0x24, 0x00,               // wPropertyNameLength – 0x24 (36) bytes
    'C',  0x00, 'a',  0x00,   // Property Name - “CacheUVCControl”  
    'c',  0x00, 'h',  0x00,  
    'e',  0x00, 'U',  0x00,
    'V',  0x00, 'C',  0x00,  
    'C',  0x00, 'o',  0x00,  
    'n',  0x00, 't',  0x00,  
    'r',  0x00, 'o',  0x00,  
    'l',  0x00, 0x00, 0x00,
    0x00, 0x00, 0x00, 0x00,
    0x04, 0x00,               // wPropertyDataLength – 4 bytes  
    0x01, 0x00, 0x00, 0x00,   // Enable to cache UVC controls  
}
```
