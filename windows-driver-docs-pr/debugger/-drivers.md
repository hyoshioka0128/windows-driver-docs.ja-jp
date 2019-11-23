---
title: ドライバー
description: Windows XP 以降のバージョンの Windows では、ドライバーの拡張機能は互換性のために残されています。 代わりに、lm コマンドを使用します。
ms.assetid: 48b69af3-bf00-43d3-ac1a-e9513ead8647
keywords:
- ドライバーの Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- drivers
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 20701b8f00bda2228900a43d425fc422f99d69e1
ms.sourcegitcommit: 667b4be765b2eac6bc586d39abef3393a718b23f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2019
ms.locfileid: "70063901"
---
# <a name="drivers"></a>!drivers

>[!NOTE] 
> Windows XP 以降のバージョンの Windows では、 **! drivers**拡張機能は廃止されています。 読み込まれたドライバーおよびその他のモジュールに関する情報を表示するには、 [**lm**](lm--list-loaded-modules-.md)コマンドを使用します。 
>

Lm のコマンドでは、古い **! drivers**拡張子とよく似た形式で情報が表示されます。 ただし、このコマンドでは **、ドライバーの拡張機能**と同じように、ドライバーのメモリ使用量が表示されません。 ドライバーの開始アドレスと終了アドレス、イメージ名、タイムスタンプのみが表示されます。 [ **! Vm**](-vm.md)および[ **! memusage**](-memusage.md)拡張機能を使用して、メモリ使用量の統計情報を表示できます。

```dbgcmd
!drivers [Flags]
```

## <a name="span-idddk__drivers_dbgspanspan-idddk__drivers_dbgspanparameters"></a><span id="ddk__drivers_dbg"></span><span id="DDK__DRIVERS_DBG"></span>パラメータ


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*フラグ*   
には、次の値の任意の組み合わせを指定できます。 (既定値は0x0 です)。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
ディスプレイに、常駐メモリとスタンバイメモリに関する情報が含まれるようにします。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>ビット 1 (0x2)  
このビットが設定され、ビット 2 (0x4) が設定されていない場合、表示には、常駐、スタンバイ、およびロックされているメモリに関する情報と、ローダーエントリのアドレスが含まれます。 ビット2が設定されている場合は、表示がかなり長くなり、より詳細なドライバーイメージの一覧になります。 ヘッダーに関する情報は、セクション情報として記載されています。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>ビット 2 (0x4)  
表示を、より長い、より詳細なドライバーイメージの一覧にします。 各セクションに関する情報が含まれています。 ビット 1 (0x2) が設定されている場合は、ヘッダー情報も含まれます。

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
<td align="left"><p>利用不可</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

この拡張機能コマンドのアプリケーションについては、「[プラグアンドプレイデバッグ](plug-and-play-debugging.md)」を参照してください。 ドライバーとそのメモリ使用量の詳細については、「Windows Driver Kit (WDK)」ドキュメントと「 *Microsoft windows の内部構造*(Mark Russinovich と David ソロモン)」を参照してください。

<a name="remarks"></a>注釈
-------

このコマンドの表示については、次の表で説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">列</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>基本</p></td>
<td align="left"><p>デバイスドライバーコードの開始アドレス (16 進数)。 停止の原因となったコードによって使用されるメモリアドレスが、ドライバーのベースアドレスとリスト内の次のドライバーのベースアドレスの間である場合、そのドライバーは多くの場合、エラーの原因になります。 たとえば、Ncrc810 のベースは0x80654000 です。 そのと0x8065a000 の間のアドレスは、このドライバーに属します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>コードサイズ</p></td>
<td align="left"><p>ドライバーコードの16進数と10進数の両方でのサイズ (kb 単位)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>データサイズ</p></td>
<td align="left"><p>データのドライバーに割り当てられた領域のサイズ (16 進数と10進数の両方)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Locked (ロック)</p></td>
<td align="left"><p>(フラグ0x2 が使用されている場合のみ)ドライバーによってロックされているメモリの量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Tsr</p></td>
<td align="left"><p>(フラグ0x1 または0x2 が使用されている場合のみ)実際に物理メモリに格納されているドライバーのメモリの量。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Standby</p></td>
<td align="left"><p>(フラグ0x1 または0x2 が使用されている場合のみ)スタンバイ状態のドライバーのメモリの量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ローダーエントリ</p></td>
<td align="left"><p>(フラグ0x2 が使用されている場合のみ)ローダーエントリのアドレス。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ドライバー名</p></td>
<td align="left"><p>ドライバーのファイル名。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>作成時刻</p></td>
<td align="left"><p>ドライバーのリンク日。 これをドライバーのファイルの日付と混同しないでください。これは、外部ツールで設定できます。 リンクの日付は、ドライバーまたは実行可能ファイルがコンパイルされるときにコンパイラによって設定されます。 ファイルの日付の近くに配置する必要がありますが、常に同じであるとは限りません。</p></td>
</tr>
</tbody>
</table>

 

次に、このコマンドの切り詰められた例を示します。

```dbgcmd
kd> !drivers
Loaded System Driver Summary
Base     Code Size      Data Size      Driver Name  Creation Time
80080000 f76c0 (989 kb) 1f100 (124 kb) ntoskrnl.exe Fri May 26 15:13:00
80400000 d980  ( 54 kb) 4040  ( 16 kb) hal.dll      Tue May 16 16:50:34
80654000 3f00  ( 15 kb) 1060   ( 4 kb) ncrc810.sys  Fri May 05 20:07:04
8065a000 a460  ( 41 kb) 1e80   ( 7 kb) SCSIPORT.SYS Fri May 05 20:08:05
```

 

 





