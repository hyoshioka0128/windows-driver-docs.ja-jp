---
title: sprocess
description: Sprocess 拡張機能では、指定したセッションですべてのプロセスまたは指定したセッションのプロセスに関する情報を表示します。
ms.assetid: 03c69f3c-501a-44e4-98e0-bf851ca6d24e
keywords:
- Windows デバッグ sprocess
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- sprocess
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f71bb250a80c46037e673ce1a7dc6e84c12290a7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553943"
---
# <a name="sprocess"></a>! sprocess


**! Sprocess**拡張機能は、指定したセッションですべてのプロセスまたは指定したセッションのプロセスに関する情報を表示します。

```dbgcmd
!sprocess Session [Flags [ImageName]] 
!sprocess -?
```

## <a name="span-idddksprocessdbgspanspan-idddksprocessdbgspanparameters"></a><span id="ddk__sprocess_dbg"></span><span id="DDK__SPROCESS_DBG"></span>パラメーター


<span id="_______Session______"></span><span id="_______session______"></span><span id="_______SESSION______"></span> *セッション*   
目的のプロセスを所有しているセッションを指定します。 *セッション*は、常に 10 進数として解釈されます。

*セッション*次の値を持つことができます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>-1</p></td>
<td align="left"><p>現在のセッションを使用します。 これが既定値です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>-2</p></td>
<td align="left"><p>使用<a href="changing-contexts.md#session-context" data-raw-source="[session context](changing-contexts.md#session-context)">セッション コンテキスト</a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>-4</p></td>
<td align="left"><p>セッションですべてのプロセスを表示します。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
表示の詳細レベルを指定します。 *フラグ*次のビットの組み合わせにすることができます。 既定値は 0 です。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>0x0</p></td>
<td align="left"><p>最小限の情報を表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ビット 0 (0x1)</p></td>
<td align="left"><p>時間と優先順位の統計情報を表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ビット 1 (0x2)</p></td>
<td align="left"><p>表示スレッドとプロセスとスレッドの待機状態に関連付けられているイベントの一覧に追加します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ビット 2 (0x4)</p></td>
<td align="left"><p>プロセスに関連付けられているスレッドの一覧の表示を追加します。 ビット 1 (0x2) せずにこのビットを使用する場合、各スレッドは 1 行に表示されます。 これは、ビット 1 に含まれていますが、スタック トレースを各スレッドが表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ビット 3 (0x8)</p></td>
<td align="left"><p>各関数の戻り値のアドレスでは、スタック ポインターと、Itanium ベース システムでは、表示を追加します、 <strong>bsp</strong>値を登録します。 これは、関数の引数の表示を抑制します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ビット 4 (0x10)</p></td>
<td align="left"><p>各関数の戻り値のアドレスのみを表示します。 引数を抑制して、スタック ポインター。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______ImageName______"></span><span id="_______imagename______"></span><span id="_______IMAGENAME______"></span> *ImageName*   
表示するプロセスの名前を指定します。 すべてのプロセスが実行可能イメージの名前一致*ImageName*が表示されます。 イメージの名前と一致しなければなりません」プロセス ブロックにします。 一般に、ファイル拡張子 (通常は .exe) を含む、15 文字の後に切り捨ては、プロセスを開始する呼び出された実行可能ファイルの名前です。 スペースを含むイメージの名前を指定する方法はありません。

<span id="_______-_______"></span> **-?**   
この拡張機能のデバッガー コマンド ウィンドウでヘルプを表示します。 このヘルプ テキストが、いくつか除外します。

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
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

セッションおよびカーネル モード プロセスについては、次を参照してください。[変更コンテキスト](changing-contexts.md)します。 プロセスとスレッドの分析に関する詳細については、次を参照してください。 *Microsoft Windows internals 』*、Mark Russinovich と David Solomon します。 (この本できない場合がありますのいくつかの言語および国。)

<a name="remarks"></a>注釈
-------

この拡張機能の出力はのように[ **! プロセス**](-process.md)ことを除いてのアドレス\_MM\_セッション\_領域と\_MMSESSION は表示されます。

 

 





