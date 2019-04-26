---
title: gdikdx.verifier
description: Gdikdx.verifier 拡張機能には、グラフィックス ドライバーの検証中にドライバーの検証の状態が表示されます。
ms.assetid: a7e189bb-ed63-4da3-ab7a-bf502ec131ed
keywords:
- デバッグ gdikdx.verifier Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- gdikdx.verifier
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0c2d691e8dcf7a6743776c60c3a8bb8646b945a6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336569"
---
# <a name="gdikdxverifier"></a>!gdikdx.verifier


**! Gdikdx.verifier**拡張機能は、グラフィックス ドライバーの検証中にドライバーの検証ツールの状態を表示します。

```dbgcmd
!gdikdx.verifier [-Flags] 
```

## <a name="span-idddkgdikdxverifierdbgspanspan-idddkgdikdxverifierdbgspanparameters"></a><span id="ddk__gdikdx_verifier_dbg"></span><span id="DDK__GDIKDX_VERIFIER_DBG"></span>パラメーター


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
このコマンドの出力で表示する情報を指定します。 (ハイフンの前に) 次の任意の組み合わせが使用できます。

<span id="d"></span><span id="D"></span>**D**  
統計を含める表示**メモリ プールの追跡**します。 これには、アドレス、サイズ、および各プールのタグが含まれます。

<span id="h__or___"></span><span id="H__OR___"></span>**h** (または **?**)  
デバッガー コマンド ウィンドウで、このコマンドのいくつかの簡単なヘルプ テキストを表示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Gdikdx.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>利用不可</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

Driver Verifier については、Windows Driver Kit (WDK) ドキュメントを参照してください。

<a name="remarks"></a>注釈
-------

ドライバーはグラフィックス ドライバーでは、標準のカーネル モード拡張機能を確認するとき[ **! verifier** ](-verifier.md)の代わりに使用する必要があります **! gdikdx.verifier**します。

どのフラグを選択するに関係なくこの拡張機能にアクティブになっている Driver Verifier のオプションが表示されます。 ランダムな失敗の頻度に統計情報も表示されます。

 

 





