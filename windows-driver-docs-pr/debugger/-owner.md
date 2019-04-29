---
title: 所有者
description: 所有者の拡張機能は、モジュールまたは関数の所有者を表示します。
ms.assetid: f881bd86-89cf-49fd-9bca-3ecc96123be8
keywords:
- 所有者が Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- owner
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ad1f624edd930da5da8edc86ae1ab4b61d90d45e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334423"
---
# <a name="owner"></a>!owner


**! 所有者**拡張機能は、モジュールまたは関数の所有者を表示します。

```dbgcmd
!owner [Module[!Symbol]]
```

## <a name="span-idddkownerdbgspanspan-idddkownerdbgspanparameters"></a><span id="ddk__owner_dbg"></span><span id="DDK__OWNER_DBG"></span>パラメーター


<span id="_______Module______"></span><span id="_______module______"></span><span id="_______MODULE______"></span> *モジュール*   
所有者が必要なモジュールを指定します。 アスタリスク (\*) の末尾に*モジュール*追加の文字の任意の数を表します。

<span id="_______Symbol______"></span><span id="_______symbol______"></span><span id="_______SYMBOL______"></span> *シンボル*   
内のシンボルを指定*モジュール*所有者が必要です。 アスタリスク (\*) の末尾に*シンボル*追加の文字の任意の数を表します。 場合*シンボル*は省略すると、全体のモジュールの所有者が表示されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

パラメーターを指定しないと、エラーが発生した場合 **! 所有者**エラーが発生したモジュールまたは関数の所有者の名前が表示されます。

モジュールまたは関数の名前を渡す場合、 **! 所有者**拡張機能、デバッガーは、単語を表示します。**フォロー アップ**後に指定されたモジュールまたは関数の所有者の名前。

この拡張機能の有用な情報を表示するには、まずモジュールおよび関数の所有者の名前を含む triage.ini ファイルを作成する必要があります。

Triage.ini ファイルとの例の詳細について、 **! 所有者**拡張機能を参照してください[モジュールを指定して、関数の所有者](specifying-module-and-function-owners.md)します。

 

 





