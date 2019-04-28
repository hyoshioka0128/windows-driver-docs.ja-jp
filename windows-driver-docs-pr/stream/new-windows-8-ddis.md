---
title: Windows 8 用の新しい AVStream インターフェイス
ms.assetid: B3C223BD-2A00-4B87-9D0E-557C0CA3F2DE
description: AVStream ストリーミング メディアに関する情報は、新しいまたは Windows 8 向けに更新されたドライバー インターフェイスを提供します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: feb2052137a12b339916fab962d53ce3696b6dea
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377776"
---
# <a name="new-avstream-interfaces-for-windows-8"></a>Windows 8 用の新しい AVStream インターフェイス


これら AVStream ストリーミング メディア ドライバーのインターフェイスは、新しい Windows 8 向けに更新されました。

## <a name="extended-camera-control-interface"></a>拡張のカメラ コントロール インターフェイス


この拡張機能の既存のインターフェイスは、イメージ キャプチャ中にカメラの機能の制御に使用されます。 参照してください[カメラ コントロールのプロパティを拡張](extended-camera-control-properties.md)します。

## <a name="usb-video-class-15-driver-update-h264-video-codec"></a>USB ビデオ クラス 1.5 ドライバーの更新 (H.264 ビデオ コーデック)


Windows 8 以降では、USB ビデオ クラス ドライバーの新しいバージョン 1.5 がサポートされていること。 このドライバーの更新では、H.264 ビデオ コーデックの標準が組み込まれており、これらのトピックで説明されている場合は。

-   [USB ビデオ クラス ドライバーの概要](usb-video-class-driver-overview.md)
-   [USB H.264 ビデオをカメラのサポート](usb-h-264-video-cameras-support.md)
-   [**KS\_DATAFORMAT\_H264VIDEOINFO**](https://msdn.microsoft.com/library/windows/hardware/hh463996)
-   [**KS\_DATARANGE\_H264\_ビデオ**](https://msdn.microsoft.com/library/windows/hardware/hh464002)
-   [**KS\_H264VIDEOINFO**](https://msdn.microsoft.com/library/windows/hardware/hh464008)

新しい定数の値が追加されているさらに、 [ **KS\_VideoControlFlags** ](https://msdn.microsoft.com/library/windows/hardware/ff567696)列挙体。

## <a name="image-data-format-structures"></a>イメージ データの形式の構造


これらの構造は、JPEG イメージのキャプチャで使用して pin (またはストリーム) にイメージ データを指定するエンコードされます。

-   [**KS\_DATAFORMAT\_IMAGEINFO**](https://msdn.microsoft.com/library/windows/hardware/jj151598)
-   [**KS\_DATARANGE\_イメージ**](https://msdn.microsoft.com/library/windows/hardware/jj151599)

## <a name="device-removal-and-preemption"></a>デバイスの削除および切断


この新しいインターフェイスは、カメラ デバイス (失わ) システムから削除されましたまたは新しい UWP アプリでは割り込まれましたときに使用されます。

-   [**KSEVENTSETID\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/jj156036)
-   [**KSEVENT\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/jj151588)
-   [**KSEVENT\_デバイス\_LOST**](https://msdn.microsoft.com/library/windows/hardware/jj156039)
-   [**KSEVENT\_デバイス\_割り込み**](https://msdn.microsoft.com/library/windows/hardware/jj156040)

 

 




