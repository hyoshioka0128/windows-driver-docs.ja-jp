---
title: '*.hh* (HTML ヘルプ ファイルを開く)'
description: '*.Hh* コマンドでは、Windows のツールのデバッグ ドキュメントが開きます。'
ms.assetid: 6c6d5b33-ad54-4325-93d7-ed63f9f012e8
keywords:
- '*.hh* (HTML ヘルプ ファイルを開く) Windows のデバッグ'
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .hh (Open HTML Help File)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6d418cb363e08b9358401f9139df9c41de6e75ef
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551418"
---
# <a name="hh-open-html-help-file"></a>*.hh* (HTML ヘルプ ファイルを開く)


***.Hh*** コマンド ツールを Windows のデバッグ ドキュメントが開きます。

```dbgcmd
.hh [Text] 
```

## <a name="span-idddkmetaopenhtmlhelpfiledbgspanspan-idddkmetaopenhtmlhelpfiledbgspanparameters"></a><span id="ddk_meta_open_html_help_file_dbg"></span><span id="DDK_META_OPEN_HTML_HELP_FILE_DBG"></span>パラメーター


<span id="_______Text______"></span><span id="_______text______"></span><span id="_______TEXT______"></span> *テキスト*   
ヘルプ ドキュメントのインデックスで検索するテキストを指定します。

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

 

実行している場合は、このコマンドを使用することはできません[Remote.exe を通じてリモート デバッグ](remote-debugging-through-remote-exe.md)します。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ヘルプ ドキュメントの詳細については、[、のヘルプ ファイルを使用して](using-the-help-documentation.md)を参照してください。

<a name="remarks"></a>注釈
-------

***.Hh*** コマンドは、Windows のツールのデバッグ ドキュメント (Debugger.chm) を開きます。 指定した場合*テキスト*、デバッガーが開きます、**インデックス**し、ドキュメントの検索 ウィンドウ*テキスト*インデックス内のキーワードとして。 指定しない場合*テキスト*、デバッガーが開きます、**内容**ドキュメントのウィンドウ。

 

 





