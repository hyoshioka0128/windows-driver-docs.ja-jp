---
title: poolused
description: Poolused 拡張機能では、各プール割り当てに使用されるタグに基づいて、メモリ使用量の概要が表示されます。
ms.assetid: e801342d-2536-43a3-992b-99942eb3c5ae
keywords:
- poolused Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- poolused
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ef77fb5afa09c0669db9fa72ce8583453208897d
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025192"
---
# <a name="poolused"></a>!poolused


**! Poolused**拡張機能では、各プール割り当てに使用されるタグに基づいて、メモリ使用量の概要が表示されます。

```dbgcmd
!poolused [Flags [TagString]] 
```

## <a name="span-idddk__poolused_dbgspanspan-idddk__poolused_dbgspanparameters"></a><span id="ddk__poolused_dbg"></span><span id="DDK__POOLUSED_DBG"></span>パラメータ


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*フラグ*   
表示する出力の量と、出力を並べ替える方法を指定します。 これは、ビット 1 (0x2) と 2 (0x4) を同時に使用できない点を除いて、次のビット値の任意の組み合わせにすることができます。 既定値は0x0 で、プールタグによって並べ替えられた概要情報を生成します。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
詳細情報を表示します。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>ビット 1 (0x2)  
非ページメモリ使用量によってディスプレイを並べ替えます。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>ビット 2 (0x4)  
ページングされたメモリ使用量で表示を並べ替えます。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>ビット 3 (0x8)  
(Windows Server 2003 以降)標準プールではなくセッションプールを表示します。

**注:**   セッションを切り替えるには、 [ **! session**](-session.md)コマンドを使用します。

 

<span id="_______TagString______"></span><span id="_______tagstring______"></span><span id="_______TAGSTRING______"></span>*Tagstring*   
プールタグを指定します。 *Tagstring*は、大文字と小文字を区別する ASCII 文字列です。 アスタリスク (\*) を使用すると、任意の数の文字を表すことができます。疑問符 (?) を使用すると、正確に1文字を表すことができます。 アスタリスクを使用しない限り、 *Tagstring*の長さは4文字にする必要があります。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts .dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

メモリプールとプールタグの詳細については、「Windows Driver Kit (WDK)」のドキュメントと*Microsoft windows の内部構造*を参照してください。これには、Mark Russinovich と David ソロモンが使用されます。

<a name="remarks"></a>コメント
-------

**! Poolused**拡張機能は、Windows のプールタグ付け機能からデータを収集します。 プールのタグ付けは、Windows Server 2003 以降のバージョンの Windows で完全に有効になります。 Windows XP 以前のバージョンの Windows では、 [Gflags](gflags.md)を使用してプールのタグ付けを有効にする必要があります。

完了前に拡張機能の実行を停止した場合、デバッガーは部分的な結果を表示します。

このコマンドの表示では、ページングプールおよび非ページプールの各タグのメモリ使用量が表示されます。 どちらの場合も、表示には、指定されたタグに対する現在未解決の割り当ての数と、それらの割り当てによって使用されているバイト数が含まれます。

この拡張機能からの出力の例を次に示します。

```dbgcmd
0: kd> !poolused
   Sorting by  Tag

  Pool Used:
            NonPaged            Paged
 Tag    Allocs     Used    Allocs     Used
 1394        1      520         0        0UNKNOWN pooltag '1394', please update pooltag.txt
 1MEM        1     3368         0        0UNKNOWN pooltag '1MEM', please update pooltag.txt
 2MEM        1     3944         0        0UNKNOWN pooltag '2MEM', please update pooltag.txt
 3MEM        3      248         0        0UNKNOWN pooltag '3MEM', please update pooltag.txt
 8042        4     3944         0        0PS/2 kb and mouse , Binary: i8042prt.sys
 AGP         1      344         2      384UNKNOWN pooltag 'AGP ', please update pooltag.txt
 AcdN        2     1072         0        0TDI AcdObjectInfoG 
 AcpA        3      192         1      504ACPI Pooltags , Binary: acpi.sys
 AcpB        0        0         4      576ACPI Pooltags , Binary: acpi.sys
 AcpD       40    13280         0        0ACPI Pooltags , Binary: acpi.sys
 AcpF        6      240         0        0ACPI Pooltags , Binary: acpi.sys
 AcpM        0        0         1      128ACPI Pooltags , Binary: acpi.sys
 AcpO        4      208         0        0ACPI Pooltags , Binary: acpi.sys

...

 WmiG       30     6960         0        0Allocation of WMIGUID 
 WmiR       63     4032         0        0Wmi Registration info blocks 
 Wmip      146     3504       182    18600Wmi General purpose allocation 
 Wmit        1     4096         7    49480Wmi Trace 
 Wrpa        2      720         0        0WAN_ADAPTER_TAG 
 Wrpc        1       72         0        0WAN_CONN_TAG 
 Wrpi        1      120         0        0WAN_INTERFACE_TAG 
 Wrps        2      128         0        0WAN_STRING_TAG 
 aEoP        1      672         0        0UNKNOWN pooltag 'aEoP', please update pooltag.txt
 fEoP        1       16         0        0UNKNOWN pooltag 'fEoP', please update pooltag.txt
 hSVD        0        0         1       40Shared Heap Tag , Binary: mrxdav.sys
 hibr        0        0         1    24576UNKNOWN pooltag 'hibr', please update pooltag.txt
 iEoP        1       24         0        0UNKNOWN pooltag 'iEoP', please update pooltag.txt
 idle        2      208         0        0Power Manager idle handler 
 jEoP        1       24         0        0UNKNOWN pooltag 'jEoP', please update pooltag.txt
 mEoP        1       88         0        0UNKNOWN pooltag 'mEoP', please update pooltag.txt
 ohci        1      136         0        01394 OHCI host controller driver 
 rx..       3     1248         0        0UNKNOWN pooltag '  rx', please update pooltag.txt
 sidg        2       48         0        0GDI spooler events 
 thdd        0        0         1    20480DirectDraw/3D handle manager table 
 usbp       18    77056         2       96UNKNOWN pooltag 'usbp', please update pooltag.txt
 vPrt        0        0        18    68160UNKNOWN pooltag 'vPrt', please update pooltag.txt
 TOTAL     3570214 209120008     38769 13066104
```

 

 





