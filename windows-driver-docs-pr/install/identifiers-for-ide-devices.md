---
title: IDE デバイスの識別子
description: IDE デバイスの識別子
ms.assetid: b1624eb9-afa7-49ce-9db1-b0eab466ddcd
keywords:
- デバイスの識別文字列 WDK、IDE デバイス
- 識別文字列の WDK デバイス、IDE デバイス
- 識別子の WDK デバイス、IDE デバイス
- IDE デバイス識別子 WDK デバイスのインストール
- デバイス Id の WDK デバイスのインストール
- ハードウェア Id の WDK デバイスのインストール
- 互換性のある Id WDK デバイスのインストール
- 統合デバイス electronics 識別子 WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91125da000488cbff6d15771b6ac700d2ac1c5ff
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335366"
---
# <a name="identifiers-for-ide-devices"></a>IDE デバイスの識別子





統合デバイス electronics (IDE) デバイスの識別子では、SCSI 識別子に似ています。 デバイス ID の形式は次のとおりです。

IDE\\t\*v(40)r(8)

各項目の意味は次のとおりです。

- *t\** 可変長のデバイスの種類のコードに示します。

- *v(40)* ベンダー名、アンダー スコア、ベンダーの製品名、および合計 40 文字にするための十分なアンダー スコアを格納した文字列です。

- *r(8)* は 8 文字のリビジョン番号です。

これには、デバイス ID だけでなく、3 つのハードウェア Id があります。

IDE\\v(40)r(8)

IDE\\t\*v(40)

V(40)r(8)

SCSI の場合と同様は、1 つだけの互換性のある ID、SCSI ポート ドライバーによって提供されるが、18 ではなくのみ 11 個のエントリを含む標準の SCSI 型名のようなジェネリック型名があります。 IDE デバイスの汎用的なデバイスの種類名は次のとおりです。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">IDE の種類のコード</th>
<th align="left">デバイスの種類</th>
<th align="left">ジェネリック型</th>
<th align="left">周辺機器の ID</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DIRECT_ACCESS_DEVICE (0)</p></td>
<td align="left"><p>Disk</p></td>
<td align="left"><p>GenDisk</p></td>
<td align="left"><p>DiskPeripheral</p></td>
</tr>
<tr class="even">
<td align="left"><p>SEQUENTIAL_ACCESS_DEVICE (1)</p></td>
<td align="left"><p>シーケンシャル</p></td>
<td align="left"><p>GenSequential</p></td>
<td align="left"><p>TapePeripheral</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PRINTER_DEVICE (2)</p></td>
<td align="left"><p>プリンター</p></td>
<td align="left"><p>GenPrinter</p></td>
<td align="left"><p>PrinterPeripheral</p></td>
</tr>
<tr class="even">
<td align="left"><p>PROCESSOR_DEVICE (3)</p></td>
<td align="left"><p>処理者</p></td>
<td align="left"><p>GenProcessor</p></td>
<td align="left"><p>OtherPeripheral</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WRITE_ONCE_READ_MULTIPLE_DEVICE (4)</p></td>
<td align="left"><p>ワーム</p></td>
<td align="left"><p>GenWorm</p></td>
<td align="left"><p>WormPeripheral</p></td>
</tr>
<tr class="even">
<td align="left"><p>READ_ONLY_DIRECT_ACCESS_DEVICE (5)</p></td>
<td align="left"><p>CdRom</p></td>
<td align="left"><p>GenCdRom</p></td>
<td align="left"><p>CdRomPeripheral</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SCANNER_DEVICE (6)</p></td>
<td align="left"><p>スキャナー</p></td>
<td align="left"><p>GenScanner</p></td>
<td align="left"><p>ScannerPeripheral</p></td>
</tr>
<tr class="even">
<td align="left"><p>OPTICAL_DEVICE (7)</p></td>
<td align="left"><p>光学式</p></td>
<td align="left"><p>GenOptical</p></td>
<td align="left"><p>OpticalDiskPeripheral</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MEDIUM_CHANGER (8)</p></td>
<td align="left"><p>チェンジャー</p></td>
<td align="left"><p>GenChanger</p></td>
<td align="left"><p>MediumChangerPeripheral</p></td>
</tr>
<tr class="even">
<td align="left"><p>COMMUNICATION_DEVICE (9)</p></td>
<td align="left"><p>Net</p></td>
<td align="left"><p>GenNet</p></td>
<td align="left"><p>CommunicationsPeripheral</p></td>
</tr>
<tr class="odd">
<td align="left"><p>10</p></td>
<td align="left"><p>その他</p></td>
<td align="left"><p>GenOther</p></td>
<td align="left"><p>OtherPeripheral</p></td>
</tr>
</tbody>
</table>

 

チェンジャーの IDE デバイスのジェネリック型の名前は**GenChanger**の代わりに**ScsiChanger**通信デバイス、ジェネリック型の名前は、 **GenNet** ではなく**ScsiNet**します。 SCSI ポート ドライバーには順次アクセスと「プロセッサ」のデバイスのすべての汎用名を返しますなし、IDE バス ドライバーを返しますが、 **GenSequential**と**GenProcessor**します。 また、IDE バス ドライバーは、SCSI ポート ドライバーは現在 18 を返しますが、10 個のジェネリック型を返します。 その他の点では、IDE バス ドライバーによって返される一般的な名前は、SCSI ポート ドライバーによって返されるものと同じです。

IDE のテープ ドライブの互換性のある ID は次のとおりです。

GenSequential

%.*ls 120 デバイスの特殊な場合は、IDE バス ドライバーは、次の互換性のある ID を返します。

GenSFloppy

IDE ハード ディスク ドライブを生成できる識別子の種類を次に示します。

IDE\\DiskMaxtor_91000D8___SASX1B18

IDE\\Maxtor_91000D8___SASX1B18

IDE\\DiskMaxtor_91000D8___

Maxtor_91000D8__________________________SASX1B18

GenDisk

 

 





