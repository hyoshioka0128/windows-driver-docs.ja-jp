---
title: 監視
description: 監視拡張機能では、現在のシステム リソース仲裁を表示し、範囲を調停します。
ms.assetid: 95149538-6fcd-4638-b35f-4e1a562e5231
keywords:
- Windows デバッグ アービター
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- arbiter
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b2b46e2b87090e5096ca131515dd02cf86bab3e0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337003"
---
# <a name="arbiter"></a>!arbiter


**! アービター**拡張機能は、現在のシステム リソース アービタと調停範囲が表示されます。

```dbgcmd
    !arbiter [Flags] 
```

## <a name="span-idddkarbiterdbgspanspan-idddkarbiterdbgspanparameters"></a><span id="ddk__arbiter_dbg"></span><span id="DDK__ARBITER_DBG"></span>パラメーター


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
アービタのクラスが表示されますを指定します。 省略した場合、すべての仲裁が表示されます。 これらのビットを自由に組み合わせることができます。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
I/O 仲裁を表示します。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>ビット 1 (0x2)  
メモリの仲裁を表示します。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>ビット 2 (0x4)  
IRQ 仲裁を表示します。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>ビット 3 (0x8)  
DMA 仲裁を表示します。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>ビット 4 (0x10)  
バス番号仲裁を表示します。

<span id="Bit_8__0x100_"></span><span id="bit_8__0x100_"></span><span id="BIT_8__0X100_"></span>ビット 8 (0x100)  
エイリアスは表示されません。

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

参照してください[プラグ アンド プレイ デバッグ](plug-and-play-debugging.md)この拡張機能コマンドのアプリケーション。

<a name="remarks"></a>注釈
-------

各決定者の **! アービター** PDO が範囲 (つまり、範囲の所有者)、およびこの所有者のサービス名に接続されている (わかる場合) にシステム リソースをいくつかのオプション フラグの範囲を割り当てる各が表示されます。

フラグには、次の意味があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Flag</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>S</p></td>
<td align="left"><p>範囲を共有します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>C</p></td>
<td align="left"><p>競合の範囲します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>B</p></td>
<td align="left"><p>ブートに割り当てられた範囲は、します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D</p></td>
<td align="left"><p>範囲は排他のドライバー</p></td>
</tr>
<tr class="odd">
<td align="left"><p>A</p></td>
<td align="left"><p>範囲のエイリアス</p></td>
</tr>
<tr class="even">
<td align="left"><p>P</p></td>
<td align="left"><p>範囲は正の値のデコードします。</p></td>
</tr>
</tbody>
</table>

 

以下に例を示します。

```console
kd> !arbiter 4

DEVNODE 80e203b8 (HTREE\ROOT\0)
  Interrupt Arbiter "" at 80167140
    Allocated ranges:
      0000000000000000 - 0000000000000000   B   80e1d3d8 
      0000000000000001 - 0000000000000001   B   80e1d3d8 
 .....
      00000000000001a2 - 00000000000001a2    
        00000000000001a2 - 00000000000001a2  CB   80e1d3d8 
        00000000000001a2 - 00000000000001a2  CB   80e52538  (Serial)
      00000000000001a3 - 00000000000001a3       80e52778  (i8042prt)
      00000000000001b3 - 00000000000001b3       80e1b618  (i8042prt)
 Possible allocation:
      < none >
```

この例で、[次へ]、最後の行範囲を示しますリソースで構成されるだけで 0x1A3)、0x80E52778 の PDO と i8042prt.sys のサービス。 この行では、フラグは表示されません。

使用できるように[ **! devobj** ](-devobj.md)ノード アドレスの拡張機能とデバイスのデバイスを検索するには、この PDO アドレス。

```console
kd> !devobj 80e52778
Device object (80e52778) is for:
 00000034 \Driver\PnpManager DriverObject 80e20610
Current Irp 00000000 RefCount 1 Type 00000004 Flags 00001040
DevExt 80e52830 DevObjExt 80e52838 DevNode 80e52628 
ExtensionFlags (0000000000)  
AttachedDevice (Upper) 80d78b28 \Driver\i8042prt
Device queue is not busy.
```

 

 





