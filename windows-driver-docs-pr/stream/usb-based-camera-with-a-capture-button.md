---
title: キャプチャ ボタン付きの USB ベース カメラ
description: キャプチャ ボタン付きの USB ベース カメラ
ms.assetid: abbd824c-1ade-4dbc-8807-e558c444a3ea
keywords:
- フィルター グラフ構成 WDK ビデオ キャプチャには、USB ベースのカメラ キャプチャ ボタン
- ピン WDK ビデオ キャプチャします。
- WDK AVStream のキャプチャ ボタン
- USB ベースのカメラ ボタン WDK ビデオ キャプチャをキャプチャします。
- まだイメージ WDK ビデオ キャプチャのキャプチャ
- WDK のビデオ キャプチャ静止画像
- カメラの WDK ビデオのキャプチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b17b5a84e77abc3f92ce0bb3dcc1cdcd332a2dc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377726"
---
# <a name="usb-based-camera-with-a-capture-button"></a>キャプチャ ボタン付きの USB ベース カメラ


比較すると、少し複雑なフィルター グラフを[USB またはベース 1394 会議カメラ](usb-or-1394-based-conferencing-camera.md)ミニドライバーが静止画像をキャプチャするためのボタンをサポートするもの pin を公開する会議カメラが作成されます。 まだ暗証番号 (pin) は、ユーザー、カメラの電源ボタンをプッシュするときより高い解像度のイメージを提供できます。

ベンダーは、UVC 仕様に準拠している場合、ミニドライバーは、USB ベースのカメラを記述する必要はありません。 Microsoft が提供、 [USB ビデオ クラス ドライバー](usb-video-class-driver.md)のような cameras します。 マイクロソフトでは、新しい USB ベース会議カメラ ハードウェアが UVC 仕様に準拠して開発することをお勧めします。

Microsoft も用意されています。、 [USBCAMD ミニドライバー ライブラリ](usbcamd-minidriver-library.md)旧バージョンとの互換性のためです。 USBCAMD に引き続きピン カメラがサポートされています。 ただし、USBCAMD インターフェイスは廃止されていますと Microsoft がさらに、開発廃止されました。

次の図は、まだ pin と USB ベースのカメラの使用可能なフィルター グラフ構成を示します。

![まだ pin と usb ベースのカメラの使用可能なフィルター グラフ構成を示す図](images/usb-camera-still.gif)

図では、ユーザー、カメラの電源ボタンをプッシュするときに、静止 pin は 1 つのイメージのみをストリームします。 または、プログラムによる制御によってまだ暗証番号 (pin) をトリガーできます。

Windows Image Acquisition (WIA) テクノロジーで、まだイメージのアーキテクチャ (STI) は、USBCAMD によって提供される機能を補完します。 参照してください[Windows Image Acquisition ドライバー](https://docs.microsoft.com/windows-hardware/drivers/image/windows-image-acquisition-drivers)と[イメージ ドライバーも](https://docs.microsoft.com/windows-hardware/drivers/image/still-image-drivers)詳細についてはします。

WIA ビデオ スナップショット フィルターは、Microsoft Windows XP 以降のオペレーティング システムに付属する WIA の追加です。 WIA ビデオ スナップショット フィルターは引き続き、ビデオ ストリームからキャプチャするフレームを使用します。

デバイスからまだイメージのキャプチャの 2 つの方法はあります。 最初は、キャプチャ フィルターから下流にある、WIA ビデオ スナップショット フィルターを挿入し、プログラムによるキャプチャをトリガーします。 2 番目、ミニドライバーを開発する USBCAMD インターフェイスを使用して引き続き pin のサポートを有効にすることです。 WIA ビデオ スナップショット フィルターは、デバイス上のボタンを押すことによってトリガーできます。

ビデオ ストリームではなく静止暗証番号 (pin) からイメージのキャプチャの利点には、静止暗証番号 (pin) がより高い解像度のイメージを提供し、デバイスのボタンをクリックしてイメージをキャプチャするユーザーを許可できます。

まだ pin のサポートはされていないようにミニドライバーに明示的に追加、WIA ビデオ スナップショット フィルターは、ソフトウェアによって発生する可能性しますが、解像度には、ビデオ ストリームと同じになります。

いくつかはまだピン留めするキャプチャ暗証番号 (pin) のデータ形式に基づいているために、実装をキャプチャの暗証番号 (pin) の後にレンダリングだけことができます。

WIA ドライバーの開発の詳細については、次を参照してください。、[静止テクノロジをイメージング](https://go.microsoft.com/fwlink/p/?linkid=8768)web サイト。

 

 




