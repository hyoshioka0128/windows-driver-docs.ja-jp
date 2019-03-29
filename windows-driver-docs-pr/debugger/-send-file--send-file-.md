---
title: .send_file (ファイルの送信)
description: .Send_file コマンドでは、ファイルをコピーします。 プロセス サーバーをリモート デバッグを実行する場合に送信ファイル、スマート クライアントのコンピューターからプロセス サーバーのコンピューター。
ms.assetid: ad12ec46-79a3-458a-acdc-c2ccb06f8c96
keywords:
- .send_file (送信ファイル) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .send_file (Send File)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a0905f792e32ed595c7053573525b5836b1ba277
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578164"
---
# <a name="sendfile-send-file"></a>.send\_ファイル (ファイルの送信)


**.Send\_ファイル**コマンド ファイルをコピーします。 プロセス サーバーをリモート デバッグを実行する場合に送信ファイル、スマート クライアントのコンピューターからプロセス サーバーのコンピューター。

```dbgcmd
.send_file [-f] Source Destination 
.send_file [-f] -s Destination 
```

## <a name="span-idddkmetasendfiledbgspanspan-idddkmetasendfiledbgspanparameters"></a><span id="ddk_meta_send_file_dbg"></span><span id="DDK_META_SEND_FILE_DBG"></span>パラメーター


<span id="_______-f______"></span><span id="_______-F______"></span> **-f**   
強制的にファイルを作成します。 既定では、 **.send\_ファイル**の既存のファイルは上書きされません。 -F スイッチを使用する場合は、先のファイルは、作成、および同じ名前の既存のファイルは上書きされます。

<span id="_______Source______"></span><span id="_______source______"></span><span id="_______SOURCE______"></span> *ソース*   
送信するファイルのファイル名と完全なパスを指定します。 プロセス サーバーをデバッグする場合は、スマート クライアントが実行されているコンピューターでこのファイルを配置する必要があります。

<span id="_______Destination______"></span><span id="_______destination______"></span><span id="_______DESTINATION______"></span> *変換先*   
ファイルが書き込まれるディレクトリを指定します。 プロセス サーバーをデバッグする場合、このディレクトリ名は、プロセス サーバーが実行されているコンピューターで評価されます。

<span id="_______-s______"></span><span id="_______-S______"></span> **-s**   
原因のデバッガーが読み込まれたシンボル ファイルをすべてコピーします。

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

 

<a name="remarks"></a>コメント
-------

このコマンドは、プロセス サーバー、リモート デバッグ実行されましたが、代わりにローカルでデバッグを開始する場合に特に便利です。 この場合、.send を使用することができます\_ファイル、プロセス サーバーに、デバッガーが使用されているすべてのシンボル ファイルをコピーする -s コマンド。 これらのシンボル ファイルは、ローカル コンピューターで実行されているデバッガーで使用できます。

 

 





