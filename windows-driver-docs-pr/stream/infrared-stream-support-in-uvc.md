---
title: UVC での赤外線ストリームのサポート
description: UVC でサポートされる赤外線ストリーム情報を提供します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 512b58a817cc4efe95a4d48b8bc3d28a1d0ffcfb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360496"
---
# <a name="infrared-stream-support-in-uvc"></a>UVC での赤外線ストリームのサポート

Windows 10 バージョン 1607 以降では、受信トレイの USB ビデオ クラス (UVC) ドライバーは、赤外線 (IR) のストリームを生成するカメラをサポートします。 

これらのカメラはシーンの輝度値をキャプチャし、非圧縮形式として、または圧縮の MJPEG 形式として、USB 経由でフレームを送信します。 これらのカメラと、ストリームは、メディアのキャプチャ パイプライン経由でアプリケーションに公開されます。 

次の IR 形式の種類の Guid を使用して、IR ストリームは、アプリケーションに正しく公開されるように、ストリームのビデオ形式の記述子を指定します。

これら IR 形式の種類の Guid は ksmedia.h で定義されます。

| IR 形式の種類の GUID             | 説明                          |
|---------------------------------|--------------------------------------|
| KSDATAFORMAT_SUBTYPE_L8_IR      | 8 ビットの輝度および専用のフレーム               |
| KSDATAFORMAT_SUBTYPE_L16_IR     | 16 ビットの輝度および専用のフレーム              |
| KSDATAFORMAT_SUBTYPE_MJPEG_IR   | MJPEG 輝度および専用のフレームを圧縮します。    |

これら IR 形式の種類の Guid を指定すると、キャプチャ パイプラインは自動的に、これらのストリームを自分のシナリオの適切なストリームを選択するときのアプリケーションを支援する IR ストリームとしてマークします。

```cpp
// Example: Format descriptor for UVC 1.1 frame based uncompressed format

typedef struct _VIDEO_FORMAT_FRAME
{
    UCHAR bLength;
    UCHAR bDescriptorType;
    UCHAR bDescriptorSubtype;
    UCHAR bFormatIndex;
    UCHAR bNumFrameDescriptors;
    GUID  guidFormat;           // guidFormat must contain one of the IIR format type GUIDs from the table above
    UCHAR bBitsPerPixel;
    UCHAR bDefaultFrameIndex;
    UCHAR bAspectRatioX;
    UCHAR bAspectRatioY;
    UCHAR bmInterlaceFlags;
    UCHAR bCopyProtect;
    UCHAR bVariableSize;
} VIDEO_FORMAT_FRAME, *PVIDEO_FORMAT_FRAME;
```





