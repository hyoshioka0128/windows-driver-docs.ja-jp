---
title: gflag
description: Gflag 拡張機能を設定またはグローバル フラグが表示されます。
ms.assetid: b661f775-a313-4a4d-a3db-1e4dacf830de
keywords:
- Windows デバッグ gflag
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- gflag
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 95848b6dc0eded63d377144d75aa0d3d3be0f1ae
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336561"
---
# <a name="gflag"></a>!gflag


**! Gflag**拡張機能を設定またはグローバル フラグを表示します。

```dbgcmd
!gflag [+|-] Value 
!gflag {+|-} Abbreviation 
!gflag -? 
!gflag 
```

## <a name="span-idddkgflagdbgspanspan-idddkgflagdbgspanparameters"></a><span id="ddk__gflag_dbg"></span><span id="DDK__GFLAG_DBG"></span>パラメーター


<span id="_______Value______"></span><span id="_______value______"></span><span id="_______VALUE______"></span> *値*   
32 ビットの 16 進数を指定します。 プラス記号を使用しない場合 (**+**) またはマイナス記号 (**-**)、グローバル フラグのビット フィールドの新しい値がこの数になります。 プラス記号を追加する場合 (**+**)、この数値の前に、数は 1 に設定する 1 つまたは複数のグローバル フラグのビットを指定します。 マイナス記号を追加する場合 (**-**)、この数値の前に、数は 0 に設定する 1 つまたは複数のグローバル フラグ ビットを指定します。

<span id="_______Abbreviation______"></span><span id="_______abbreviation______"></span><span id="_______ABBREVIATION______"></span> *省略形*   
1 つのグローバル フラグを指定します。 *省略形*グローバル フラグを 1 に設定されている 3 文字の省略形は、(**+**) または 0 (**-**)。

<span id="_______-_______"></span> **-?**   
グローバル フラグの省略形の一覧を含むこの拡張機能のいくつかのヘルプ テキストが表示されます、[デバッガー コマンド ウィンドウ](debugger-command-window.md)します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p></p>
Kdextx86.dll Ntsdexts.dll</td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Exts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

グローバル フラグ ユーティリティ (Gflags.exe) を使用して、これらのフラグを設定することもできます。

<a name="remarks"></a>注釈
-------

任意の引数を指定しない場合、 **! gflag**拡張機能は、現在のグローバル フラグの設定を表示します。

次の表には使用できる省略形が含まれています、*略称*パラメーター。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値</th>
<th align="left">名前</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x00000001</p></td>
<td align="left"><p>「soe と略記されます」</p></td>
<td align="left"><p>例外で停止します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000002</p></td>
<td align="left"><p>「sls」</p></td>
<td align="left"><p>ローダーのスナップを表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00000004</p></td>
<td align="left"><p>"dic"</p></td>
<td align="left"><p>最初のコマンドをデバッグします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000008</p></td>
<td align="left"><p>"shg"</p></td>
<td align="left"><p>GUI では、応答を停止 (つまり、ハングなど) が停止した場合を停止します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00000010</p></td>
<td align="left"><p>"htc"</p></td>
<td align="left"><p>ヒープの末尾のチェックを有効にします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000020</p></td>
<td align="left"><p>"hfc"</p></td>
<td align="left"><p>ヒープの無料のチェックを有効にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00000040</p></td>
<td align="left"><p>"hpc"</p></td>
<td align="left"><p>ヒープ パラメーター チェックを有効にします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000080</p></td>
<td align="left"><p>"hvc"</p></td>
<td align="left"><p>呼び出しでヒープの検証を有効にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00000100</p></td>
<td align="left"><p>"ptc"</p></td>
<td align="left"><p>プールの末尾のチェックを有効にします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000200</p></td>
<td align="left"><p>"pfc"</p></td>
<td align="left"><p>プールの空きチェックを有効にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00000400</p></td>
<td align="left"><p>"ptg"</p></td>
<td align="left"><p>プールのタグ付けを有効にします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000800</p></td>
<td align="left"><p>「加熱」</p></td>
<td align="left"><p>ヒープのタグ付けを有効にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00001000</p></td>
<td align="left"><p>"ust"</p></td>
<td align="left"><p>ユーザー モードのスタック トレース DB を作成します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00002000</p></td>
<td align="left"><p>"kst"</p></td>
<td align="left"><p>カーネル モード スタック トレース DB を作成します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00004000</p></td>
<td align="left"><p>"otl"</p></td>
<td align="left"><p>各型のオブジェクトの一覧を維持します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00008000</p></td>
<td align="left"><p>"htd"</p></td>
<td align="left"><p>DLL をヒープでタグ付けを有効にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00010000</p></td>
<td align="left"><p>"idp"</p></td>
<td align="left"><p>未使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00020000</p></td>
<td align="left"><p>"d32"</p></td>
<td align="left"><p>Microsoft Win32 サブシステムのデバッグを有効にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00040000</p></td>
<td align="left"><p>"ksl"</p></td>
<td align="left"><p>カーネル デバッガーのシンボルの読み込みを有効にします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00080000</p></td>
<td align="left"><p>"dp"</p></td>
<td align="left"><p>カーネル スタックのページングを無効にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00100000</p></td>
<td align="left"><p>"scb"</p></td>
<td align="left"><p>重要なシステムの区切りを有効にします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00200000</p></td>
<td align="left"><p>"dhc"</p></td>
<td align="left"><p>ヒープを無効にする無料で結合します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00400000</p></td>
<td align="left"><p>"ece"</p></td>
<td align="left"><p>閉じる例外を有効にします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00800000</p></td>
<td align="left"><p>"eel"</p></td>
<td align="left"><p>例外のログ記録を有効にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x01000000</p></td>
<td align="left"><p>"eot"</p></td>
<td align="left"><p>オブジェクト ハンドル型のタグ付けを有効にします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x02000000</p></td>
<td align="left"><p>"hpa"</p></td>
<td align="left"><p>ページの末尾のヒープ割り当てを配置します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x04000000</p></td>
<td align="left"><p>"dwl"</p></td>
<td align="left"><p>Winlogon プロセスをデバッグします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x08000000</p></td>
<td align="left"><p>"ddp"</p></td>
<td align="left"><p>カーネル モードを無効にする<strong>による DbgPrint</strong>と<strong>KdPrint</strong>出力します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10000000</p></td>
<td align="left"><p>NULL</p></td>
<td align="left"><p>未使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x20000000</p></td>
<td align="left"><p>「sue」</p></td>
<td align="left"><p>Stop on unhandled user-mode exception</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x40000000</p></td>
<td align="left"><p>NULL</p></td>
<td align="left"><p>未使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x80000000</p></td>
<td align="left"><p>"dpd"</p></td>
<td align="left"><p>保護されている DLL の検証を無効にします。</p></td>
</tr>
</tbody>
</table>

 

 

 





