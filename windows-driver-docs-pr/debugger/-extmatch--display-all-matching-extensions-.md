---
title: .extmatch (一致するすべての拡張機能の表示)
description: .Extmatch コマンドには、現在読み込まれている拡張機能の指定したパターンに一致する Dll によってエクスポートされた拡張機能のコマンドが表示されます。
ms.assetid: 068a32ce-c5ac-4fee-9e9d-e47393097675
keywords:
- .extmatch (一致するすべての拡張機能を表示する) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .extmatch (Display All Matching Extensions)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 34b0e8fe39749ce5a29d1ff0cd3f1417296f3b44
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556719"
---
# <a name="extmatch-display-all-matching-extensions"></a>.extmatch (一致するすべての拡張機能の表示)


**.Extmatch**コマンド拡張機能が現在読み込まれている、指定したパターンに一致する Dll によってエクスポートされた拡張機能のコマンドを表示します。

```dbgcmd
.extmatch [Options] Pattern 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
検索オプションを指定します。 次のオプションの 1 つ以上を使用することができます。

<span id="_e_ExtDLLPattern"></span><span id="_e_extdllpattern"></span><span id="_E_EXTDLLPATTERN"></span>**/e** **** *ExtDLLPattern*  
パターンを指定した文字列と一致する拡張 Dll によってエクスポートされた拡張機能コマンドに列挙型を制限します。 *ExtDLLPattern*拡張 DLL のファイル名と照合されます。

<span id="_n"></span><span id="_N"></span>**/n**  
拡張機能が表示される場合は、拡張機能名を除外します。 したがって、このオプションが指定されている場合、拡張機能名のみが表示されます。

<span id="________D______"></span><span id="________d______"></span> **/D**   
使用して、出力が表示されます。[デバッガー マークアップ言語 (DML)](debugger-markup-language-commands.md)します。 出力では、表示されている各拡張機能は、拡張機能の詳細を取得するクリックできるリンクです。 すべての拡張機能モジュールでは、DML をサポートします。

<span id="_______Pattern______"></span><span id="_______pattern______"></span><span id="_______PATTERN______"></span> *パターン*   
拡張機能を含める必要があるパターンを指定します。 *パターン*さまざまなワイルドカード文字と指定子を含めることができます。 構文の詳細については、次を参照してください。[文字列のワイルドカード構文](string-wildcard-syntax.md)します。

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
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

読み込まれた拡張 Dll の一覧を表示するには、使用、 [ **.chain** ](-chain--list-debugger-extensions-.md)コマンド。

すべての読み込まれた拡張 Dll を持つエクスポートという名前を示す、このコマンドの例を次に示します。 ヘルプ。

```dbgcmd
0:000> .extmatch help 
!ext.help
!exts.help
!uext.help
!ntsdexts.help
```

次の例では、文字列で始まるすべての拡張機能コマンドの一覧"he"拡張機能の名前が文字列"ex"で始まる Dll によってエクスポートされます。

```dbgcmd
0:000> .extmatch /e ext* he* 
!ext.heap
!ext.help
!exts.heap
!exts.help
```

次の例では、どの DML のサポートを確認するために、すべての拡張機能コマンドが一覧表示します。

![screen shot of .extmatch /d output](images/extmatch01.png)

 

 





