---
title: Remote クライアントの構文
description: リモートツールのクライアント側を起動するには、コマンドラインで次の構文を使用します。
ms.assetid: 4728ef17-a365-4024-815c-2719b51b81f6
keywords:
- リモートクライアント構文の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- Remote Client Syntax
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2ad54a20220119253cfcf3c894eac2a03409473d
ms.sourcegitcommit: d2dab8b8bf335835d0341ca3f0a36eab0ec028f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72892687"
---
# <a name="remote-client-syntax"></a>Remote クライアントの構文
リモートツールのクライアント側を起動するには、コマンドラインで次の構文を使用します。

```console
remote /c Server SessionName [/L Lines] [/f] [/b] [/k ColorFile] 
```

## <a name="span-idparametersspanspan-idparametersspanparameters"></a><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ

<span id="________c______"></span><span id="________C______"></span> **/c**   
クライアントをリモートセッションに接続します。

<span id="_______Server______"></span><span id="_______server______"></span><span id="_______SERVER______"></span>*サーバー*   
セッションを確立したサーバーのコンピューター名を指定します。

<span id="_______SessionName______"></span><span id="_______sessionname______"></span><span id="_______SESSIONNAME______"></span>*セッション名*   
リモートセッションの名前を指定します。 このパラメーターでは、大文字と小文字は区別されません。

<span id="________L_______Lines______"></span><span id="________l_______lines______"></span><span id="________L_______LINES______"></span> **/L** *行*   
コンソール画面からクライアントコンピューターに送信される行の数を指定します。 既定値は200行です。 *行*は10進数です。

<span id="________f______"></span><span id="________F______"></span> **/f**   
サーバーコマンドウィンドウ内のテキストの色を指定します。

<span id="________b______"></span><span id="________B______"></span> **/b**   
サーバーコマンドウィンドウの背景色を指定します。

<span id="_______Color______"></span><span id="_______color______"></span><span id="_______COLOR______"></span>*色*の   
色を指定します。 有効な値は、黒、青、緑、シアン、赤、紫、黄、白、lblack、lblack、lblack、lblack、lblack、lblack、および lblack です。

<span id="________k_______ColorFile______"></span><span id="________k_______colorfile______"></span><span id="________K_______COLORFILE______"></span> **/K** *colorfile*   
クライアントコンピューターで出力を表示するときの色を指定する、書式設定されたテキストファイルのパス (省略可能) と名前を示します。

カラーファイルは、出力のキーワードとテキストの色を関連付けます。 キーワードが出力行に表示されると、リモートツールによって、関連付けられているテキストの色がその行に適用されます。 ファイルの形式については、「解説」を参照してください。

<span id="________q_______Computer______"></span><span id="________q_______computer______"></span><span id="________Q_______COMPUTER______"></span> **/Q** *コンピューター*   
指定したコンピューターで使用可能なリモートセッションを表示します。 表示されているセッションだけが一覧に表示されます。 (「[**リモートサーバー構文**](remote-server-syntax.md)」の「 **/v** 」を参照してください)。

## <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>Comments

*サーバー*と*セッション*のパラメーターは、構文行に示されている順序で表示される必要があります。

リモートセッションから切断するには、「 <strong>@q</strong>」と入力します。 詳細については、「[リモートセッションのコマンド](remote-session-commands.md)」を参照してください。

**キーワードカラーファイル。** キーワードカラーファイルの形式は次のとおりです。 キーワードインタープリターでは大文字と小文字が区別されません。

キーワードまたは語句は、単独で行に表示されます。 次の構文に示すように、そのキーワードに関連付けられている色は、次の行に単独で表示されます。

```text
Keyword
TextColor[, BackgroundColor]
```

たとえば、次のファイルでは、"error" という単語が黒の背景に薄い赤で表示されるようにリモートに指示しています。明るい青に "warning" という単語が含まれている行 (既定の背景) と、既定の背景に明るい緑の語句 "Windows Vista" を含む行を表示する場合は。

```text
ERROR
black, lred
WARNING
lblue
Windows Vista
lgreen
```

## <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>使用例

```console
remote /c Server01 TestSession
remote /c Domain1\ComputerA0 "cmd" "My Remote Session"
remote /c Server01 TestSession /L 50 /f black /b white /k c:\remote_file.txt
remote /q Server01
```
