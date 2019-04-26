---
title: slist
description: Slist 拡張機能では、シングル リンク リスト (SList) が表示されます。
ms.assetid: 2ce6e941-eaa7-4850-9dd9-f4546659dbca
keywords:
- SList (シングル リンク リスト)
- Windows デバッグ slist
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- slist
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ed758b0a7c6114129190248e884c9d77226502bc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338821"
---
# <a name="slist"></a>!slist


**! Slist**拡張機能 (SList) シングル リンク リストを表示します。

```dbgcmd
!slist Address [ Symbol [Offset] ] 
!slist -?
```

## <a name="span-idddkslistdbgspanspan-idddkslistdbgspanparameters"></a><span id="ddk__slist_dbg"></span><span id="DDK__SLIST_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
SLIST のアドレス指定\_ヘッダー。

<span id="_______Symbol______"></span><span id="_______symbol______"></span><span id="_______SYMBOL______"></span> *シンボル*   
表示に使用するデータ型を指定します。 場合*シンボル*を指定すると、デバッガーは、SList の各ノードは、それを表示するときにこのデータ型のインスタンスを前提としています。

<span id="_______Offset______"></span><span id="_______offset______"></span><span id="_______OFFSET______"></span> *オフセット*   
SList ポインター構造内のバイト オフセットを指定します。

<span id="_______-_______"></span> **-?**   
デバッガー コマンド ウィンドウで、この拡張機能の簡単なヘルプ テキストを表示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>利用不可</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Exts.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

リンクされた構造、性質がわかっている場合、*シンボル*と*オフセット*パラメーターは非常に便利です。 違いを確認するには、2 つの例をここでは最初の省略、*シンボル*と*オフセット*パラメーター、2 番目に含まれているときにします。

```dbgcmd
0:000> !slist ListHead
SLIST HEADER:
   +0x000 Alignment          : a000a002643e8
   +0x000 Next               : 2643e8
   +0x004 Depth              : a
   +0x006 Sequence           : a

SLIST CONTENTS:
002643e8  002642c0 0000000a 6e676953 72757461
002642c0  00264198 00000009 6e676953 72757461
00264198  00264070 00000008 6e676953 72757461
00264070  00263f48 00000007 6e676953 72757461
00263f48  00261420 00000006 6e676953 72757461
00261420  002612f8 00000005 6e676953 72757461
002612f8  002611d0 00000004 6e676953 72757461
002611d0  002610a8 00000003 6e676953 72757461
002610a8  00260f80 00000002 6e676953 72757461
00260f80  00000000 00000001 6e676953 72757461
```

```dbgcmd
0:000> !slist ListHead _PROGRAM_ITEM 0
SLIST HEADER:
 +0x000 Alignment          : a000a002643e8
   +0x000 Next               : 2643e8
 +0x004 Depth              : a
   +0x006 Sequence           : a

SLIST CONTENTS:
002643e8
   +0x000 ItemEntry        : _SINGLE_LIST_ENTRY
   +0x004 Signature        : 0xa
   +0x008 Description      : [260]  "Signature is: 10"
002642c0
   +0x000 ItemEntry        : _SINGLE_LIST_ENTRY
   +0x004 Signature        : 9
   +0x008 Description      : [260]  "Signature is: 9"
00264198
   +0x000 ItemEntry        : _SINGLE_LIST_ENTRY
   +0x004 Signature        : 8
   +0x008 Description      : [260]  "Signature is: 8"
00264070
   +0x000 ItemEntry        : _SINGLE_LIST_ENTRY
   +0x004 Signature        : 7
   +0x008 Description      : [260]  "Signature is: 7"
00263f48
   +0x000 ItemEntry        : _SINGLE_LIST_ENTRY
   +0x004 Signature        : 6
   +0x008 Description      : [260]  "Signature is: 6"
00261420
   +0x000 ItemEntry        : _SINGLE_LIST_ENTRY
   +0x004 Signature        : 5
   +0x008 Description      : [260]  "Signature is: 5"
002612f8
   +0x000 ItemEntry        : _SINGLE_LIST_ENTRY
   +0x004 Signature        : 4
   +0x008 Description      : [260]  "Signature is: 4"
002611d0
   +0x000 ItemEntry        : _SINGLE_LIST_ENTRY
   +0x004 Signature        : 3
   +0x008 Description      : [260]  "Signature is: 3"
002610a8
   +0x000 ItemEntry        : _SINGLE_LIST_ENTRY
   +0x004 Signature        : 2
   +0x008 Description      : [260]  "Signature is: 2"
00260f80
   +0x000 ItemEntry        : _SINGLE_LIST_ENTRY
   +0x004 Signature        : 1
   +0x008 Description      : [260]  "Signature is: 1"
```

 

 





