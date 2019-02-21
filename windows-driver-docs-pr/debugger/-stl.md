---
title: stl
description: Stl の拡張機能では、既知の標準テンプレート ライブラリ (STL) のテンプレートの一部が表示されます。
ms.assetid: a1f1f923-64bd-44c9-941f-9a648888c7e0
keywords:
- stl の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- stl
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a00d9bc1f14bab55c2bed449ed6129a1d136fc4b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529586"
---
# <a name="stl"></a>! stl


**! Stl**拡張機能では、既知の標準テンプレート ライブラリ (STL) のテンプレートの一部が表示されます。

```dbgcmd
!stl [Options] Template 
!stl -?
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
次のいずれかを含めることができます。

<span id="-v"></span><span id="-V"></span>**-v**  
エラーの原因の詳しい出力を表示します。

<span id="-V"></span><span id="-v"></span>**-V**  
によりより詳細な出力など、特定の関数が呼び出され、返されるときに、拡張機能の進行状況に関する情報など、表示されます。

<span id="_______Template______"></span><span id="_______template______"></span><span id="_______TEMPLATE______"></span> *テンプレート*   
表示するテンプレートの名前を指定します。

<span id="_______-_______"></span> **-?**   
デバッガー コマンド ウィンドウで、この拡張機能の簡単なヘルプ テキストを表示します。

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
<td align="left"><p>Exts.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

デバッガーの詳細出力モードが有効になっている場合、詳細なオプションは有効にのみ。

この拡張機能には現在、次の種類の STL テンプレートがサポートしています: string、wstring, vector&lt;*文字列*&gt;、ベクター&lt;*wstring*&gt;、リスト&lt;*文字列*&gt;、リスト&lt;*wstring*&gt;、およびこれらの型のいずれかへのポインター。

 

 





