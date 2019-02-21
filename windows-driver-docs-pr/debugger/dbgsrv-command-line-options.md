---
title: DbgSrv コマンド ライン オプション
description: DbgSrv コマンドラインは、次の構文を使用します。
ms.assetid: 817f7ede-bdaf-4d4e-a1bd-579c67ea1ab9
keywords:
- DbgSrv コマンド ライン オプションの Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DbgSrv Command-Line Options
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fe270ca2f7e6fd79e87f418914becf893ec2c94d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558083"
---
# <a name="dbgsrv-command-line-options"></a>DbgSrv コマンド ライン オプション


DbgSrv コマンドラインは、次の構文を使用します。

```console
dbgsrv -t ServerTransport [-sifeo image.ext] -c[s] AppCmdLine [-x | -pc] 

dbgsrv -? 
```

すべてのオプションは、大文字小文字を区別します。

## <a name="span-idddkdbgsrvcommandlineoptionsdbgspanspan-idddkdbgsrvcommandlineoptionsdbgspanparameters"></a><span id="ddk_dbgsrv_command_line_options_dbg"></span><span id="DDK_DBGSRV_COMMAND_LINE_OPTIONS_DBG"></span>パラメーター


<span id="_______-t_______ServerTransport______"></span><span id="_______-t_______servertransport______"></span><span id="_______-T_______SERVERTRANSPORT______"></span> **-t** *サーバトランスポート*   
トランスポート プロトコルを指定します。 可能なプロトコルとの構文の一覧については*サーバトランスポート*各ケースを参照してください。 [**プロセス サーバーをアクティブ化する**](activating-a-process-server.md)します。

<span id="_______-sifeo_______Executable______"></span><span id="_______-sifeo_______executable______"></span><span id="_______-SIFEO_______EXECUTABLE______"></span> **-sifeo** *実行可能ファイル*   
指定したイメージのイメージ ファイルの実行オプション (IFEO) 値を中断します。 *実行可能*ファイル名拡張子を含む、実行可能イメージのファイル名を含める必要があります。 -Sifeo オプションは、IFEO 設定が原因の再帰呼び出しを発生させずに-c オプションで作成されたイメージの IFEO デバッガーとして設定する DbgSrv を使用できます。 このオプションは、c を使用する場合にのみ使用できます。

<span id="_______-c______"></span><span id="_______-C______"></span> **-c**   
新しいプロセスを作成する DbgSrv をによりします。 これを使用して、デバッグするプロセスを作成することができます。 点を除いて、このプロセスは、デバッガーから新しいプロセスを生成することに似ています*いない*作成時にデバッグします。 このプロセスをデバッグするその PID を判断し、使用、 **-p**オプション、このプロセスをデバッグするスマート クライアントを開始するときにします。

<span id="_______s______"></span><span id="_______S______"></span> **s**   
新しく作成されたプロセスをすぐに中断するさせます。 このオプションを使用している場合は、スマート クライアントとして CDB を使用することと-p PID と組み合わせて、-pb のコマンド ライン オプションでは、スマート クライアントを起動することをお勧めします。 デバッガーがそれにアタッチすると、プロセスが再開されます、コマンドラインで -pb オプションを含める場合使用して、プロセスを再開するそれ以外の場合、 [  **~ \*m** ](-m--resume-thread-.md)コマンド。

<span id="_______AppCmdLine______"></span><span id="_______appcmdline______"></span><span id="_______APPCMDLINE______"></span> *AppCmdLine*   
作成するプロセスの完全なコマンドラインを指定します。 *AppCmdLine* Unicode または ASCII のいずれかの文字列を使用でき、印刷可能な文字を含めることができます。 後に表示されるすべてのテキスト、 **-c**\[**s** \]パラメーターは、文字列が形成される*AppCmdLine*します。

<span id="_______-x______"></span><span id="_______-X______"></span> **-x**   
無視するコマンドラインの残りの部分をによりします。 このオプションは、アプリケーションをコマンドラインに不要なテキストを追加することがありますから DbgSrv を起動する場合に便利です。

<span id="_______-pc______"></span><span id="_______-PC______"></span> **-pc**   
無視するコマンドラインの残りの部分をによりします。 このオプションは、アプリケーションをコマンドラインに不要なテキストを追加することがありますから DbgSrv を起動する場合に便利です。 Pc が DbgSrv コマンドラインでの最後の要素の場合は、構文エラーが発生します。 Pc とは別に、この制限と同じですが、x。

<span id="_______-_______"></span> **-?**   
DbgSrv コマンドラインのヘルプ テキストを含むメッセージ ボックスが表示されます。

DbgSrv の使用方法の詳細については、次を参照してください。[プロセス サーバー (ユーザー モード)](process-servers--user-mode-.md)します。

 

 





