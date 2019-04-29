---
title: ドライバー
description: Windows XP および Windows の以降のバージョンでは、ドライバー拡張機能は廃止されています。 代わりに、lm コマンドを使用します。
ms.assetid: 48b69af3-bf00-43d3-ac1a-e9513ead8647
keywords:
- ドライバーが Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- drivers
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 10b925d99cd29487ed4d3d1ce72a43861bf97213
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336797"
---
# <a name="drivers"></a>!drivers

Windows XP および Windows での以降のバージョンで、 **! ドライバー**拡張機能は廃止されています。 読み込まれているドライバーと他のモジュールに関する情報を表示するには、使用、 [ **lm** ](lm--list-loaded-modules-.md)コマンド。 コマンドの lm t n が非常に古いのような形式で情報を表示します **! ドライバー**拡張機能。 ただし、このコマンドには、ドライバーのメモリ使用量が表示されますされません、 **! ドライバー**拡張機能でした。 ドライバーの開始と終了アドレス、イメージの名前、およびタイムスタンプのみが表示されます。 [ **! Vm** ](-vm.md)と[ **! memusage** ](-memusage.md)拡張機能を使用して、メモリ使用量の統計情報を表示します。

```dbgcmd
!drivers [Flags]
```

## <a name="span-idddkdriversdbgspanspan-idddkdriversdbgspanparameters"></a><span id="ddk__drivers_dbg"></span><span id="DDK__DRIVERS_DBG"></span>パラメーター


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
次の値の組み合わせにすることができます。 (既定値は 0x0。)

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
メモリ常駐とスタンバイ メモリに関する情報が追加ディスプレイをによりします。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>ビット 1 (0x2)  
このビットが設定されて、ビット 2 (0x4) が設定されていない場合は、表示にはローダーのエントリのアドレスと同様に常駐している、スタンバイ、およびロックのメモリに関する情報が含まれます。 ビット 2 が設定されている場合にくらい時間が長くより詳細な一覧ドライバー イメージの表示に、これにより、します。 ヘッダーに関する情報は、セクションの情報が含まれています。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>ビット 2 (0x4)  
くらい時間が長くより詳細な一覧に、ドライバーのイメージの表示をによりします。 各セクションの情報が含まれます。 ビット 1 (0x2) を設定すると、これと、ヘッダー情報も含まれます。

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
<td align="left"><p>利用不可</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

参照してください[プラグ アンド プレイ デバッグ](plug-and-play-debugging.md)この拡張機能コマンドのアプリケーション。 ドライバーと、メモリの使用については、Windows Driver Kit (WDK) ドキュメントを参照してくださいと*Microsoft Windows internals 』* Mark Russinovich と David Solomon します。 (これらのリソースできない場合がありますのいくつかの言語および国。)

<a name="remarks"></a>注釈
-------

このコマンドの表示の詳細については、次の表で示されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">列</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>基本</p></td>
<td align="left"><p>16 進数で、デバイス ドライバーのコードの開始アドレス。 ドライバーのベース アドレスと、一覧で [次へ] のドライバーのベース アドレスの間、停止を原因となるコードで使用されるメモリ アドレスが少なくなると、そのドライバーは頻繁にエラーの原因です。 たとえば、Ncrc810.sys の基本クラスは、0x80654000 です。 0x8065a000 との間にあるアドレスは、このドライバーに属しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>コードのサイズ</p></td>
<td align="left"><p>16 進数および 10 進数の両方で、ドライバーのコードのサイズ。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>データ サイズ</p></td>
<td align="left"><p>16 進数および 10 進数の両方でのデータ用のドライバーをキロバイト単位での領域の量が割り当てられます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Locked (ロック)</p></td>
<td align="left"><p>(使用場合にのみフラグ 0x2 です)ドライバーによってロックされているメモリの量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>常駐</p></td>
<td align="left"><p>(0x1 にフラグを付けるときにのみまたは 0x2 を使用)実際に物理メモリに存在するドライバーのメモリの量。</p></td>
</tr>
<tr class="even">
<td align="left"><p>スタンバイ</p></td>
<td align="left"><p>(0x1 にフラグを付けるときにのみまたは 0x2 を使用)スタンバイ状態では、ドライバーのメモリの量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ローダーのエントリ</p></td>
<td align="left"><p>(使用場合にのみフラグ 0x2 です)ローダーのエントリのアドレス。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ドライバー名</p></td>
<td align="left"><p>ドライバーのファイル名。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>作成時刻</p></td>
<td align="left"><p>ドライバーのリンクの日付。 混同しないでくださいこのファイルの日時のドライバーは、外部ツールで設定できます。 リンクの日付は、ドライバーまたは実行可能ファイルのコンパイル時に、コンパイラによって設定されます。 ファイルの日付の近くにある必要がありますが、常に同じではありません。</p></td>
</tr>
</tbody>
</table>

 

このコマンドの切り捨てられた例を次に示します。

```dbgcmd
kd> !drivers
Loaded System Driver Summary
Base     Code Size      Data Size      Driver Name  Creation Time
80080000 f76c0 (989 kb) 1f100 (124 kb) ntoskrnl.exe Fri May 26 15:13:00
80400000 d980  ( 54 kb) 4040  ( 16 kb) hal.dll      Tue May 16 16:50:34
80654000 3f00  ( 15 kb) 1060   ( 4 kb) ncrc810.sys  Fri May 05 20:07:04
8065a000 a460  ( 41 kb) 1e80   ( 7 kb) SCSIPORT.SYS Fri May 05 20:08:05
```

 

 





