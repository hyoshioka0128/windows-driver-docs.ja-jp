---
title: pcitree
description: Pcitree 拡張機能には、子の PCI バスと CardBus バスに接続されているデバイスなど、PCI デバイス オブジェクトに関する情報が表示されます。
ms.assetid: cd1b2f85-b8de-4396-8b37-79bb3d62092c
keywords:
- PCI バス
- PCI デバイス
- Windows デバッグ pcitree
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pcitree
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4ec6a45831e8f04d9b6cf7b6ba66fb57622e5fb7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334441"
---
# <a name="pcitree"></a>!pcitree


**! Pcitree**拡張機能には、子の PCI バス CardBus バスなど、PCI デバイス オブジェクトに関する情報が表示され、デバイスを関連付けること。

```dbgcmd
!pcitree
```

## <span id="ddk__pcitree_dbg"></span><span id="DDK__PCITREE_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

参照してください[プラグ アンド プレイ デバッグ](plug-and-play-debugging.md)この拡張機能コマンドのアプリケーション。 PCI バスと PCI デバイス オブジェクトについては、Windows Driver Kit (WDK) ドキュメントを参照してください。

<a name="remarks"></a>注釈
-------

以下に例を示します。

```dbgcmd
kd> !pcitree

Bus 0x0 (FDO Ext fe517338)
  0600 12378086 (d=0,  f=0) devext fe4f4ee8 Bridge/HOST to PCI
  0601 70008086 (d=d,  f=0) devext fe4f4ce8 Bridge/PCI to ISA
  0101 70108086 (d=d,  f=1) devext fe4f4ae8 Mass Storage Controller/IDE
  0604 00211011 (d=e,  f=0) devext fe4f4788 Bridge/PCI to PCI

Bus 0x1 (FDO Ext fe516998)
  0200 905010b7 (d=8,  f=0) devext fe515ee8 Network Controller/Ethernet
  0100 81789004 (d=9,  f=0) devext fe515ce8 Mass Storage Controller/SCSI
  0300 0519102b (d=10, f=0) devext fe4f4428 Display Controller/VGA

Total PCI Root busses processed = 1
```

この表示を理解するのには、表示される最終的なデバイスを検討してください。 基底クラスは 03 で、そのサブクラスは 00、そのデバイス ID は 0x0519、なり、仕入先 ID は 0x102B です。 これらの値はすべて、デバイス自体に固有です。

数値"d ="デバイス番号です。数値"f ="は、関数の数です。 After"devext"は、デバイスの拡張機能のアドレス、0xFE4F4428 です。 最後に、基底クラス名とサブクラス名が表示されます。

使用して、デバイスの詳細情報を取得する、 [ **! devext** ](-devext.md)拡張機能コマンドの引数としてデバイスの拡張機能のアドレスを使用します。 この特定のデバイス用に使用するコマンドになります。

```dbgcmd
kd> !devext fe4f4428 pci 
```

場合、 **! pcitree**拡張機能、エラーが、多くの場合、この適切に読み込まれた、PCI シンボルがなかったことを意味します。 使用[ **.reload pci.sys** ](-reload--reload-module-.md)この問題を解決します。

 

 





