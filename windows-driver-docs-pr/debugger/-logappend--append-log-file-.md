---
title: .logappend (ログ ファイルの追加)
description: .Logappend コマンドでは、イベントと、デバッガー コマンド ウィンドウから指定されたログ ファイルにコマンドのコピーを追加します。
ms.assetid: e1c58c34-1fc5-4ec3-bd37-6c7816735aec
keywords:
- ログ ファイル (.logappend) コマンドを追加します。
- ログ ファイル、ログ ファイル (.logappend) の追加コマンド
- .logappend (ログ ファイルを追加する) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .logappend (Append Log File)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2355ff00e776403108f1f480b2b04a6965927956
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336181"
---
# <a name="logappend-append-log-file"></a>.logappend (ログ ファイルの追加)


**.Logappend**コマンドは、イベントのコピーを追加しからコマンドを[デバッガー コマンド ウィンドウ](debugger-command-window.md)指定されたログ ファイルにします。

```dbgcmd
.logappend [/u] [FileName]
```

## <a name="span-idddkmetaappendlogfiledbgspanspan-idddkmetaappendlogfiledbgspanparameters"></a><span id="ddk_meta_append_log_file_dbg"></span><span id="DDK_META_APPEND_LOG_FILE_DBG"></span>パラメーター


<span id="________u______"></span><span id="________U______"></span> **/u**   
ログ ファイルを Unicode 形式で書き込みます。 このパラメーターを省略した場合、デバッガーは、ASCII (ANSI) 形式でログ ファイルを書き込みます。

**注**  が使用する既存のログ ファイルに追加するときに、 **/u**パラメーターを使用して、ログ ファイルを作成する場合にのみ、 **/u**オプション。 それ以外の場合、ログ ファイルには読み取りにくくなる可能性があります、ASCII および Unicode 文字が含まれます。

 

<span id="_______FileName______"></span><span id="_______filename______"></span><span id="_______FILENAME______"></span> *FileName*   
ログ ファイルの名前を指定します。 完全なパスまたはファイル名のみを指定することができます。 ファイル名にスペースが含まれている場合は、囲む*FileName*引用符で囲んで指定します。 パスを指定しない場合、デバッガーには、現在のディレクトリが使用されます。 省略した場合*FileName*、デバッガー Dbgeng.log ファイルの名前します。

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

ファイルを開くログがあれば実行すると、 **.logappend**コマンド、デバッガーが、ログ ファイルを閉じます。 既に存在するファイルの名前を指定する場合、デバッガーは、ファイルに新しい情報を追加します。 ファイルが存在しない場合、デバッガーが作成されます。

 

 





