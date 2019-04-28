---
title: SCSI デバイスの識別子
description: SCSI デバイスの識別子
ms.assetid: 8bc68813-5096-40b2-bbd1-0aebb5a3326d
keywords:
- デバイスの識別文字列 WDK、SCSI デバイス
- SCSI デバイスの識別文字列 WDK デバイス
- 識別子の WDK デバイス、SCSI デバイス
- SCSI デバイス識別子 WDK デバイスのインストール
- デバイス Id の WDK デバイスのインストール
- ハードウェア Id の WDK デバイスのインストール
- 互換性のある Id WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 917a542f60f67beb473cadc340232a481da0c3ad
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362994"
---
# <a name="identifiers-for-scsi-devices"></a>SCSI デバイスの識別子





小規模なコンピューター システムの scsi デバイスのデバイス ID の形式は次のとおりです。

SCSI\\t\*v(8)p(16)r(4)

各項目の意味は次のとおりです。

- *t\** 可変長のデバイスの種類のコードに示します。

- *v(8)* 8 文字の仕入先識別子です。

- *p(16)* は 16 文字のプロダクトの識別子です。

- *r(4)* は 4 文字のリビジョン レベル値です。

Bus 列挙子は、次の表に示すように、デバイスを照会して取得した、数字でエンコードされた SCSI デバイスの種類コードを使用する、内部文字列テーブルのインデックスを作成して、デバイスの種類を決定します。 残りのコンポーネントは、特殊文字 (スペース、コンマ、および印刷されない任意のグラフィックを含む)、アンダー スコアに置き換えられますが、デバイスによって返される文字列にすぎません。

SCSI ポート ドライバー現在文字列を返します、次のデバイスの種類、うちの最初の 9 が標準の SCSI 型コードに対応しています。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SCSI 型コード</th>
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
<td align="left"></td>
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
<td align="left"></td>
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
<td align="left"><p>ScsiChanger</p></td>
<td align="left"><p>MediumChangerPeripheral</p></td>
</tr>
<tr class="even">
<td align="left"><p>COMMUNICATION_DEVICE (9)</p></td>
<td align="left"><p>Net</p></td>
<td align="left"><p>ScsiNet</p></td>
<td align="left"><p>CommunicationsPeripheral</p></td>
</tr>
<tr class="odd">
<td align="left"><p>10</p></td>
<td align="left"><p>ASCIT8</p></td>
<td align="left"><p>ScsiASCIT8</p></td>
<td align="left"><p>ASCPrePressGraphicsPeripheral</p></td>
</tr>
<tr class="even">
<td align="left"><p>11</p></td>
<td align="left"><p>ASCIT8</p></td>
<td align="left"><p>ScsiASCIT8</p></td>
<td align="left"><p>ASCPrePressGraphicsPeripheral</p></td>
</tr>
<tr class="odd">
<td align="left"><p>12</p></td>
<td align="left"><p>配列</p></td>
<td align="left"><p>ScsiArray</p></td>
<td align="left"><p>ArrayPeripheral</p></td>
</tr>
<tr class="even">
<td align="left"><p>13</p></td>
<td align="left"><p>エンクロージャ</p></td>
<td align="left"><p>ScsiEnclosure</p></td>
<td align="left"><p>EnclosurePeripheral</p></td>
</tr>
<tr class="odd">
<td align="left"><p>14</p></td>
<td align="left"><p>RBC</p></td>
<td align="left"><p>ScsiRBC</p></td>
<td align="left"><p>RBCPeripheral</p></td>
</tr>
<tr class="even">
<td align="left"><p>15</p></td>
<td align="left"><p>「カード リーダー</p></td>
<td align="left"><p>ScsiCardReader</p></td>
<td align="left"><p>CardReaderPeripheral</p></td>
</tr>
<tr class="odd">
<td align="left"><p>16</p></td>
<td align="left"><p>Bridge</p></td>
<td align="left"><p>ScsiBridge</p></td>
<td align="left"><p>BridgePeripheral</p></td>
</tr>
<tr class="even">
<td align="left"><p>17</p></td>
<td align="left"><p>その他</p></td>
<td align="left"><p>ScsiOther</p></td>
<td align="left"><p>OtherPeripheral</p></td>
</tr>
</tbody>
</table>

 

ディスク ドライブのデバイス ID の例に次のようになります。

SCSI\\DiskSEAGATE_ST39102LW_______0004

これには、デバイス ID だけでなく 4 つのハードウェア Id があります。

SCSI\\t\*v(8)p(16)

SCSI\\t\*v(8)

SCSI\\v(8)p(16)r(1)

v(8)p(16)r(1)

3 番目と 4 番目のこれらの他の識別子で*r(1)* リビジョン識別子の最初の文字だけを表します。 これらのハードウェア Id は次の例に示します。

SCSI\\DiskSEAGATE_ST39102LW___

SCSI\\DiskSEAGATE_

SCSI\\DiskSEAGATE_ST39102LW___0

SEAGATE_ST39102LW_______0

SCSI ポート ドライバーでは、前の表のジェネリック型の可変サイズのコードのいずれか 1 つだけの互換性のある ID を提供します。

たとえば、互換性のある ID ディスク ドライブのとおりです。

GenDisk

汎用識別子は、SCSI ドライバーは通常、ジェネリックであるためによりも、他の SCSI デバイスの INF ファイルで使用されます。 SCSI ポート ドライバーないジェネリックの名を返しますまったくシーケンシャル アクセスと「プロセッサ」のデバイスを認識します。

 

 





