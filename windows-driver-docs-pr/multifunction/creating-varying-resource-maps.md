---
title: さまざまなリソース マップの作成
description: さまざまなリソース マップの作成
ms.assetid: bfe3a760-d8fe-4213-9bbe-2bad6927d8e2
keywords:
- さまざまなリソースは、WDK の多機能デバイスをマップします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a02047076db951b88d87b4af4f4404c66ee2bcc6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323618"
---
# <a name="creating-varying-resource-maps"></a>さまざまなリソース マップの作成





標準的なリソース マップでは、多機能端末の子に、全体の親リソースを割り当てることができますのみ、リソース マップをさまざまなで mf.sys によって列挙子の間で、親リソースに分割できます。 さまざまなリソース マップは、Windows XP および、NT ベースのオペレーティング システムの以降のバージョンでサポートされます。

たとえば、PCI バス上のマルチポート シリアル カードを検討してください。 8 個の I/O ポートと単一の共有の割り込みのセットが必要です、カードの 16550 UART 関数の各前提としています。 また、カードが 1 つの PCI 関数として実装されるとします。 このシナリオでは、I/O ポートの 1 つのブロックを要求して、このブロックを各 16550 UART 関数の 1 つの 8 つのセグメントに分割するには一般的です。

カードの 16550 UART 関数に必要な I/O ポートと割り込みリソースだけでなく、デバイスも必要であるメモリの範囲とデバイスのユーザー リソースと仮定します。

これらの前提条件に基づき、mf.sys は次のように構築された、このデバイスのリソース要件の一覧を返します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>リソース</th>
<th>リソース</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>00</p></td>
<td><p><em>メモリ範囲</em>ベース レジスタ アドレス (バー) 0</p></td>
</tr>
<tr class="even">
<td><p>01</p></td>
<td><p><em>プライベート データ</em></p></td>
</tr>
<tr class="odd">
<td><p>02</p></td>
<td><p><em>メモリ範囲</em>1 バー</p></td>
</tr>
<tr class="even">
<td><p>03</p></td>
<td><p><em>プライベート データ</em></p></td>
</tr>
<tr class="odd">
<td><p>04</p></td>
<td><p><em>I/O ポート範囲</em>バー 2</p></td>
</tr>
<tr class="even">
<td><p>05</p></td>
<td><p><em>プライベート データ</em></p></td>
</tr>
<tr class="odd">
<td><p>06</p></td>
<td><p><em>割り込み</em></p></td>
</tr>
</tbody>
</table>

 

ベンダーでは、INF ファイルのディレクティブを使用して、カードの 16550 UART 関数間でのこれらのリソースの共有を指定します。 デバイスのリソースのセグメントを必要とする各関数を使用する必要があります、 **VaryingResourceMap**レジストリ エントリを作成する INF で入力します。 このデバイスの INF ファイルからの抜粋を次に示します。

```cpp
[DDInstall.RegHW] 
; for each "child" function list hardware ID and resource map 
; and/or varying resource map
HKR,Child0002,HardwareID,, child0002-hardware ID
HKR,Child0002,VaryingResourceMap,1,04, 10,00,00,00, 08,00,00,00
HKR,Child0002,ResourceMap,1,06
```

行を含む**VaryingResourceMap**は次のように解釈されます。

-   「1」の次、 **VaryingResourceMap**パラメーターを指定、レジストリ エントリのデータ型が REG\_バイナリ。

-   「1」に続く数字は、さまざまなリソース マップ値です。 '04' では、親リソースは、この子を代入しているのセグメントを示します。 この場合、リソース 04 のセグメント (2 バー) (つまり、シリアル ポートごとに 8 つの I/O ポート範囲を表すリソースの一部) の子に割り当てます。

-   次 2 つの Dword を示す、最初に、リソースと、この子に割り当てる必要がある範囲の長さは、2 番目のオフセット。 この場合、8 個の I/O ポートは、親リソースへのオフセット 0x10 から始まる、この子に割り当てられています。

-   別の親リソース、リソースの数、長さ、この子が必要なし、オフセット、INF、次の最初のリソースの同じ行に含まれます。

**ResourceMap**パラメーターについては、「[標準リソース マップの作成](creating-standard-resource-maps.md)を示し、この子が PCI デバイスの割り込みをここでは 06 リソース共有を取得する必要があります。

このデバイスの 4 つの子関数を指定する場合より完全な例を次に示します。

```cpp
[Version]
Signature="$Windows NT$"
Class=MultiFunction
ClassGUID={4d36e971-e325-11ce-bfc1-08002be10318}
Provider=%MYCOMPANY%
LayoutFile=layout.inf
DriverVer=1/20/2000
[ControlFlags]
ExcludeFromSelect=*
[Manufacturer]
%MYCOMPANY%=MYCOMPANY

[MYCOMPANY]
%MYCOMPANY_4PORT%=MYCOMPANY4PORT_inst, PCI\VEN_10B5&DEV_9050&SUBSYS_003112E0

[MYCOMPANY4PORT_inst]
Include = mf.inf
Needs = MFINSTALL.mf

[MYCOMPANY4PORT_inst.HW]
AddReg=MYCOMPANY4PORT_inst.RegHW

[MYCOMPANY4PORT_inst.Services]
Include = mf.inf
Needs = MFINSTALL.mf.Services

[MYCOMPANY4PORT_inst.RegHW] 
HKR,Child0000,HardwareID,,*PNP0501
HKR,Child0000,VaryingResourceMap,1,04, 00,00,00,00, 08,00,00,00
HKR,Child0000,ResourceMap,1,06
HKR,Child0001,HardwareID,,*PNP0501
HKR,Child0001,VaryingResourceMap,1,04, 08,00,00,00, 08,00,00,00
HKR,Child0001,ResourceMap,1,06
HKR,Child0002,HardwareID,,*PNP0501
HKR,Child0002,VaryingResourceMap,1,04, 10,00,00,00, 08,00,00,00
HKR,Child0002,ResourceMap,1,06
HKR,Child0003,HardwareID,,*PNP0501
HKR,Child0003,VaryingResourceMap,1,04, 18,00,00,00, 08,00,00,00
HKR,Child0003,ResourceMap,1,06

[Strings]
MYCOMPANY= "MYCOMPANY Inc."
MYCOMPANY_4PORT="MYCOMPANY 4PORT"
```

 

 




