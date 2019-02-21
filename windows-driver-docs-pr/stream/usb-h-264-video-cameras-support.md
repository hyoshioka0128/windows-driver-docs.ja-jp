---
title: USB H.264 ビデオをカメラのサポート
description: Windows 8 以降、H.264 ビデオ コーデック (エンコーダー/デコーダー) はサポートされています。
ms.assetid: EB73E2B2-B34E-4DC1-807A-4990A54E6E8D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1aa183949986475444c3cded4944b598d231c40f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531561"
---
# <a name="usb-h264-video-cameras-support"></a>USB H.264 ビデオをカメラのサポート


Windows 8 以降、H.264 ビデオ コーデック (エンコーダー/デコーダー) はサポートされています。 コーデックは、エンコードおよびデコードのビデオ データを高品質で高解像度ビデオのストリーミングを可能にするためのアルゴリズムに基づいています。 Windows 8 UVC クラス ドライバー、Usbvideo.sys、既定でサポートされる機能の一部を次に示します。

-   H.264 のビデオ_カメラでサポートされる機能の検出。
-   ビデオ_カメラでストリームを H.264 のセッションのネゴシエーション。
-   カメラからストリーミング H.264 ペイロード。
-   H.264 のビデオ_カメラでサポートされる機能の検出。

H.264 コーデックを減らし、冗長なビデオ データを削除する、効率的なビデオの圧縮を使用します。 デジタルのビデオ ファイルを効率的に格納し、ネットワーク経由で交換可能になります。

UVC クラス ドライバー Usbvideo.sys と独自のドライバーではなくを使用する場合は、次に説明されているガイドラインに従って、デバイスでストリーミング ビデオのファームウェアを実装する必要があります。

### <a name="firmware-guidelines"></a>ファームウェアのガイドライン

Usbvideo.sys UVC クラス ドライバーは、その機能を取得するには、直接ビデオ_カメラを照会し、必要な独自のドライバーで、デバイスをドライブします。 現在の実装のガイドラインについては、H.264/mpeg-4 のビデオ クラス ドライバーの Microsoft 仕様に参照する必要があります。 参照することも、 [H.264 の USB ビデオ クラスに提案された拡張機能の Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=233063)します。

**注**  にこの場所にある将来の標準的なドキュメントで、公式のガイドラインは公開されます。[ビデオ デバイスの仕様のデバイス クラス定義はユニバーサル シリアル バス](https://go.microsoft.com/fwlink/p/?linkid=516989)します。

 

## <a name="related-topics"></a>関連トピック
[**KS\_DATAFORMAT\_H264VIDEOINFO**](https://msdn.microsoft.com/library/windows/hardware/hh463996)  
[**KS\_DATARANGE\_H264\_ビデオ**](https://msdn.microsoft.com/library/windows/hardware/hh464002)  
[**KS\_H264VIDEOINFO**](https://msdn.microsoft.com/library/windows/hardware/hh464008)  



