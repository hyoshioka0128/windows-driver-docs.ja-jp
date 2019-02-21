---
title: .fpo (FPO コントロールより優先)
description: .Fpo コマンドでは、フレーム ポインターの省略 (FPO) の上書きを制御します。
ms.assetid: a1a20f5d-71c9-487b-bcba-a87b60d74588
keywords:
- .fpo (FPO コントロールより優先) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .fpo (Control FPO Overrides)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4f5d395cc83473a7003830004e506d23e5f757ca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528053"
---
# <a name="fpo-control-fpo-overrides"></a>.fpo (FPO コントロールより優先)


**.Fpo**コマンドは、フレーム ポインターの省略 (FPO) の上書きを制御します。

```dbgcmd
.fpo -s [-fFlag] Address 
.fpo -d Address 
.fpo -x Address 
.fpo -o Address 
.fpo Address 
```

## <a name="span-idddkmetacontrolfpooverridesdbgspanspan-idddkmetacontrolfpooverridesdbgspanparameters"></a><span id="ddk_meta_control_fpo_overrides_dbg"></span><span id="DDK_META_CONTROL_FPO_OVERRIDES_DBG"></span>パラメーター


<span id="_______-s______"></span><span id="_______-S______"></span> **-s**   
指定したアドレスに FPO オーバーライドを設定します。

<span id="_______-fFlag______"></span><span id="_______-fflag______"></span><span id="_______-FFLAG______"></span> **-f * * * フラグ*   
上書きの FPO フラグを指定します。 間にスペースを追加する必要がありますいない **-f**と*フラグ*します。 フラグは、引数として受け取り、フラグとその引数の間にスペースを追加する必要があります。 必要に応じて複数のフラグ、行う必要があります、 **-f**スイッチ (たとえば、 **fb fp 4 - fe**)。 使用することができます、 **-f**スイッチとのみ **-s**します。 次の値のいずれかを使用することができます*フラグ*します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Flag</th>
<th align="left">効果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>B</strong></p></td>
<td align="left"><p>セット<strong>fUseBP</strong>等しく<strong>TRUE</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>e</strong></p></td>
<td align="left"><p>セット<strong>fUseSEH</strong>等しく<strong>TRUE</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>n</strong></p></td>
<td align="left"><p>セット<strong>cbFrame</strong> FRAME_NONFPO を等しくします。 (既定では、cbFrame に設定 FRAME_FPO。)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>l</strong> <strong></strong>  <em>用語</em></p></td>
<td align="left"><p>セット<strong>cdwLocals</strong>等しく<em>用語</em>します。 <em>用語</em>するローカル DWORD 数を指定する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>p</strong> <strong></strong>  <em>用語</em></p></td>
<td align="left"><p>セット<strong>cdwParams</strong>等しく<em>用語</em>します。 <em>用語</em>する DWORD カウント パラメーターを指定する必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>r</strong> <strong></strong>  <em>用語</em></p></td>
<td align="left"><p>セット<strong>cbRegs</strong>等しく<em>用語</em>します。 <em>用語</em>するレジスタの数を指定する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>s</strong> <strong></strong>  <em>用語</em></p></td>
<td align="left"><p>セット<strong>cbProcSize</strong>等しく<em>用語</em>します。 <em>用語</em>するプロシージャのサイズを指定する必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>t</strong> <strong></strong>  <em>用語</em></p></td>
<td align="left"><p>セット<strong>cbFrame</strong>等しく<em>用語</em>します。 <em>用語</em>フレームの種類は次のいずれかを指定する必要があります。</p>
<ul>
<li><p>FRAME_FPO 0</p></li>
<li><p>FRAME_TRAP 1</p></li>
<li><p>FRAME_TSS 2</p></li>
<li><p>FRAME_NONFPO 3</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
デバッガーを設定またはオーバーライドまたはアドレス、デバッガーを表示する必要がありますが上書きを削除する場所のアドレスを指定します。 このアドレスは、現在のモジュールの一覧で、モジュール内である必要があります。

<span id="_______-d______"></span><span id="_______-D______"></span> -**D**   
指定したアドレスに FPO オーバーライドを削除します。

<span id="_______-x______"></span><span id="_______-X______"></span> **-x**   
含むモジュール内のすべての FPO 上書きの削除、*アドレス*アドレス。

<span id="_______-o______"></span><span id="_______-O______"></span> **-o**   
含むモジュール内のすべての FPO 上書きが表示されます、*アドレス*アドレス。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

パラメーターを指定せず、 **.fpo**コマンドは、指定したアドレスを FPO 上書きを表示します。

(Microsoft Visual Studio 6.0 と以前のバージョンを含む)、一部のコンパイラでは、スタック フレームを設定する方法を示す FPO 情報を生成します。 スタック ウォーク、中に、デバッガーは、スタックを理解するのにこれらの FPO レコードを使用します。 使用することができます、コンパイラに FPO、間違った情報が生成された場合、 **.fpo**この問題を解決するコマンド。

 

 





