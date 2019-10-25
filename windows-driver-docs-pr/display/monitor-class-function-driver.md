---
title: モニター クラスの関数ドライバー
description: モニター クラスの関数ドライバー
ms.assetid: d16c3dcc-2fbf-4579-8962-1b89e6e7b347
keywords:
- 複数のモニター (WDK)
- クラス関数ドライバー WDK の監視
- 関数ドライバー WDK モニター
- デバイススタックの監視 WDK
- デバイススタック WDK モニター
- 物理デバイスオブジェクト WDK モニタ
- 機能デバイスオブジェクト WDK モニター
- PDOs WDK モニター
- FDOs WDK モニター
- DOs WDK モニターをフィルター処理する
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e46a9ade660ea960ef7c447b6ee8dbbba321906
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840558"
---
# <a name="monitor-class-function-driver"></a>モニター クラスの関数ドライバー


## <span id="ddk_monitor_class_function_driver_gg"></span><span id="DDK_MONITOR_CLASS_FUNCTION_DRIVER_GG"></span>


モニターが接続されているディスプレイアダプターの各ビデオ出力は、ディスプレイアダプターのデバイスノードの子であるデバイスノードによって表されます。

通常、デバイススタックには、(ビデオ出力、モニター) ペアを表すデバイスオブジェクトが2つだけあります。これは、物理デバイスオブジェクト (PDO) と機能デバイスオブジェクト (FDO) です。 場合によっては、ベンダーから提供されたフィルタードライバーに関連付けられたフィルターが FDO の上にあることがあります。 ラップトップコンピューターの内蔵フラットパネルなど、統合されたモニターの場合、PDO の上位の Advanced Configuration and Power Interface (ACPI) ドライバーに関連付けられているフィルターが存在する可能性があります。

次の表は、モニターが接続されているビデオ出力のデバイススタックを示しています。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">デバイスオブジェクト</th>
<th align="left">必須/オプション</th>
<th align="left">[ドライバー]</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>フィルター処理</p></td>
<td align="left"><p>省略可能。通常は必要ありません</p></td>
<td align="left"><p>モニタベンダーによって提供されるフィルタドライバ</p></td>
</tr>
<tr class="even">
<td align="left"><p>FDO</p></td>
<td align="left"><p>必須かどうか</p></td>
<td align="left"><p>Microsoft によって提供されるクラス関数ドライバー (.sys) を監視します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>フィルター処理</p></td>
<td align="left"><p>統合された ACPI ディスプレイパネルにのみ必要</p></td>
<td align="left"><p>Microsoft によって提供される ACPI ドライバー (Acpi)</p></td>
</tr>
<tr class="even">
<td align="left"><p>PDO</p></td>
<td align="left"><p>必須かどうか</p></td>
<td align="left"><p>ディスプレイアダプターベンダーによって指定されたバスドライバー (ミニポートとポートのペアの表示)</p></td>
</tr>
</tbody>
</table>

 

ユーザーモードのアプリケーションは、WMI を使用して、monitor クラスの関数ドライバーのサービスを呼び出します。 これらのサービスには、モニターの識別データの公開、(ACPI ディスプレイの場合) ディスプレイの明るさの設定などが含まれます。

モニターは、id と機能に関する情報を、拡張された表示識別データ (EDID) 構造で格納します。この形式は、通信に依存しない id と機能についての情報を表示するように指定します。モニタとホストの間で使用されるプロトコル。 ユーザーモードアプリケーションからモニターの EDID を読み取る要求は、そのモニターのデバイススタックの関数ドライバー (.sys) によって処理されます。 Monitor 関数ドライバーは、モニターの EDID を取得する要求を受信すると、モニターのデバイススタックの一番下にある物理デバイスオブジェクト (PDO) によって表されるディスプレイポート/ミニポートドライバーのペアに要求を送信します。 ディスプレイポート/ミニポートドライバーのペアは、ディスプレイデータチャネル (DDC) プロトコルを使用して I ² C バス上でモニターの EDID を読み取ります。これは、すべての標準モニタケーブルに組み込まれている単純な2ワイヤバスです。

EDID は、 [ACPI_METHOD_OUTPUT_DDC](https://docs.microsoft.com/windows-hardware/drivers/bringup/other-acpi-namespace-objects)メソッドを使用して取得できます。このメソッドには、エイリアスが定義されてい[ます。](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/) このメソッドは、EDID データを返すための別の標準メカニズムがない統合 Lcd に必要です。

ディスプレイアダプターとモニター間の通信の詳細については、次のトピックを参照してください。

[ディスプレイアダプターの I2C バスおよび子デバイス](i2c-bus-and-child-devices-of-the-display-adapter.md)

EDID 構造と DDC プロトコルの詳細については、ビデオエレクトロニクス標準の関連付け (VESA) によって発行された次の標準を参照してください。

-   Enhanced Display Data Channel Standard (E-DDC)

-   Enhanced EDID Standard (E EDID)

これらの標準は、「 *Free 標準*」セクションの[vesa.org](https://vesa.org/vesa-standards/)からダウンロードできます。

I ² C バスの詳細については、「[私² c バス仕様](https://www.i2c-bus.org/specification/)」を参照してください。

 

 





