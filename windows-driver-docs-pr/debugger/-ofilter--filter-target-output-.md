---
title: .ofilter (ターゲット出力のフィルター処理)
description: .Ofilter コマンドは、ターゲット アプリケーションまたは対象のコンピュータからの出力をフィルター処理します。
ms.assetid: 0b94d177-0e41-4781-b0bc-ed58cee584f1
keywords:
- ターゲットの出力 (.ofilter) コマンドをフィルター処理します。
- .ofilter (ターゲット出力のフィルター) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .ofilter (Filter Target Output)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9a677e282689a761b13b40abbaea4427de4a5d19
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579804"
---
# <a name="ofilter-filter-target-output"></a>.ofilter (ターゲット出力のフィルター処理)


**.Ofilter**コマンドは、対象のアプリケーションまたは対象のコンピュータからの出力をフィルター処理します。

```dbgcmd
.ofilter [/!] String 
.ofilter "" 
.ofilter 
```

## <a name="span-idddkmetafiltertargetoutputdbgspanspan-idddkmetafiltertargetoutputdbgspanparameters"></a><span id="ddk_meta_filter_target_output_dbg"></span><span id="DDK_META_FILTER_TARGET_OUTPUT_DBG"></span>パラメーター


<span id="_______________"></span> **/!**   
デバッガーが含まれていない唯一の出力が表示されるようにフィルターを反転*文字列*します。 デバッガーを表示するこのパラメーターを使用しない場合のみ出力を含む*文字列*します。

<span id="_______String______"></span><span id="_______string______"></span><span id="_______STRING______"></span> *文字列*   
ターゲットの出力に一致する文字列を指定します。 *文字列*、スペースを含めることができますなどの C スタイルの制御文字を使用できません **\\"** と **\\n**します。 *文字列*さまざまなワイルドカード文字と指定子を含めることができます。 構文の詳細については、[文字列のワイルドカード構文](string-wildcard-syntax.md)を参照してください。

囲みます*文字列*引用符で囲んで指定します。 ただし場合、*文字列*セミコロン、スペースを先頭または末尾のスペースを含む引用符を使用する必要があります。 英数字で*文字列*を大文字に変換後の文字が大文字と小文字を区別しないが、実際のパターンに一致します。

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については[ **OutputDebugString** ](https://msdn.microsoft.com/library/windows/desktop/aa363362)し、その他のユーザー モード ルーチンは、Microsoft Windows SDK ドキュメントを参照してください。 詳細については**による DbgPrint**、 **DbgPrintEx**、およびその他のカーネル モード ルーチンは、Windows Driver Kit (WDK) を参照してください。

<a name="remarks"></a>コメント
-------

使用する場合、 **.ofilter**デバッガーには、現在のパターン一致条件が表示されます。 パラメーターを指定せずコマンド。

既存のフィルターをクリアする **.ofilter""** します。 このコマンドは、ユーザー モード ルーチンから送信されるすべてのデータをフィルター処理 (など[ **OutputDebugString**](https://msdn.microsoft.com/library/windows/desktop/aa363362)) とカーネル モード ルーチン (など**による DbgPrint**)。 ただし、デバッガーで常にプロンプトが表示される**DbgPrompt**送信します。

**DbgPrintEx**と**KdPrintEx**ルーチンがしないデバッグ メッセージをフィルター処理のもう 1 つのメソッドを指定します。

 

 





