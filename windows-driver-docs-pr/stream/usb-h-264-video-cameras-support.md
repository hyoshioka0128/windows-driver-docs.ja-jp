---
title: USB H.264 ビデオ カメラのサポート
description: Windows 8 以降では、h.264 ビデオコーデック (エンコーダー/デコーダー) がサポートされています。
ms.assetid: EB73E2B2-B34E-4DC1-807A-4990A54E6E8D
ms.date: 06/19/2020
ms.localizationpriority: medium
ms.openlocfilehash: 59db5535dd594476b1bf88af11c995082df580c9
ms.sourcegitcommit: f29360d62eb77b6ee875ce66483d5bc72785eede
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2020
ms.locfileid: "85111253"
---
# <a name="usb-h264-video-cameras-support"></a>USB h.264 ビデオカメラのサポート

Windows 8 以降では、h.264 ビデオコーデック (エンコーダー/デコーダー) がサポートされています。 コーデックは、高品質で解像度の高いビデオストリーミングを可能にするビデオデータをエンコードおよびデコードするためのアルゴリズムに基づいています。 Windows 8 UVC クラスドライバーでサポートされている機能の一部を次に示します (Usbvideo.sys)。

- H.264 ビデオカメラでサポートされている機能の検出。

- ビデオカメラの h.264 ストリームのセッションネゴシエーション。

- カメラからの h.264 ペイロードのストリーミング。

- H.264 ビデオカメラでサポートされている機能の検出。

H.264 コーデックは、効率的なビデオ圧縮を使用して、冗長なビデオデータを削減および削除します。 これにより、デジタルビデオファイルを効率的に保存し、ネットワーク経由で交換できます。

専用ドライバーではなく、UVC クラスドライバー Usbvideo.sys を使用する場合は、次に説明するガイドラインに従って、デバイスでビデオストリーミングファームウェアを実装する必要があります。

## <a name="firmware-guidelines"></a>ファームウェアのガイドライン

UVC クラスドライバーはビデオカメラを直接照会してその機能を取得し、専用のドライバーを必要とせずにデバイスをドライブに Usbvideo.sys します。 現在のガイドラインの実装については、「h.264/MPEG-2 のビデオクラスドライバーの仕様」を参照してください。 また、h.264[の USB ビデオクラスに対する Microsoft の提案](https://docs.microsoft.com/previous-versions/windows/hardware/download/dn550976(v=vs.85))された拡張機能についても参照してください。

> [!NOTE]
> 公式ガイドラインは、今後の標準ドキュメントで公開される予定です。[ビデオデバイス仕様のユニバーサルシリアルバスデバイスクラス定義に関する](https://www.usb.org/documents)記事をご覧ください。

## <a name="related-topics"></a>関連トピック

[**KS \_ DATAFORMAT \_ H264VIDEOINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_dataformat_h264videoinfo)  

[**KS \_ \_ datarange の \_ ビデオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_h264_video)  

[**KS \_ H264VIDEOINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_h264videoinfo)  
