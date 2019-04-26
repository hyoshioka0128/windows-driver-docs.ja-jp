---
title: PCI Express デバイス用のコンテナー ID
description: PCI Express デバイス用のコンテナー ID
ms.assetid: ff86def3-a278-4f7b-a394-42f608f8993d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e234d54d0a83bd7e90ac1742fe851e09687421fd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344327"
---
# <a name="container-ids-for-pci-express-devices"></a>PCI Express デバイス用のコンテナー ID


PCI Express (PCIe) バスは、コンテナー ID を表現できません。 Windows オペレーティング システムは、PCI バス ドライバーを返す PCIe デバイスのグループ化デバイス コンテナーと判断した場合、リムーバブル機能に依存します。

PCIe デバイスは、次の PCIe 登録ビットを読み取ることによってリムーバブル PCI バス ドライバーを決定します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">PCIe 登録</th>
<th align="left">バイト オフセット</th>
<th align="left">ビットの場所</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>PCI Express 機能</p></td>
<td align="left"><p>0x02</p></td>
<td align="left"><p>8-スロットの実装</p></td>
<td align="left"><p>1 に設定すると、このビット値は、統合されたコンポーネントに接続されているのではなく、物理スロットにこのポートに関連付けられている PCIe リンクが接続されていることを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>スロットの機能</p></td>
<td align="left"><p>0x14</p></td>
<td align="left"><p>6-ホット プラグ可能</p></td>
<td align="left"><p>このビット値を 1 に設定すると、このスロットがホット プラグ操作をサポートできることを示します。</p></td>
</tr>
</tbody>
</table>

 

両方の次の条件が満たされている場合、PCI バス ドライバーはリムーバブルと PCIe デバイスをマークします。

-   スロットが実装されているビットは 1 に設定されます。

-   ホット プラグ可能なビットが 1 に設定します。

これらの設定に使用されるメカニズムは登録ビット PCIe チップセットのバージョンとの製造元によって異なります。 など一部チップセットの他のチップセットが革帯電圧料金接続 (Vcc) またはゼロ (GND) にある物理ピンが必要ですが、プログラムのこれらのビットでは、ファームウェアことができます。

デバイスは、ACPI 名前空間、_EJ0 メソッドを実装する場合は、ACPI ドライバーとしてリムーバブル デバイスとマークことに注意します。 これは、スロットの実装します。 またはホット プラグ可能なビットの設定に関係なく発生します。 詳細については、次を参照してください。、[ホットプラグ PCI と Windows](https://go.microsoft.com/fwlink/p/?linkid=26278)ホワイト ペーパー。

PCIe インターフェイスの詳細については、次を参照してください。、 [PCIe ベース](https://go.microsoft.com/fwlink/p/?linkid=69486)仕様。

 

 





