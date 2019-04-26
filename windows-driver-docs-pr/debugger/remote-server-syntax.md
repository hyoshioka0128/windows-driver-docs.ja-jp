---
title: Remote サーバーの構文
description: サーバー側のリモート ツールを開始するには、コマンドラインで、次の構文を使用します。
ms.assetid: fecc9f43-6946-4d99-840b-a85c75ac397c
keywords:
- リモート サーバーの構文の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- Remote Server Syntax
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 93fa605ad436efbf676756cdd871888f1c198045
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353505"
---
# <a name="remote-server-syntax"></a>Remote サーバーの構文


サーバー側のリモート ツールを開始するには、コマンドラインで、次の構文を使用します。

```console
remote /s Command SessionName [/f Color] [/b] [/u User [/u User...]] [/ud User [/ud User...]] [/v | /-v]
```

## <a name="span-idddkremoteserversyntaxdtoolsspanspan-idddkremoteserversyntaxdtoolsspanparameters"></a><span id="ddk_remote_server_syntax_dtools"></span><span id="DDK_REMOTE_SERVER_SYNTAX_DTOOLS"></span>パラメーター


<span id="________s______"></span><span id="________S______"></span> **/s**   
サーバー セッションを開始します。

<span id="_______Command______"></span><span id="_______command______"></span><span id="_______COMMAND______"></span> *コマンド*   
コンソール ベースのプログラムを起動するコマンドを指定します。 コマンドは、パラメーターを含めることができます。 コマンドには、スペースが含まれている場合は、引用符で囲みます。

<span id="_______SessionName______"></span><span id="_______sessionname______"></span><span id="_______SESSIONNAME______"></span> *SessionName*   
リモート セッションに名前を割り当てます。 名前にスペースが含まれている場合は、引用符で囲みます。 このパラメーターは区別されません。

<span id="________f______"></span><span id="________F______"></span> **/f**   
サーバーのコマンド ウィンドウで、テキストの色を指定します。

<span id="________b______"></span><span id="________B______"></span> **/b**   
サーバーのコマンド ウィンドウの背景色を指定します。

<span id="_______Color______"></span><span id="_______color______"></span><span id="_______COLOR______"></span> *色*   
色を指定します。 有効な値は黒、青、緑、シアン、赤、紫、黄色、白、lblack、lblue、lgreen、lred、lpurple、lyellow、および lwhite は。

<span id="________u______"></span><span id="________U______"></span> **/u**   
ユーザーまたはリモート セッションに接続を許可するグループを指定します既定では、すべてのユーザーは許可されています。 ユーザーと指定されたグループ以外の権限を拒否されたすべてのユーザーこのパラメーターを使用すると、*ユーザー*サブパラ メーターです。

<span id="________ud______"></span><span id="________UD______"></span> **/ud**   
リモート セッションに接続する権限を拒否するユーザーまたはグループを指定します既定では、だれのアクセス許可が拒否されました。

<span id="_______User______"></span><span id="_______user______"></span><span id="_______USER______"></span> *ユーザー*   
ユーザーまたはグループの名前を示す\[*ドメイン* | *コンピューター*\]\\{*ユーザー*  | *グループ*} の形式。 ローカル コンピューターのユーザーまたはグループを指定する場合は、コンピューター名を省略します。

<span id="________v______"></span><span id="________V______"></span> **/v**   
セッションは、表示します。 詳細については、次を参照してください。[表示セッション](remote-tool-concepts.md#visible-session)します。

既定では、デバッガー セッションのみが表示され、セッションは、の値、*コマンド*パラメーターに含める単語**kd**、 **dbg**、 **remoteds**、 **ntsd**、または**cdb**。 そうしないと、セッションは表示されません。

<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
リモート デバッガー セッションは、見えなくなります。 詳細については、次を参照してください。[表示セッション](remote-tool-concepts.md#visible-session)します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

*コマンド*と*SessionName*構文行に示されている順序でパラメーターを表示する必要があります。

リモート セッションを終了するには、次のように入力します。  <strong>@k</strong>します。 詳細については、次を参照してください。[リモート セッションのコマンド](remote-session-commands.md)します。

リモート ツールでは、現在のユーザーには、参加するアクセス許可はありません。 セッションは作成されません。

1 台のコンピューターでは、複数のリモート セッションを開始するときに、セッションごとに新しいコマンド ウィンドウを開きます。 また、セッションごとに別のセッション名を使用します。 セッション名は名前付きパイプのラベル付けに使用するため、コンピューター上で一意で、必要があります。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>サンプルの使用法

```console
remote /s "i386kd -v" TestSession
remote /s "cmd" "My Remote Session" /f white /b black /u Server01\Administrators
remote /s "ntsd -d -g -x" DebugIt /-v
remote /q Server01
```

 

 





