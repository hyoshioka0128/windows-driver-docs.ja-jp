---
title: モニター クラスの関数のドライバー
description: モニター クラスの関数のドライバー
ms.assetid: d16c3dcc-2fbf-4579-8962-1b89e6e7b347
keywords:
- 複数のモニター WDK
- 関数のクラス ドライバー WDK を監視します。
- 関数のドライバー WDK モニター
- デバイス スタック WDK を監視します。
- デバイス スタックの WDK モニター
- 物理デバイス オブジェクトの WDK モニター
- 機能のデバイス オブジェクトの WDK モニター
- Pdo WDK モニター
- Fdo WDK モニター
- DOs WDK モニターをフィルター処理します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a46c032183e55f26c665f3e3bd40c2e6553e55a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553706"
---
# <a name="monitor-class-function-driver"></a>モニター クラスの関数のドライバー


## <span id="ddk_monitor_class_function_driver_gg"></span><span id="DDK_MONITOR_CLASS_FUNCTION_DRIVER_GG"></span>


各ビデオの出力に接続されているモニター ディスプレイ アダプターでは、ディスプレイ アダプターの [デバイス] ノードの子である [デバイス] ノードで表されます。

通常、デバイス スタックでデバイス オブジェクトを表す 2 つだけが (ビデオ出力、モニター) ペア: 物理デバイス オブジェクト (PDO) と機能のデバイス オブジェクト (FDO)。 場合によってでは、fdo のベンダーから提供されたフィルター ドライバーに関連付けられているフィルターがあります。 統合モニターは、ラップトップ コンピューターでは、組み込みのフラット パネルなど、フィルターは、Advanced Configuration and Power Interface (ACPI) ドライバーの PDO の上に関連付けられている可能性があります。

次の表には、接続されているモニターを含むビデオの出力デバイス スタックが表示されます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">デバイス オブジェクト</th>
<th align="left">必須/オプション</th>
<th align="left">Driver (ドライバー)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>操作をフィルター処理します。</p></td>
<td align="left"><p>省略可能で、通常は必要ありません。</p></td>
<td align="left"><p>モニターのベンダーから提供されたドライバーをフィルター処理します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FDO</p></td>
<td align="left"><p>必須</p></td>
<td align="left"><p>Microsoft から提供される関数クラス ドライバー (Monitor.sys) の監視します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>操作をフィルター処理します。</p></td>
<td align="left"><p>統合の ACPI 表示パネルのみ必要です。</p></td>
<td align="left"><p>Microsoft から提供される ACPI ドライバー (Acpi.sys)</p></td>
</tr>
<tr class="even">
<td align="left"><p>PDO</p></td>
<td align="left"><p>必須</p></td>
<td align="left"><p>ディスプレイ アダプターの製造元によって提供されるバス ドライバー (表示ミニポート/ポート ペア)</p></td>
</tr>
</tbody>
</table>

 

ユーザー モード アプリケーションでは、WMI を使用して、監視クラスの関数のドライバーのサービスを呼び出します。 これらのサービスには、モニターの id データを公開することが含まれます (ACPI ディスプレイの場合) の場合、ディスプレイの明るさを設定します。

モニターの識別と機能の情報構造体に格納拡張表示 Identification Data (EDID)、その id、および通信の独立した機能に関する情報を持つホストを指定する、表示できる形式モニターとホスト間で使用されるプロトコル。 デバイス スタックを監視するモニターのディスプレイが EDID が関数のドライバー (Monitor.sys) によって処理されるを読み取るように、ユーザー モード アプリケーションからの要求。 モニター関数のドライバーでは、モニターのディスプレイが EDID を取得する要求を受信したときに、モニターのデバイス スタックの一番下にある物理デバイス オブジェクト (PDO) で表される表示ポート/ミニポート ドライバーのペアを要求を送信します。 ディスプレイ ポート/ミニポート ドライバーのペアでは、表示データ チャネル (DDC) プロトコルを使用してすべての標準的なモニター ケーブルに組み込まれている単純な 2 つのネットワーク バスは I²C バス経由で、モニターのディスプレイが EDID を読み取ります。

EDID を使用して取得できます、 [ACPI_METHOD_OUTPUT_DDC](https://docs.microsoft.com/windows-hardware/drivers/bringup/other-acpi-namespace-objects)メソッドでその別名が定義されている[Dispmprt.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/)します。 このメソッドは、統合の Lcd EDID データを返すためのもう 1 つの標準メカニズムがない必要があります。

ディスプレイ アダプターとモニターの間の通信の詳細については、次のトピックを参照してください。

[I2C バスとディスプレイ アダプターの子デバイス](i2c-bus-and-child-devices-of-the-display-adapter.md)

EDID 構造体と DDC プロトコルに関する詳細については、次のビデオ Electronics Standards アソシエーション (VESA) によって発行された標準を参照してください。

-   表示データ チャネルの強化された標準 (E DDC)

-   強化された EDID 標準 (E EDID)

これらの基準をダウンロードする[vesa.org](https://vesa.org/vesa-standards/)で、*無料標準*セクション。

詳細については、I²C バスは、次を参照してください。、 [I²C Bus 仕様](https://www.i2c-bus.org/specification/)Philips 半導体によって発行されました。

 

 





