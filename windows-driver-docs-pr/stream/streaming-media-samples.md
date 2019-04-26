---
title: ストリーミング メディアのサンプル
description: ストリーミング メディアのサンプル
ms.assetid: 797763a6-cd13-4d76-8ddb-75d812a8dde3
keywords:
- ストリーミング メディア サンプル WDK
- ストリーミング メディアの WDK サンプル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f559224f9dcd5b2d2097eb01ab355bdf3fda4b72
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359632"
---
# <a name="streaming-media-samples"></a>ストリーミング メディアのサンプル


### <a href="" id="streaming-media-samples"></a>

Windows 10 以降、[Windows ドライバーのサンプル リポジトリ](https://go.microsoft.com/fwlink/p/?LinkId=616507)は GitHub で入手できます。

[Windows 8 ドライバー サンプル](https://go.microsoft.com/fwlink/p/?LinkId=616509)と[Windows 8.1 ドライバー サンプル](https://go.microsoft.com/fwlink/p/?LinkId=618052)からダウンロードできます、 [Windows ハードウェア デベロッパー センター](https://go.microsoft.com/fwlink/p/?LinkId=616506)します。

Windows 7 では、サンプルには、Windows Driver Kit (WDK) では含まれます。

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
<th>環境を構築します。</th>
<th>対象のオペレーティング システム</th>
<th>PnP ドライバー</th>
<th>インボックス ドライバー</th>
<th>サンプルの説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AVStream フィルター中心のシミュレートされたキャプチャ ドライバー (Avssamp)</p></td>
<td><p>Windows 8.1</p>
<p>Windows 8</p>
<p>Windows 7</p></td>
<td><p>Windows 8.1</p>
<p>Windows 8</p>
<p>Windows 7</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>オーディオの機能に関するフィルターを中心とした AVStream キャプチャ ドライバーを提供します。 ドライバーは、ユーザー指定のパルス コード変調 (PCM) wave オーディオ ファイルをループでの再生中に RGB24 または YUV422 形式で 320 x 240 解像度でキャプチャを実行します。 このサンプルでは、フィルターを中心とした AVStream ミニドライバーを記述する方法を示します。</p></td>
</tr>
<tr class="even">
<td><p>AVStream シミュレートされたハードウェア サンプル ドライバー (Avshws)</p></td>
<td><p>Windows 8.1</p>
<p>Windows 8</p>
<p>Windows 7</p></td>
<td><p>Windows 8.1</p>
<p>Windows 8</p>
<p>Windows 7</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>シミュレーションのハードウェアの暗証番号 (pin) を中心とした AVStream キャプチャ ドライバーを提供します。 ドライバーは、キャプチャ バッファーに直接 DMA 経由 RGB24 または YUV422 のいずれかの形式で 320 x 240 でキャプチャを実行します。</p>
<p>サンプルでは、暗証番号 (pin) を中心とした AVStream ミニドライバーを作成する方法について説明します。 このサンプルでは、AVStream の関連機能を使用して、DMA を実装する方法も示します。</p>
<p>このサンプルの機能には、パラメーターの検証とオーバーフローの検出が強化されています。</p></td>
</tr>
<tr class="odd">
<td><p>SonyDCam 1394 web カメラ ドライバー</p></td>
<td><p>Windows 7</p></td>
<td><p>Windows 7</p></td>
<td><p>X</p></td>
<td><p>〇</p></td>
<td><p>1394 貿易からデジタル カメラの仕様に準拠する 1394 に基づくデジタル カメラをサポートする Microsoft Windows Driver Model (WDM) Stream クラス ビデオ キャプチャ ドライバー。</p></td>
</tr>
<tr class="even">
<td><p>USBIntel web カメラ ドライバー</p></td>
<td><p>Windows 7</p></td>
<td><p>Windows 7</p></td>
<td><p>X</p></td>
<td><p>〇</p></td>
<td><p>Microsoft Windows Driver Model (WDM) ストリーム クラス ビデオ キャプチャ ドライバー。</p></td>
</tr>
<tr class="odd">
<td><p>SW チューナー</p></td>
<td><p>Windows 7</p></td>
<td><p>Windows 7</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>いくつかのデジタル ネットワークの種類を示します。</p></td>
</tr>
</tbody>
</table>

 

 

 




