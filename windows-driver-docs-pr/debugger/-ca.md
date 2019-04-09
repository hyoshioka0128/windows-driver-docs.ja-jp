---
title: ca
description: Ca 拡張機能では、コントロールの領域に関する情報が表示されます。
ms.assetid: 7e9164a5-238e-4327-bd2a-a814bff5f7db
keywords:
- コントロールの領域
- ca の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ca
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 329cbf608b047efc53ccf316e3d1af7a332c89a2
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238479"
---
# <a name="ca"></a>!ca


**! Ca**拡張機能は、コントロールの領域に関する情報を表示します。

```dbgsyntax
!ca [Address | 0 | -1] [Flags]
```

## <a name="span-idddkcadbgspanspan-idddkcadbgspanparameters"></a><span id="ddk__ca_dbg"></span><span id="DDK__CA_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
コントロールの領域のアドレス。 このパラメーターに 0 を指定する場合は、すべてのコントロールの領域に関する情報が表示されます。 このパラメーターに-1 を指定する場合は、使用されていないセグメントの一覧に関する情報が表示されます。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
情報を指定するフラグが表示されます。 このパラメーターは、次のフラグの 1 つ以上のビットごとの OR です。

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
<td align="left"><p><span id="0x1"></span><span id="0X1"></span>0x1</p></td>
<td align="left"><p>セグメント情報を表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="0x2"></span><span id="0X2"></span>0x2</p></td>
<td align="left"><p>サブセクションの情報を表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="0x4"></span><span id="0X4"></span>0x4</p></td>
<td align="left"><p>マップ ビューの一覧を表示します。 (Windows 7 以降)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="0x8"></span><span id="0X8"></span>0x8</p></td>
<td align="left"><p>表示 (単一行) 出力を最適化します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="0x10"></span><span id="0X10"></span>0x10</p></td>
<td align="left"><p>コントロールのファイルに格納された領域を表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="0x20"></span><span id="0X20"></span>0x20</p></td>
<td align="left"><p>表示のコントロールの領域は、ページング ファイルによってバックアップします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="0x40"></span><span id="0X40"></span>0x40</p></td>
<td align="left"><p>イメージ コントロールの領域を表示します。</p></td>
</tr>
</tbody>
</table>

 

指定されていない最後の 3 つのフラグの 3 種類すべてのコントロールの領域が表示されます。

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

コントロールの領域については、次を参照してください。 *Microsoft Windows internals 』* Mark Russinovich と David Solomon します。 

<a name="remarks"></a>注釈
-------

すべてのコントロールの領域の一覧を取得するマップ ファイルを使用して、 [ **! memusage** ](-memusage.md)拡張機能。

以下に例を示します。

```dbgcmd
kd> !memusage
 loading PFN database
loading (99% complete)
             Zeroed:     16 (    64 kb)
               Free:      0 (     0 kb)
            Standby:   2642 ( 10568 kb)
           Modified:    720 (  2880 kb)
    ModifiedNoWrite:      0 (     0 kb)
       Active/Valid:  13005 ( 52020 kb)
         Transition:      0 (     0 kb)
            Unknown:      0 (     0 kb)
              TOTAL:  16383 ( 65532 kb)
  Building kernel map
  Finished building kernel map

  Usage Summary (in Kb):
Control Valid Standby Dirty Shared Locked PageTables  name
ff8636e8    56    376     0     0     0     0  mapped_file( browseui.dll )
ff8cf388    24      0     0     0     0     0  mapped_file( AVH32DLL.DLL )
ff8d62c8    12      0     0     0     0     0  mapped_file( PSAPI.DLL )
ff8dd468   156     28     0     0     0     0  mapped_file( INOJOBSV.EXE )
fe424808   136     88     0    52     0     0  mapped_file( oleaut32.dll )
fe4228a8   152     44     0   116     0     0  mapped_file( MSVCRT.DLL )
ff8ec848     4      0     0     0     0     0    No Name for File
ff859de8     0     32     0     0     0     0  mapped_file( timedate.cpl )
. . . . .

kd> !ca ff8636e8

ControlArea @ff8636e8
  Segment:    e1b74548    Flink              0   Blink:               0
 Section Ref        0    Pfn Ref           6c   Mapped Views:        1
  User Ref           1    Subsections        5   Flush Count:         0
  File Object ff86df88    ModWriteCount      0   System Views:        0
  WaitForDel         0    Paged Usage      380   NonPaged Usage       e0
  Flags (10000a0) Image File HadUserReference 

   File: \WINNT\System32\browseui.dll

Segment @ e1b74548:
   Base address        0  Total Ptes        c8  NonExtendPtes:       c8
   Image commit        1  ControlArea ff8636e8  SizeOfSegment: c8000
   Image Base          0  Committed          0  PTE Template:   31b8438
 Based Addr   76e10000  ProtoPtes   e1b74580  Image Info:    e1b748a4

Subsection 1. @ ff863720
   ControlArea: ff8636e8  Starting Sector 0 Number Of Sectors 2
   Base Pte     e1b74580  Ptes In subsect        1 Unused Ptes          0
   Flags              15  Sector Offset          0 Protection           1
    ReadOnly CopyOnWrite 

Subsection 2. @ ff863740
   ControlArea: ff8636e8  Starting Sector 2 Number Of Sectors 3d0
   Base Pte     e1b74584  Ptes In subsect       7a Unused Ptes          0
   Flags              35  Sector Offset          0 Protection           3
    ReadOnly CopyOnWrite 

Subsection 3. @ ff863760
   ControlArea: ff8636e8  Starting Sector 3D2 Number Of Sectors 7
   Base Pte     e1b7476c  Ptes In subsect        1 Unused Ptes          0
   Flags              55  Sector Offset          0 Protection           5
    ReadOnly CopyOnWrite 

Subsection 4. @ ff863780
   ControlArea: ff8636e8  Starting Sector 3D9 Number Of Sectors 21f
   Base Pte     e1b74770  Ptes In subsect       44 Unused Ptes          0
   Flags              15  Sector Offset          0 Protection           1
    ReadOnly CopyOnWrite 

Subsection 5. @ ff8637a0
   ControlArea: ff8636e8  Starting Sector 5F8 Number Of Sectors 3a
   Base Pte     e1b74880  Ptes In subsect        8 Unused Ptes          0
   Flags              15  Sector Offset          0 Protection           1
    ReadOnly CopyOnWrite 
```

 

 





