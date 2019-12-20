---
title: TList コマンド
description: Tlist.exe コマンドの構文は次のとおりです。
ms.assetid: d1527ffe-ea80-4e02-9a32-b6eccddc1c6a
keywords: Tlist.exe コマンド、Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- TList Commands
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 54993a7426813020f22130bdb55c003fc249332b
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209678"
---
# <a name="tlist-commands"></a>TList コマンド


Tlist.exe コマンドの構文は次のとおりです。

```dbgcmd
tlist [/p ProcessName | PID | Pattern | /t | /c | /e | /k | /m [Module] | /s | /v
```

## <a name="span-idddk_tlist_commands_dtoolsspanspan-idddk_tlist_commands_dtoolsspanparameters"></a><span id="ddk_tlist_commands_dtools"></span><span id="DDK_TLIST_COMMANDS_DTOOLS"></span>パラメータ


<span id="_______tlist______"></span><span id="_______TLIST______"></span>**tlist.exe**   
追加のパラメーターを指定しない場合、Tlist.exe には、実行中のすべてのプロセス、プロセス識別子 (Pid)、および実行されているウィンドウのタイトル (存在する場合) が表示されます。

<span id="________p_______ProcessName______"></span><span id="________p_______processname______"></span><span id="________P_______PROCESSNAME______"></span>**/P** *ProcessName*   
指定したプロセスのプロセス識別子 (PID) が表示されます。

*ProcessName*は、パターンではなく、プロセスの名前 (ファイル名拡張子の有無にかかわらず) です。

*ProcessName*の値が実行中のどのプロセスとも一致しない場合、tlist.exe には-1 が表示されます。 複数のプロセス名と一致する場合、Tlist.exe は最初に一致したプロセスの PID のみを表示します。

<span id="_______PID______"></span><span id="_______pid______"></span>*PID*   
PID によって指定されたプロセスに関する詳細情報を表示します。 表示の詳細については、以下の「解説」セクションを参照してください。 プロセス ID を検索するには、追加のパラメーターを指定せずに**tlist.exe**と入力します。

<span id="_______Pattern______"></span><span id="_______pattern______"></span><span id="_______PATTERN______"></span>*パターン*   
指定したパターンに一致する名前またはウィンドウタイトルを持つすべてのプロセスに関する詳細情報を表示します。 パターンには、完全な名前または正規表現を使用できます。

<span id="________t______"></span><span id="________T______"></span>**/t**   
各プロセスを作成したプロセスの子として表示されるタスクツリーを表示します。

<span id="________c______"></span><span id="________C______"></span>**/c**   
各プロセスを開始したコマンドラインを表示します。

<span id="________e______"></span><span id="________E______"></span>**/e**   
各プロセスのセッション識別子を表示します。

<span id="________k______"></span><span id="________K______"></span>**/k**   
各プロセスでアクティブになっている COM コンポーネントを表示します。

<span id="________m_______Module______"></span><span id="________m_______module______"></span><span id="________M_______MODULE______"></span>**/M** *モジュール*   
指定された DLL または実行可能モジュールが読み込まれるタスクを一覧表示します。 モジュールには、モジュール名またはモジュール名の完全なパターンを指定できます。

<span id="________s______"></span><span id="________S______"></span>**/s**   
各プロセスでアクティブになっているサービスを表示します。

<span id="________v______"></span><span id="________V______"></span> **/v**   
プロセス ID、セッション ID、ウィンドウタイトル、コマンドライン、およびプロセスで実行されているサービスなど、実行中のプロセスの詳細が表示されます。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>Comments

プロセスの詳細な表示 (**Tlist.exe** *PID*または**tlist.exe** *パターン*) では、tlist.exe は次の情報を表示します。

-   プロセス ID、実行可能ファイル名、プログラムのフレンドリ名。

-   現在の作業ディレクトリ (CWD)。

-   プロセスを開始したコマンドライン (CmdLine)。

-   現在の仮想アドレス空間の値。

-   スレッド数。

-   プロセスで実行されているスレッドの一覧。 各スレッドについて、Tlist.exe はスレッド ID (TID)、スレッドが実行されている関数、エントリポイントのアドレス、最後に報告されたエラーのアドレス (存在する場合)、およびスレッドの状態を表示します。

-   プロセス用に読み込まれたモジュールの一覧。 各モジュールについて、Tlist.exe には、モジュールのバージョン番号、属性、仮想アドレス、およびモジュール名が表示されます。

**/E**パラメーターを使用する場合、有効なセッション識別子は、次の条件下でのみプロセス一覧に表示されます。 それ以外の場合、セッション識別子はゼロ (0) です。

-   Windows XP では、ユーザーの簡易切り替えが有効になっていて、複数のユーザーがコンソール以外のセッションに接続されている必要があります。

-   既定では、すべてのプロセスが2つのターミナルサービスセッションに関連付けられている Windows Vista では、少なくとも1人のユーザーがコンソール以外のセッションに接続されている必要があります。
