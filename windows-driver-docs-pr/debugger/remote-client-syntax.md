---
title: Remote クライアントの構文
description: リモート ツールのクライアント側を起動するには、コマンドラインで、次の構文を使用します。
ms.assetid: 4728ef17-a365-4024-815c-2719b51b81f6
keywords:
- リモート クライアントの構文の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- Remote Client Syntax
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9779e7350a34fc4ced0b9750649d9acceb22b792
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581616"
---
# <a name="remote-client-syntax"></a>Remote クライアントの構文


リモート ツールのクライアント側を起動するには、コマンドラインで、次の構文を使用します。

```console
remote /c Server SessionName [/L Lines] [/f] [/b] [/k ColorFile] 
```

## <a name="span-idddkremoteclientsyntaxdtoolsspanspan-idddkremoteclientsyntaxdtoolsspanparameters"></a><span id="ddk_remote_client_syntax_dtools"></span><span id="DDK_REMOTE_CLIENT_SYNTAX_DTOOLS"></span>パラメーター


<span id="________c______"></span><span id="________C______"></span> **/c**   
クライアントは、リモート セッションに接続します。

<span id="_______Server______"></span><span id="_______server______"></span><span id="_______SERVER______"></span> *サーバー*   
セッションが確立されているサーバーのコンピューター名を指定します。

<span id="_______SessionName______"></span><span id="_______sessionname______"></span><span id="_______SESSIONNAME______"></span> *SessionName*   
リモート セッションの名前を指定します。 このパラメーターは区別されません。

<span id="________L_______Lines______"></span><span id="________l_______lines______"></span><span id="________L_______LINES______"></span> **/L** *行*   
コンソールの表示から、クライアント コンピューターに送信される行の数を指定します。 既定値は、200 の行です。 *行*は 10 進数です。

<span id="________f______"></span><span id="________F______"></span> **/f**   
サーバーのコマンド ウィンドウで、テキストの色を指定します。

<span id="________b______"></span><span id="________B______"></span> **/b**   
サーバーのコマンド ウィンドウの背景色を指定します。

<span id="_______Color______"></span><span id="_______color______"></span><span id="_______COLOR______"></span> *色*   
色を指定します。 有効な値は黒、青、緑、シアン、赤、紫、黄色、白、lblack、lblue、lgreen、lred、lpurple、lyellow、および lwhite は。

<span id="________k_______ColorFile______"></span><span id="________k_______colorfile______"></span><span id="________K_______COLORFILE______"></span> **/k** *ColorFile*   
(省略可能) のパスを指定し、クライアント コンピューターの出力を表示するための色を指定する書式設定されたテキスト ファイルの名前。

色のファイルは、テキストの色を出力に含まれるキーワードを関連付けます。 キーワードは、出力の行に表示されたら、リモート ツールには、その行に関連付けられているテキストの色が適用されます。 ファイルの形式は、「解説」を参照してください。

<span id="________q_______Computer______"></span><span id="________q_______computer______"></span><span id="________Q_______COMPUTER______"></span> **/q** *コンピューター*   
指定したコンピューター上には、使用可能なリモート セッションを表示します。 一覧に表示されているセッションのみが表示されます。 (を参照してください **/v**で[**リモート サーバー構文**](remote-server-syntax.md))。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

*Server*と*SessionName*構文行に示されている順序でパラメーターを表示する必要があります。

リモート セッションから切断して、次のように入力します。  <strong>@q</strong>します。 詳細については、次を参照してください。[リモート セッションのコマンド](remote-session-commands.md)します。

**キーワードの色のファイルです。** キーワード ファイルの形式は次のとおりです。 キーワード インタープリターは大文字小文字が区別されません。

キーワードまたは語句を単独で行が表示されます。 そのキーワードに関連付けられている色では、次の行に単独で表示、構文に示すように。

```text
Keyword
TextColor[, BackgroundColor]
```

たとえば、次のファイルに指示、ライトの赤い背景に黒のテキストに"error"という単語が含まれる行を表示するリモート薄い青 (既定バック グラウンド) 上で、既定の背景に明るい緑の"Windows Vista"という語句を含む行には、「警告」という単語を含む行を表示します。

```text
ERROR
black, lred
WARNING
lblue
Windows Vista
lgreen
```

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>サンプルの使用法

```console
remote /c Server01 TestSession
remote /c Domain1\ComputerA0 "cmd" "My Remote Session"
remote /c Server01 TestSession /L 50 /f black /b white /k c:\remote_file.txt
remote /q Server01
```

 

 





