---
title: .logopen (ログ ファイルを開く)
description: .Logopen コマンドでは、新しいログ ファイルに、デバッガー コマンド ウィンドウからイベントとコマンドのコピーを送信します。
ms.assetid: 00ccc09b-3fd7-462f-a688-2f7b45b584fb
keywords:
- ログ ファイル (.logopen) を開くコマンド
- ログ ファイル、ログ ファイルを開く (.logopen) コマンド
- .logopen (ログ ファイルを開く) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .logopen (Open Log File)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 06cc9590f1b7304cf1ff5061681d534d5dc87c15
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574139"
---
# <a name="logopen-open-log-file"></a>.logopen (ログ ファイルを開く)


**.Logopen**コマンドは、イベントのコピーを送信しからコマンドを[デバッガー コマンド ウィンドウ](debugger-command-window.md)新しいログ ファイルにします。

```dbgcmd
.logopen [Options] [FileName] 
.logopen /d
```

## <a name="span-idddkmetaopenlogfiledbgspanspan-idddkmetaopenlogfiledbgspanparameters"></a><span id="ddk_meta_open_log_file_dbg"></span><span id="DDK_META_OPEN_LOG_FILE_DBG"></span>パラメーター


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
次のオプションのいずれか:

<span id="_t"></span><span id="_T"></span>**/t**  
ログ ファイルの名前には、現在の日付と時刻のプロセス ID を追加します。 ファイル名の後とファイル名拡張子の前に、このデータが挿入されます。

<span id="_u"></span><span id="_U"></span>**/u**  
ログ ファイルを Unicode 形式で書き込みます。 このオプションを省略した場合、デバッガーは、ASCII (ANSI) 形式でログ ファイルを書き込みます。

<span id="_______FileName______"></span><span id="_______filename______"></span><span id="_______FILENAME______"></span> *FileName*   
ログ ファイルの名前を指定します。 完全なパスまたはファイル名のみを指定することができます。 ファイル名にスペースが含まれている場合は、囲む*FileName*引用符で囲んで指定します。 パスを指定しない場合、デバッガーには、現在のディレクトリが使用されます。 省略した場合*FileName*、デバッガー Dbgeng.log ファイルの名前します。

<span id="________d______"></span><span id="________D______"></span> **/d**   
ターゲット プロセスまたはターゲット コンピュータと対象の状態の名前に基づいてファイル名を自動的に選択します。 ファイルは、常にファイル名拡張子は .log を持ちます。

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

 

<a name="remarks"></a>コメント
-------

ファイルを開くログがあれば実行すると、 **.logopen**コマンド、デバッガーが終了します。 既に存在するファイル名を指定する場合、ファイルの内容は上書きされます。

**.Logopen/t**コマンド プロセス ID、日付と時刻をログ ファイルの名前を追加します。 次の例では、16 進数でプロセス ID が 0x02BC、日付が 2005 年 2 月 28 日、および時間は、9:05:50.935。

```dbgcmd
0:000> .logopen /t c:\logs\mylogfile.txt
Opened log file 'c:\logs\mylogfile_02BC_2005-02-28_09-05-50-935.txt'
```

 

 





