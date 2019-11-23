---
title: USB H.264 ビデオ カメラのサポート
description: Windows 8 以降では、h.264 ビデオコーデック (エンコーダー/デコーダー) がサポートされています。
ms.assetid: EB73E2B2-B34E-4DC1-807A-4990A54E6E8D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1ca0f9bb2c36928f7935e51dc5d683a9331a7ba
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842620"
---
# <a name="usb-h264-video-cameras-support"></a>USB H.264 ビデオ カメラのサポート


Windows 8 以降では、h.264 ビデオコーデック (エンコーダー/デコーダー) がサポートされています。 コーデックは、高品質で解像度の高いビデオストリーミングを可能にするビデオデータをエンコードおよびデコードするためのアルゴリズムに基づいています。 Windows 8 UVC クラスドライバーでサポートされている機能の一部を次に示します。 Usbvideo は、すぐに利用できます。

-   H.264 ビデオカメラでサポートされている機能の検出。
-   ビデオカメラの h.264 ストリームのセッションネゴシエーション。
-   カメラからの h.264 ペイロードのストリーミング。
-   H.264 ビデオカメラでサポートされている機能の検出。

H.264 コーデックは、効率的なビデオ圧縮を使用して、冗長なビデオデータを削減および削除します。 これにより、デジタルビデオファイルを効率的に保存し、ネットワーク経由で交換できます。

専用ドライバーではなく、UVC クラスドライバーの Usbvideo を使用する場合は、次に説明するガイドラインに従って、デバイスでビデオストリーミングファームウェアを実装する必要があります。

### <a name="firmware-guidelines"></a>ファームウェアのガイドライン

UVC クラスドライバー Usbvideo はビデオカメラを直接照会してその機能を取得し、専用のドライバーを必要とせずにデバイスをドライブにします。 現在のガイドラインの実装については、「h.264/MPEG-2 のビデオクラスドライバーの仕様」を参照してください。 また、h.264[の USB ビデオクラスに対する Microsoft の提案](https://go.microsoft.com/fwlink/p/?LinkId=233063)された拡張機能についても参照してください。

公式のガイドラインは、今後の標準ドキュメントで公開される予定です。[ビデオデバイスの仕様については、ユニバーサルシリアルバスデバイスクラスの定義に関する](https://go.microsoft.com/fwlink/p/?linkid=516989)記事に記載されています **。  。**

 

## <a name="related-topics"></a>関連トピック
[**KS\_DATAFORMAT\_H264VIDEOINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_dataformat_h264videoinfo)  
[**KS\_DATARANGE H264\_ビデオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_h264_video)\_  
[**KS\_H264VIDEOINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_h264videoinfo)  



