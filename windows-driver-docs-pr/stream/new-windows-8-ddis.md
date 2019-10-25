---
title: Windows 8 用の新しい AVStream インターフェイス
ms.assetid: B3C223BD-2A00-4B87-9D0E-557C0CA3F2DE
description: Windows 8 用に新規または更新された AVStream streaming media driver インターフェイスに関する情報を提供します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd06a0589b3bf3b6ef9c0ed9627cff9dbe4adb6f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823596"
---
# <a name="new-avstream-interfaces-for-windows-8"></a>Windows 8 用の新しい AVStream インターフェイス


Windows 8 では、次の AVStream ストリーミングメディアドライバーインターフェイスが新しく追加または更新されています。

## <a name="extended-camera-control-interface"></a>拡張カメラコントロールインターフェイス


この既存のインターフェイスの拡張機能は、イメージのキャプチャ中にカメラの機能を制御するために使用されます。 「[拡張カメラコントロールのプロパティ](extended-camera-control-properties.md)」を参照してください。

## <a name="usb-video-class-15-driver-update-h264-video-codec"></a>USB ビデオクラス1.5 ドライバー更新プログラム (h.264 ビデオコーデック)


Windows 8 以降では、USB ビデオクラスドライバーの新しいバージョン1.5 がサポートされています。 このドライバー更新プログラムには、h.264 ビデオコーデック標準が組み込まれています。次のトピックで説明します。

-   [USB ビデオクラスドライバーの概要](usb-video-class-driver-overview.md)
-   [USB h.264 ビデオカメラのサポート](usb-h-264-video-cameras-support.md)
-   [**KS\_DATAFORMAT\_H264VIDEOINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_dataformat_h264videoinfo)
-   [**KS\_DATARANGE H264\_ビデオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_h264_video)
-   [**KS\_H264VIDEOINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_h264videoinfo)

さらに、新しい定数値が[**KS\_VideoControlFlags**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ks_videocontrolflags)列挙体に追加されました。

## <a name="image-data-format-structures"></a>Image データ形式の構造


これらの構造体は、JPEG イメージのキャプチャおよびエンコードと共に使用して、pin (またはストリーム) のイメージデータを指定します。

-   [**KS\_DATAFORMAT\_IMAGEINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_dataformat_imageinfo)
-   [**KS\_DATARANGE\_イメージ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_image)

## <a name="device-removal-and-preemption"></a>デバイスの削除とプリエンプション


この新しいインターフェイスは、カメラデバイスがシステムから削除された (紛失した) 場合、または新しい UWP アプリによって割り込まれた場合に使用されます。

-   [**KSEVENTSETID\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/stream/kseventsetid-device)
-   [**KSEVENT\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ne-ks-ksevent_device)
-   [**KSEVENT\_デバイス\_失われました**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-device-lost)
-   [**KSEVENT\_デバイス\_割り込まれる**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-device-preempted)

 

 




