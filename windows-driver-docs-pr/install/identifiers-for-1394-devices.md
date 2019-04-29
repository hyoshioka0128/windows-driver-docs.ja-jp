---
title: 1394 デバイスの識別子
description: 1394 デバイスの識別子
ms.assetid: 6ab2538a-af4c-4c46-bda5-abb431c5bd6b
keywords:
- デバイスの識別文字列 WDK、1394 デバイス
- 識別文字列の WDK デバイス、1394 デバイス
- 識別子の WDK デバイス、1394 デバイス
- 1394 デバイス識別子 WDK デバイスのインストール
- デバイス Id の WDK デバイスのインストール
- ハードウェア Id の WDK デバイスのインストール
- 互換性のある Id WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80c1ce1e6a3f9261b6619f483b47fdee6a80f43c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335351"
---
# <a name="identifiers-for-1394-devices"></a>1394 デバイスの識別子





1394 バス ドライバーは、デバイスのこれらの識別子を作成します。

1394\\VendorName&ModelName

1394\\UnitSpecId & UnitSwVersion

各項目の意味は次のとおりです。

-   *VendorName*ハードウェア ベンダーの名前を指定します。

-   *ModelName*デバイスを識別します。

-   *UnitSpecId*ソフトウェアの仕様の機関を識別します。

-   *UnitSwVersion*ソフトウェアの仕様を識別します。

これらの識別子の構築に使用される情報は、デバイスの構成 ROM.

1394 バス ドライバーが互換性のある ID と、デバイス ID や、ハードウェア ID の両方として最初の識別子と 2 番目の識別子を使用する場合、デバイスの製造元とモデル名の文字列がある、 バス ドライバーが、デバイス ID と互換性の ID の両方、として 2 番目の識別子を使用し、ハードウェア ID のクエリを実行している場合は、二重の null を返す場合は、デバイスは、ベンダーまたはモデルの名前文字列がない、 IEEE1394 バス ドライバーの特定の状況下でデバイス ID がないハードウェア ID を提供するそのため、 これは、デバイス ID は、ハードウェア Id のいずれかの一般的な規則の例外です。

IEEE1394 でカメラのデバイス ID は次のようになります。

1394\\SONY&CCM-DS250_1.08

多機能デバイスには、デバイスの構成 ROM. に各単位ディレクトリ識別子の別のセットがあります。

場合は、デバイスの機能のドライバーは、sbp-2 ポート ドライバーの上に位置、そのデバイス ID は、次の形式とします。

SBP2\\VendorName & ModelName LUNn\*

各項目の意味は次のとおりです。

-   *VendorName*はハードウェアのベンダーです。

-   *ModelName*デバイスを識別します。

-   *n* \*は 16 進数で論理ユニットの数の下位 2 バイトを表す文字列です。 多機能デバイス上のさまざまな関数は、この数値以外はまったく同じデバイス Id を作成します。

Sbp-2 1394 のハード ディスクのデバイス ID が次のようにあります。

SBP2\\VST_TECHNOLOGIESINC VST_FULL_HEIGHT_FIREWIRE_DRIVE &AMP; LUN0

として 1394 bus SBP2 ポート ドライバーがない、デバイス ID として分類ハードウェア ID ただし、1394 バスは、ハードウェア Id および互換性 Id を区別、一方、SBP2 ポート ドライバーは提供されません。 **IRP_MN_QUERY_ID**型の Irp **BusQueryHardwareIDs**と**IRP_MN_QUERY_ID**型の Irp **BusQueryCompatibleIDs** SBP24 つの識別子の同じセットを返します。

SBP2\\VendorName & ModelName CmdSetIdn\*

SBP2\\Gen

汎用

SBP2\\n\*(& d)\*

各項目の意味は次のとおりです。

- *n\** コマンド セットの ID 番号です。

- *Gen*は、次の表のジェネリック型の列に記載されている汎用的な名前の 1 つです。

- *d\** 論理ユニットの数の上位 2 バイトの下位 5 ビットを実行して、数値の形式です。 この数値が数値のコードに対応するデバイスの汎用的な名前を*Gen*識別子の文字列します。

4 番目の ID が前の例を記載 (SBP2\\*n\*(& d)\**)、SBP2 ハードウェアのすべての識別子をその中で一意では、どちらも*n\** 、コマンド セットの ID 番号と*d\**、汎用的な名前の数値のコードは、10 進数、いない 16 進数は。

このテーブルには、SBP2 ポート ドライバーによって返される一般的なデバイス名が一覧表示します。 すべてではなく、ほとんど SBP2 ポート ドライバーによって生成された汎用的な名前の SCSI ポート ドライバーによって生成されるもののサブセットです。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">1394 型コード</th>
<th align="left">デバイスの種類</th>
<th align="left">ジェネリック型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>RBC_DEVICE または DIRECT_ACCESS_DEVICE (0)</p></td>
<td align="left"><p>Disk</p></td>
<td align="left"><p>GenDisk</p></td>
</tr>
<tr class="even">
<td align="left"><p>SEQUENTIAL_ACCESS_DEVICE (1)</p></td>
<td align="left"><p>シーケンシャル</p></td>
<td align="left"><p>GenSequential</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PRINTER_DEVICE (2)</p></td>
<td align="left"><p>プリンター</p></td>
<td align="left"><p>GenPrinter</p></td>
</tr>
<tr class="even">
<td align="left"><p>WRITE_ONCE_READ_MULTIPLE_DEVICE (4)</p></td>
<td align="left"><p>ワーム</p></td>
<td align="left"><p>GenWorm</p></td>
</tr>
<tr class="odd">
<td align="left"><p>READ_ONLY_DIRECT_ACCESS_DEVICE (5)</p></td>
<td align="left"><p>CdRom</p></td>
<td align="left"><p>GenCdRom</p></td>
</tr>
<tr class="even">
<td align="left"><p>SCANNER_DEVICE (6)</p></td>
<td align="left"><p>スキャナー</p></td>
<td align="left"><p>GenScanner</p></td>
</tr>
<tr class="odd">
<td align="left"><p>OPTICAL_DEVICE (7)</p></td>
<td align="left"><p>光学式</p></td>
<td align="left"><p>GenOptical</p></td>
</tr>
<tr class="even">
<td align="left"><p>MEDIUM_CHANGER (8)</p></td>
<td align="left"><p>チェンジャー</p></td>
<td align="left"><p>GenChanger</p></td>
</tr>
<tr class="odd">
<td align="left"><p>既定の種類 (上記以外のすべての値)</p></td>
<td align="left"><p>その他</p></td>
<td align="left"><p>GenSbp2Device</p></td>
</tr>
</tbody>
</table>

 

 

 





