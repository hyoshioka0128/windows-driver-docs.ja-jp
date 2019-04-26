---
title: .remote (Remote.exe サーバーの作成)
description: .Remote コマンドでは、現在のデバッグ セッションへのリモート接続を有効にすると、Remote.exe サーバーを開始します。
ms.assetid: fa3de33c-ba8c-4e9c-9899-b9a43f3195bf
keywords:
- Remote.exe サーバー (.remote) コマンドを作成します。
- remote.exe、Remote.exe サーバーの作成 (.remote) コマンドをリモート デバッグ
- .remote (Remote.exe サーバーの作成) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .remote (Create Remote.exe Server)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 86f546e75d8e999298b0b59aaad0573291ef9dce
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338917"
---
# <a name="remote-create-remoteexe-server"></a>.remote (Remote.exe サーバーの作成)


**.Remote**コマンドの開始、 [Remote.exe Server](starting-a-remote-exe-session.md)、現在のデバッグ セッションへのリモート接続を有効にします。

```dbgcmd
.remote session
```

## <a name="span-idddkmetacreateremoteexeserverdbgspanspan-idddkmetacreateremoteexeserverdbgspanparameters"></a><span id="ddk_meta_create_remote_exe_server_dbg"></span><span id="DDK_META_CREATE_REMOTE_EXE_SERVER_DBG"></span>パラメーター


<span id="_______session______"></span><span id="_______SESSION______"></span> *session*   
デバッグ セッションに付ける名前を指定します。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

使用することができます、 **.remote**で WinDbg、KD、CDB でコマンドは使用できません。

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

Remote.exe サーバーおよび Remote.exe クライアントを使用する方法の詳細については、次を参照してください。 [Remote.exe でリモート デバッグ](remote-debugging-through-remote-exe.md)します。

<a name="remarks"></a>注釈
-------

**.Remote**コマンドは Remote.exe プロセスを作成し、Remote.exe サーバーに現在のデバッガーを有効にします。 このサーバーでは、Remote.exe クライアントが現在のデバッグ セッションに接続できるようにします。

 

 





