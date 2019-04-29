---
title: poolused
description: Poolused 拡張機能では、各プールの割り当てに使用されるタグに基づいて、メモリ使用の概要が表示されます。
ms.assetid: e801342d-2536-43a3-992b-99942eb3c5ae
keywords:
- Windows デバッグ poolused
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- poolused
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 52af1d34c077699dc9401fb163a0008f8c947be9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334377"
---
# <a name="poolused"></a>!poolused


**! Poolused**拡張機能には、各プールの割り当てに使用されるタグに基づいて、メモリ使用の概要が表示されます。

```dbgcmd
!poolused [Flags [TagString]] 
```

## <a name="span-idddkpooluseddbgspanspan-idddkpooluseddbgspanparameters"></a><span id="ddk__poolused_dbg"></span><span id="DDK__POOLUSED_DBG"></span>パラメーター


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
表示される出力の量と、出力の並べ替え方法を指定します。 ビット 1 (0x2) および 2 (0x4) を同時に使用できないことを除いては、次のビット値の任意の組み合わせにできます。 既定値は、0x0 で、プール タグを使用して並べ替え、集計情報を生成します。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
(詳細) のより詳細な情報が表示されます。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>ビット 1 (0x2)  
並べ替え、非ページ メモリの量の表示を使用します。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>ビット 2 (0x4)  
ページングされたメモリの使用量の表示を並べ替えます。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>ビット 3 (0x8)  
(Windows Server 2003 以降)Standard プールではなく、セッションのプールを表示します。

**注**  を使用することができます、 [ **! セッション**](-session.md)セッション間で切り替えコマンド。

 

<span id="_______TagString______"></span><span id="_______tagstring______"></span><span id="_______TAGSTRING______"></span> *TagString*   
プール タグを指定します。 *TagString*大文字の ASCII 文字列です。 アスタリスク (\*) 任意の文字数を表すために使用することができます。 1 文字を表すために使用する、疑問符 (?) は。 アスタリスクを使用すると、しない限り、 *TagString*に 4 文字の長さでなければなりません。

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

メモリ プールおよびプール タグについては、Windows Driver Kit (WDK) ドキュメントを参照してくださいと*Microsoft Windows internals 』*、Mark Russinovich と David Solomon します。 (これらのリソースできない場合がありますのいくつかの言語および国。)

<a name="remarks"></a>注釈
-------

**! Poolused**拡張機能は、Windows の機能をタグ付け、プールからデータを収集します。 プールのタグ付けは無期限に Windows Server 2003 および以降のバージョンの Windows で有効にします。 Windows XP および Windows の以前のバージョンでは、プールを使用してタグ付けを有効にする必要があります[Gflags](gflags.md)します。

完了前に、拡張機能の実行を停止した場合、デバッガーには、部分的な結果が表示されます。

このコマンドの表示と非ページ プールのページ プールの各タグのメモリ使用を示します。 どちらの場合で、表示には、特定のタグの現在未解決の割り当ての数とそれらの割り当てで消費されるバイト数が含まれます。

この拡張機能からの出力の部分的な例を次に示します。

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

 

 





