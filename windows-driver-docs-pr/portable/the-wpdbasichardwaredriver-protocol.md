---
Description: The WpdBasicHardwareDriver Protocol
title: WpdBasicHardwareDriver プロトコル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a53dc95edb3b90acd1a56727ac6fdd2ac19ae24
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570807"
---
# <a name="the-wpdbasichardwaredriver-protocol"></a>WpdBasicHardwareDriver プロトコル


WpdBasicHardwareDriver サンプル ドライバーでは、デバイス id、パケット サイズ、およびセンサー データを含む単純なプロトコルをサポートします。 プロトコルは、プログラミング可能なマイクロ コント ローラーによって送信され、サンプル ドライバーによって受信されるセンサー データの基本的なデータ形式を定義します。 ドライバーのサンプルでは、データ パケットを解析し、WPD アプリケーションによって受信されたカスタムの WPD イベントに変換します。

デバイスとドライバーのサンプルをインストールした後は、Windows Driver Kit (WDK) に付属している WpdMon ツールを使用してこのデータのパケットを表示できます。 このツールは、WPD ドライバーと WPD API 間のトラフィック (WPD コマンドとイベント) を監視します。 次のスクリーン ショットには、カスタム WPD イベントとして、ドライバーから API に送信される、Sensiron 温度と湿度センサーのセンサー データが表示されます。 WpdBasicHardwareDriver によって GUID が定義されているカスタム イベント*Stdafx.h*します。

```ManagedCPlusPlus
DEFINE_GUID (EVENT_SENSOR_READING_UPDATED, 0xada23b0b, 0xce13, 0x4e11, 0x9d, 0x2f, 0x15, 0xfe, 0x10, 0xd6, 0x63, 0x37);
```

![wpd モニター](images/wpdmon.png)

**注**  、センサー\_読み取りとセンサー\_UPDATE\_間隔イベント パラメーターが WPD スキーマの一部ではないです。 次のエントリを追加する WpdInfo プロパティ ファイルを編集する必要があります。 (これらのエントリが追加されていない場合 WpdMon および WpdInfo ツールは、表示されるフレンドリ名ではなく生 PROPERTYKEYs。

 

```cpp
{a7ef4367-6550-4055-b66f-be6fdacf4e9f}.2, SENSOR_READING, VT_UI8
{a7ef4367-6550-4055-b66f-be6fdacf4e9f}.3, SENSOR_UPDATE_INTERVAL, VT_UI4
```

前の画像では、センサーで\_読み取り行には WPD API へのドライバーを使用して、センサーから送信されるデータが含まれています。 このデータは、マルチバイト パケット形式は次の図に表示されるのです。

![センサーのパケット](images/sensiron_packetvsd.png)

最初のバイトは、センサーを識別する、2 番目の要素数を指定します、3 番目の要素のサイズを指定します、(第 4 + count) から 4 番目のバイト数が、実際のデータ要素を含めることがおよび最後の 6 バイト間隔を指定する、センサーコンピューターには、そのデータを発行します。

要素のデータの 7 つのバイト数を現在の気温が華氏の 72.6 と相対湿度が 32.8% を示します。 データ間隔の 5 つのバイトは、センサーが 2,000 ミリ秒ごと (または、2 秒ごと) に、コンピューターにデータを転送することを示します。

次の表は、視差センサー サンプル キット内にある 9 つのセンサーのパケットの書式を指定します。

<table>
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
<th align="left">センサー</th>
<th align="left">センサー ID</th>
<th align="left">要素の数</th>
<th align="left">要素のサイズ</th>
<th align="left">要素</th>
<th align="left">間隔</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Compass</td>
<td align="left">1</td>
<td align="left">1</td>
<td align="left">3</td>
<td align="left">見出し (3 バイト)</td>
<td align="left">6 バイト</td>
</tr>
<tr class="even">
<td align="left">Sensiron</td>
<td align="left">2</td>
<td align="left">1</td>
<td align="left">7</td>
<td align="left">Temp (4 バイト)
<p>湿度 (3 バイト)</p></td>
<td align="left">6 バイト</td>
</tr>
<tr class="odd">
<td align="left">フレックス Force</td>
<td align="left">3</td>
<td align="left">1</td>
<td align="left">5</td>
<td align="left">強制 (5 バイト)</td>
<td align="left">6 バイト</td>
</tr>
<tr class="even">
<td align="left">Ultrasonic Ping</td>
<td align="left">4</td>
<td align="left">1</td>
<td align="left">5</td>
<td align="left">距離 (5 バイト)</td>
<td align="left">6 バイト</td>
</tr>
<tr class="odd">
<td align="left">パッシブ赤外線</td>
<td align="left">5</td>
<td align="left">1</td>
<td align="left">1</td>
<td align="left">状態 (1 バイト)</td>
<td align="left">6 バイト</td>
</tr>
<tr class="even">
<td align="left">Memsic</td>
<td align="left">6</td>
<td align="left">1</td>
<td align="left">8</td>
<td align="left">x 軸 G (4 バイト)
<p>y 軸 G (4 バイト)</p></td>
<td align="left">6 バイト</td>
</tr>
<tr class="odd">
<td align="left">QTI</td>
<td align="left">7</td>
<td align="left">1</td>
<td align="left">4</td>
<td align="left">ライトの測定 (4 バイト)</td>
<td align="left">6 バイト</td>
</tr>
<tr class="even">
<td align="left">Piezo 振動</td>
<td align="left">8</td>
<td align="left">1</td>
<td align="left">1</td>
<td align="left">状態 (1 バイト)</td>
<td align="left">6 バイト</td>
</tr>
<tr class="odd">
<td align="left">日立</td>
<td align="left">9</td>
<td align="left">3</td>
<td align="left">4</td>
<td align="left">x 軸 G (4 バイト)
<p>y 軸 G (4 バイト)</p>
<p>z 軸 G (4 バイト)</p></td>
<td align="left">6 バイト</td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD ドライバーのサンプル](the-wpd-driver-samples.md)

 

 





