---
title: キャプチャ ボタン付きの USB ベース カメラ
description: '[キャプチャ] ボタンがある USB ベースのカメラ'
ms.assetid: abbd824c-1ade-4dbc-8807-e558c444a3ea
keywords:
- フィルターグラフ構成 WDK ビデオキャプチャ、キャプチャボタンを使用した USB ベースのカメラ
- 引き続き WDK のビデオキャプチャをピン留めする
- キャプチャボタン WDK AVStream
- キャプチャボタンを使用した USB ベースのカメラ (WDK ビデオキャプチャ)
- 静止画像のキャプチャ WDK ビデオキャプチャ
- 依然として WDK ビデオキャプチャをキャプチャするイメージ
- カメラ WDK ビデオキャプチャ
ms.date: 06/19/2020
ms.localizationpriority: medium
ms.openlocfilehash: 242c379286aa594ead2387a849f4d8d8049fef69
ms.sourcegitcommit: f29360d62eb77b6ee875ce66483d5bc72785eede
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2020
ms.locfileid: "85111243"
---
# <a name="usb-based-camera-with-a-capture-button"></a>[キャプチャ] ボタンがある USB ベースのカメラ

[USB または1394ベースの会議カメラ](usb-or-1394-based-conferencing-camera.md)と比較して、やや複雑なフィルターグラフは、ミニドライバーが静止画像をキャプチャするボタンをサポートする静止 pin を公開する会議カメラ用に作成されます。 静止ピンは、ユーザーがカメラ上にボタンをプッシュしたときに、より高い解像度のイメージを提供できます。

製造元は、UVC 仕様に準拠している場合は、USB ベースのカメラのミニドライバーを作成する必要はありません。 Microsoft は、このようなカメラ用の[USB ビデオクラスドライバー](usb-video-class-driver.md)を提供しています。 Microsoft では、UVC 仕様に従って新しい USB ベースの電話会議カメラハードウェアを開発することをお勧めします。

Microsoft では、旧バージョンとの互換性のために[USBCAMD ミニドライバーライブラリ](usbcamd-minidriver-library.md)も提供しています。 USBCAMD は、まだ pin があるカメラをサポートしています。 ただし、USBCAMD インターフェイスは互換性のために残されていますが、マイクロソフトはさらに開発を中止しました。

次の図は、pin が静止している USB ベースのカメラに使用できるフィルターグラフの構成を示しています。

![pin が静止している usb ベースのカメラに使用できるフィルターグラフ構成を示す図](images/usb-camera-still.gif)

図では、ユーザーがカメラ上にボタンをプッシュしたときに、静止ピンが1つのイメージのみをストリームします。 または、プログラムによる制御によって、まだ pin をトリガーすることもできます。

静止画像アーキテクチャ (STI) 上に構築された Windows イメージ取得 (WIA) テクノロジは、USBCAMD によって提供される機能を補完します。 詳細については、「 [Windows イメージ取得ドライバー](https://docs.microsoft.com/windows-hardware/drivers/image/windows-image-acquisition-drivers) 」および「[イメージドライバー](https://docs.microsoft.com/windows-hardware/drivers/image/still-image-drivers) 」を参照してください。

WIA ビデオスナップショットフィルターは、Microsoft Windows XP 以降のオペレーティングシステムに付属している WIA に追加されたものです。 WIA ビデオスナップショットフィルターを使用すると、ビデオストリームからフレームをキャプチャできます。

デバイスから静止イメージをキャプチャする方法は2つあります。 1つ目は、キャプチャフィルターから下流にある WIA ビデオスナップショットフィルターを挿入し、プログラムによってキャプチャをトリガーすることです。 2つ目は、USBCAMD インターフェイスを使用してミニドライバーを開発することで、引き続き pin サポートを有効にすることです。 その後、デバイスにボタンを押すことによって、WIA ビデオスナップショットフィルターをトリガーできます。

ビデオストリームではなく静止ピンからイメージをキャプチャする利点は、静止ピンが解像度の高いイメージを提供し、ユーザーがデバイスのボタンを押してイメージをキャプチャできることです。

まだ pin のサポートがミニドライバーに明示的に追加されていない場合は、ソフトウェアによって WIA ビデオスナップショットフィルターがトリガーされますが、解像度はビデオストリームと同じになります。

静止ピンの一部の実装は、キャプチャピンのデータ形式に基づいているため、キャプチャピンの後でのみレンダリングできます。

WIA ドライバーの開発の詳細については、「[イメージングデバイスドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/image)」を参照してください。
