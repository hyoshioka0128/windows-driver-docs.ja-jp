---
title: Windows 8 用の新しい AVStream インターフェイス
ms.assetid: B3C223BD-2A00-4B87-9D0E-557C0CA3F2DE
description: AVStream ストリーミング メディアに関する情報は、新しいまたは Windows 8 向けに更新されたドライバー インターフェイスを提供します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 338b12fd0d7badc84ce0dde98274f90592ff39d7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363270"
---
# <a name="new-avstream-interfaces-for-windows-8"></a>Windows 8 用の新しい AVStream インターフェイス


これら AVStream ストリーミング メディア ドライバーのインターフェイスは、新しい Windows 8 向けに更新されました。

## <a name="extended-camera-control-interface"></a>拡張のカメラ コントロール インターフェイス


この拡張機能の既存のインターフェイスは、イメージ キャプチャ中にカメラの機能の制御に使用されます。 参照してください[カメラ コントロールのプロパティを拡張](extended-camera-control-properties.md)します。

## <a name="usb-video-class-15-driver-update-h264-video-codec"></a>USB ビデオ クラス 1.5 ドライバーの更新 (H.264 ビデオ コーデック)


Windows 8 以降では、USB ビデオ クラス ドライバーの新しいバージョン 1.5 がサポートされていること。 このドライバーの更新では、H.264 ビデオ コーデックの標準が組み込まれており、これらのトピックで説明されている場合は。

-   [USB ビデオ クラス ドライバーの概要](usb-video-class-driver-overview.md)
-   [USB H.264 ビデオをカメラのサポート](usb-h-264-video-cameras-support.md)
-   [**KS\_DATAFORMAT\_H264VIDEOINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_dataformat_h264videoinfo)
-   [**KS\_DATARANGE\_H264\_ビデオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_datarange_h264_video)
-   [**KS\_H264VIDEOINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_h264videoinfo)

新しい定数の値が追加されているさらに、 [ **KS\_VideoControlFlags** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-ks_videocontrolflags)列挙体。

## <a name="image-data-format-structures"></a>イメージ データの形式の構造


これらの構造は、JPEG イメージのキャプチャで使用して pin (またはストリーム) にイメージ データを指定するエンコードされます。

-   [**KS\_DATAFORMAT\_IMAGEINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_dataformat_imageinfo)
-   [**KS\_DATARANGE\_イメージ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_datarange_image)

## <a name="device-removal-and-preemption"></a>デバイスの削除および切断


この新しいインターフェイスは、カメラ デバイス (失わ) システムから削除されましたまたは新しい UWP アプリでは割り込まれましたときに使用されます。

-   [**KSEVENTSETID\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/stream/kseventsetid-device)
-   [**KSEVENT\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ne-ks-ksevent_device)
-   [**KSEVENT\_デバイス\_LOST**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-device-lost)
-   [**KSEVENT\_デバイス\_割り込み**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-device-preempted)

 

 




