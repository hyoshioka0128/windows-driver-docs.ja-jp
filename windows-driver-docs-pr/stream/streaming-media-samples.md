---
title: ストリーミング メディアのサンプル
description: ストリーミングメディアのサンプル
ms.assetid: 797763a6-cd13-4d76-8ddb-75d812a8dde3
keywords:
- ストリーミングメディアのサンプル WDK
- WDK ストリーミングメディアのサンプル
ms.date: 06/19/2020
ms.localizationpriority: medium
ms.openlocfilehash: c98e214980d759df2ca59c2ed5fcc6f1d8263edc
ms.sourcegitcommit: f29360d62eb77b6ee875ce66483d5bc72785eede
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2020
ms.locfileid: "85111250"
---
# <a name="streaming-media-samples"></a>ストリーミングメディアのサンプル

[Microsoft サンプル ポータル](https://docs.microsoft.com/samples/browse/?products=windows-wdk)では、個々の Windows 10 ドライバーのサンプルを参照してダウンロードできます。 また、GitHub の [Windows-driver-samples](https://github.com/Microsoft/Windows-driver-samples) リポジトリを複製、フォーク、またはダウンロードすることもできます。

以前のバージョンの Windows ドライバー サンプルは、次の場所にアーカイブされています。

- [Windows 8.1 ドライバー サンプル](https://github.com/microsoftarchive/msdn-code-gallery-microsoft/tree/master/Official%20Windows%20Driver%20Kit%20Sample/Windows%20Driver%20Kit%20(WDK)%208.1%20Samples)

- [Windows 8 ドライバー サンプル](https://github.com/microsoftarchive/msdn-code-gallery-microsoft/tree/master/Official%20Windows%20Driver%20Kit%20Sample/Windows%20Driver%20Kit%20(WDK)%208.0%20Samples)

Windows 7 の場合、サンプルは[Windows Driver Kit (WDK) 7 ダウンロード](https://www.microsoft.com/download/details.aspx?id=11800)に含まれています。

| サンプル名 | ビルド環境 | ターゲットオペレーティングシステム | PnP ドライバー | インボックスドライバー | サンプルの説明 |
|--|--|--|--|--|--|
| AVStream フィルター中心のシミュレートされたキャプチャドライバー (Avssamp) | Windows 8.1<br><br>Windows 8<br><br>Windows 7 | Windows 8.1<br><br>Windows 8<br><br>Windows 7 | いいえ | いいえ | フィルター中心の AVStream キャプチャドライバーを機能オーディオと共に提供します。 このドライバーは、ループ内でユーザーが指定したパルスコード変調 (PCM) wave オーディオファイルの再生中に、RGB24 または YUV422 形式の 320 x 240 解像度でキャプチャを実行します。 このサンプルでは、フィルター中心の AVStream ミニドライバーを記述する方法を示します。 |
| AVStream のシミュレートされたハードウェアサンプルドライバー (Avshws) |Windows 8.1<br><br>Windows 8<br><br>Windows 7 | Windows 8.1<br><br>Windows 8<br><br>Windows 7| いいえ | いいえ | シミュレートされたハードウェアのための、ピン中心の AVStream キャプチャドライバーを提供します。 ドライバーは、直接 DMA によってキャプチャバッファーに RGB24 または YUV422 形式で 240 320 キャプチャを実行します。<br><br>このサンプルの目的は、ピン中心の AVStream ミニドライバーを記述する方法を示すことです。 このサンプルでは、AVStream が提供する関連機能を使用して、DMA を実装する方法も示しています。<br><br>このサンプルでは、強化されたパラメーターの検証とオーバーフロー検出を行います。 |
| SonyDCam 1394 Webcam Driver | Windows 7 | Windows 7 | いいえ | はい | 1394貿易アソシエーションからのデジタルカメラ仕様に準拠した1394ベースのデジタルカメラをサポートする、Microsoft Windows Driver Model (WDM) ストリームクラスのビデオキャプチャドライバー。 |
| USBIntel Webcam Driver | Windows 7 | Windows 7 | いいえ | はい | Microsoft Windows Driver Model (WDM) ストリームクラスのビデオキャプチャドライバー。 |
| SW チューナー | Windows 7 | Windows 7 | いいえ | いいえ | 複数のデジタルネットワークの種類を示します。 |
