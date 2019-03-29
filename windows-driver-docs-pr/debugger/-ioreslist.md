---
title: ioreslist
description: Ioreslist 拡張機能では、IO_RESOURCE_REQUIREMENTS_LIST 構造体が表示されます。
ms.assetid: cb599656-2e0a-41ec-8358-a42047974dea
keywords:
- Windows デバッグ ioreslist
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ioreslist
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 69a92e005ad4b3adcbbe4b347857ced1232e79cc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582205"
---
# <a name="ioreslist"></a>!ioreslist


**! Ioreslist**拡張機能の表示、IO\_リソース\_要件\_リスト構造体。

```dbgcmd
!ioreslist Address 
```

## <a name="span-idddkioreslistdbgspanspan-idddkioreslistdbgspanparameters"></a><span id="ddk__ioreslist_dbg"></span><span id="DDK__IORESLIST_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
IO の 16 進数のアドレスを指定します\_リソース\_要件\_リスト構造体。

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

参照してください[プラグ アンド プレイ デバッグ](plug-and-play-debugging.md)この拡張機能コマンドのアプリケーション。 については、IO\_リソース\_要件\_構造の一覧で、Windows Driver Kit (WDK) ドキュメントを参照してください。

<a name="remarks"></a>コメント
-------

この拡張機能からの出力の例を次に示します。

```dbgcmd
kd> !ioreslist 0xe122b768

IoResList at 0xe122b768 : Interface 0x5  Bus 0  Slot 0xe
  Alternative 0 (Version 1.1)
    Preferred Descriptor 0 - Port (0x1) Device Exclusive (0x1)
      Flags (0x01) - PORT_IO
      0x000100 byte range with alignment 0x000100
      1000 - 0x10ff
    Alternative Descriptor 1 - Port (0x1) Device Exclusive (0x1)
      Flags (0x01) - PORT_IO
      0x000100 byte range with alignment 0x000100
      0 - 0xffffffff
    Descriptor 2 - DevicePrivate (0x81) Device Exclusive (0x1)
      Flags (0000) -
      Data:              : 0x1 0x0 0x0
    Preferred Descriptor 3 - Memory (0x3) Device Exclusive (0x1)
      Flags (0000) - READ_WRITE
      0x001000 byte range with alignment 0x001000
      40080000 - 0x40080fff
    Alternative Descriptor 4 - Memory (0x3) Device Exclusive (0x1)
      Flags (0000) - READ_WRITE
      0x001000 byte range with alignment 0x001000
      0 - 0xffffffff
    Descriptor 5 - DevicePrivate (0x81) Device Exclusive (0x1)
      Flags (0000) -
      Data:              : 0x1 0x1 0x0
    Descriptor 6 - Interrupt (0x2) Shared (0x3)
      Flags (0000) - LEVEL_SENSITIVE
      0xb - 0xb
```

IO\_リソース\_要件\_リストに関する情報を格納します。

-   リソースの種類

    リソースの 4 つの種類があります。I/O、メモリ、IRQ、DMA します。

-   記述子

    各優先設定には、「優先」記述子をさまざまな「方法」記述子がいます。

このリソースの一覧には、次の要求が含まれています。

-   I/O の範囲

    0x1000 に 0x10FF、包括的の範囲が優先されますが、0x100 で固定された制限が、0 ~ 0 xffffffff、範囲の任意の 0x100 範囲を使用できます。 (たとえば、0x1100 に 0x11FF は許容される) です。

-   Memory

    0x40080000 に 0x40080FFF の範囲が優先されますが、任意の範囲サイズ 0x1000 にも 0x1000 に配置する、0 ~ 0 xffffffff の間にあるを使用できます。

-   IRQ

    IRQ 0 xb を使用する必要があります。

割り込みと DMA チャネルは、同じの先頭と末尾を範囲として表されます。

 

 





