---
title: TList コマンド
description: TList コマンドの構文のとおりです。
ms.assetid: d1527ffe-ea80-4e02-9a32-b6eccddc1c6a
keywords: Windows デバッグ、TList コマンド
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- TList Commands
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 314c932e87b36173a38ffe67c69fa501e3d905bc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575020"
---
# <a name="tlist-commands"></a>TList コマンド


TList コマンドの構文は次のとおりです。

```dbgcmd
tlist [/p ProcessName | PID | Pattern | /t | /c | /e | /k | /m [Module] | /s | /v
```

## <a name="span-idddktlistcommandsdtoolsspanspan-idddktlistcommandsdtoolsspanparameters"></a><span id="ddk_tlist_commands_dtools"></span><span id="DDK_TLIST_COMMANDS_DTOOLS"></span>パラメーター


<span id="_______tlist______"></span><span id="_______TLIST______"></span> **tlist**   
追加のパラメーターを指定せず TList を表示しますすべての実行中のプロセスや、プロセス id (Pid)、これらは、実行しているウィンドウのタイトル存在する場合。

<span id="________p_______ProcessName______"></span><span id="________p_______processname______"></span><span id="________P_______PROCESSNAME______"></span> **/p** *ProcessName*   
指定されたプロセスのプロセス id (PID) が表示されます。

*ProcessName* (またはファイル名拡張子を除く)、プロセスの名前を指定パターンではありません。

場合の値*ProcessName*実行中のプロセス、TList 表示-1 とは一致しません。 1 つ以上のプロセス名が一致すると、TList に最初の一致するプロセスの PID のみが表示されます。

<span id="_______PID______"></span><span id="_______pid______"></span> *PID*   
詳細については、PID で指定されたプロセスを表示します。 表示の詳細については、以下の「解説」セクションを参照してください。 プロセス ID を検索する次のように入力します。 **tlist**追加パラメーターがない場合。

<span id="_______Pattern______"></span><span id="_______pattern______"></span><span id="_______PATTERN______"></span> *パターン*   
詳細ウィンドウのタイトルまたは名前を持つ指定したパターンに一致するすべてのプロセスに関する情報を表示します。 パターンには、完全な名前または正規表現を指定できます。

<span id="________t______"></span><span id="________T______"></span> **/t**   
各プロセスが作成したプロセスの子として表示されるタスク ツリーを表示します。

<span id="________c______"></span><span id="________C______"></span> **/c**   
各プロセスを起動したコマンドラインを表示します。

<span id="________e______"></span><span id="________E______"></span> **/e**   
各プロセスのセッション識別子が表示されます。

<span id="________k______"></span><span id="________K______"></span> **/k**   
各プロセスでアクティブな COM コンポーネントを表示します。

<span id="________m_______Module______"></span><span id="________m_______module______"></span><span id="________M_______MODULE______"></span> **/m** *モジュール*   
指定された DLL または実行可能モジュールが読み込まれているタスクを一覧表示します。 モジュールには、完全なモジュール名またはモジュール名のパターンを指定できます。

<span id="________s______"></span><span id="________S______"></span> **/s**   
各プロセスでアクティブなサービスが表示されます。

<span id="________v______"></span><span id="________V______"></span> **/v**   
実行中のプロセス ID、セッション ID、ウィンドウのタイトル、コマンドライン、およびプロセスの実行中のサービスを含むプロセスの詳細が表示されます。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

プロセスの詳細の表示 (**tlist** *PID*または**tlist** *パターン*)、TList には、次の情報が表示されます。

-   プロセス ID、実行可能ファイル名、プログラムのフレンドリ名。

-   現在の作業ディレクトリ (CWD)。

-   (CmdLine) プロセスを開始したコマンドライン。

-   現在の仮想アドレス空間の値。

-   スレッドの数。

-   プロセスの実行中のスレッドの一覧。 各スレッドでは、TList スレッド ID (TID)、スレッドを実行している関数、エントリ ポイントのアドレス (ある場合) の最後の報告されたエラー、およびスレッドの状態のアドレスが表示されます。

-   プロセスのモジュールの一覧が読み込まれます。 各モジュールのバージョン番号、属性、モジュール、およびモジュールの名前の仮想アドレス TList を表示します。

使用する場合、 **/e**パラメーター、プロセスの一覧を次の条件下でのみで有効なセッションの識別子が表示されます。 それ以外の場合、セッション識別子は、ゼロ (0) です。

-   Windows 2000 および Windows Server 2003 では、少なくとも 1 つのユーザーがコンソール セッション以外のセッションに接続する必要があります。

-   Windows xp でユーザーの簡易切り替えを有効にする必要があり、1 つ以上のユーザーが非コンソール セッションに接続する必要があります。

-   Windows Vista では、場所のすべてのプロセスは既定で 2 つのターミナル サービス セッションに関連付け、少なくとも 1 人のユーザーをコンソール以外のセッションに接続する必要があります。

 

 





