---
title: ストリーミング メディアのサンプル
description: ストリーミング メディアのサンプル
ms.assetid: 797763a6-cd13-4d76-8ddb-75d812a8dde3
keywords:
- ストリーミングメディアのサンプル WDK
- WDK ストリーミングメディアのサンプル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 882211ebd73768a158ec13fe910798d1568ca184
ms.sourcegitcommit: 44f09d983954f27fd90b737a2dd142aad7dffd9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2019
ms.locfileid: "70059170"
---
# <a name="streaming-media-samples"></a>ストリーミング メディアのサンプル

[Microsoft サンプルポータル](https://docs.microsoft.com/samples/browse/?products=windows-wdk)では、個々の Windows 10 ドライバーのサンプルを参照してダウンロードできます。 GitHub で[Windows ドライバーのサンプル](https://github.com/Microsoft/Windows-driver-samples)リポジトリを複製、フォーク、またはダウンロードすることもできます。

以前のバージョンの Windows ドライバーサンプルは、次の場所にアーカイブされています。

- [Windows 8.1 ドライバーのサンプル](https://go.microsoft.com/fwlink/p/?LinkId=618052)

- [Windows 8 ドライバーのサンプル](https://go.microsoft.com/fwlink/p/?LinkId=616509)

Windows 7 では、サンプルは Windows Driver Kit (WDK) に含まれていました。

<table style="width:100%;">
<colgroup>
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th>サンプル名</th>
<th>ビルド環境</th>
<th>ターゲットオペレーティングシステム</th>
<th>PnP ドライバー</th>
<th>インボックスドライバー</th>
<th>サンプルの説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AVStream フィルター中心のシミュレートされたキャプチャドライバー (Avssamp)</p></td>
<td><p>Windows 8.1</p>
<p>Windows 8</p>
<p>Windows 7</p></td>
<td><p>Windows 8.1</p>
<p>Windows 8</p>
<p>Windows 7</p></td>
<td><p>いいえ</p></td>
<td><p>いいえ</p></td>
<td><p>フィルター中心の AVStream キャプチャドライバーを機能オーディオと共に提供します。 このドライバーは、ループ内でユーザーが指定したパルスコード変調 (PCM) wave オーディオファイルの再生中に、RGB24 または YUV422 形式の 320 x 240 解像度でキャプチャを実行します。 このサンプルでは、フィルター中心の AVStream ミニドライバーを記述する方法を示します。</p></td>
</tr>
<tr class="even">
<td><p>AVStream のシミュレートされたハードウェアサンプルドライバー (Avshws)</p></td>
<td><p>Windows 8.1</p>
<p>Windows 8</p>
<p>Windows 7</p></td>
<td><p>Windows 8.1</p>
<p>Windows 8</p>
<p>Windows 7</p></td>
<td><p>いいえ</p></td>
<td><p>いいえ</p></td>
<td><p>シミュレートされたハードウェアのための、ピン中心の AVStream キャプチャドライバーを提供します。 ドライバーは、直接 DMA によってキャプチャバッファーに RGB24 または YUV422 形式で 240 320 キャプチャを実行します。</p>
<p>このサンプルの目的は、ピン中心の AVStream ミニドライバーを記述する方法を示すことです。 このサンプルでは、AVStream が提供する関連機能を使用して、DMA を実装する方法も示しています。</p>
<p>このサンプルでは、強化されたパラメーターの検証とオーバーフロー検出を行います。</p></td>
</tr>
<tr class="odd">
<td><p>SonyDCam 1394 Webcam Driver</p></td>
<td><p>Windows 7</p></td>
<td><p>Windows 7</p></td>
<td><p>いいえ</p></td>
<td><p>はい</p></td>
<td><p>1394貿易アソシエーションからのデジタルカメラ仕様に準拠した1394ベースのデジタルカメラをサポートする、Microsoft Windows Driver Model (WDM) ストリームクラスのビデオキャプチャドライバー。</p></td>
</tr>
<tr class="even">
<td><p>USBIntel Webcam Driver</p></td>
<td><p>Windows 7</p></td>
<td><p>Windows 7</p></td>
<td><p>いいえ</p></td>
<td><p>はい</p></td>
<td><p>Microsoft Windows Driver Model (WDM) ストリームクラスのビデオキャプチャドライバー。</p></td>
</tr>
<tr class="odd">
<td><p>SW チューナー</p></td>
<td><p>Windows 7</p></td>
<td><p>Windows 7</p></td>
<td><p>いいえ</p></td>
<td><p>いいえ</p></td>
<td><p>複数のデジタルネットワークの種類を示します。</p></td>
</tr>
</tbody>
</table>

 

 

 




