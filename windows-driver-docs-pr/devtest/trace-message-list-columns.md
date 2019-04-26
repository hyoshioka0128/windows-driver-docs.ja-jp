---
title: トレース メッセージ一覧の列
description: トレース メッセージ一覧の列
ms.assetid: d0f5873e-9b01-4a74-8448-90194545da1f
keywords:
- トレース メッセージの一覧 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52726498ccf71f138fe65b79af67e3a1875ff629
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354632"
---
# <a name="trace-message-list-columns"></a>トレース メッセージ一覧の列


トレース メッセージの一覧で列がトレース メッセージのプロパティを表す、もののような一般的に表示される、[トレース メッセージのプレフィックス](trace-message-prefix.md)します。 表示し、列を非表示にできますが、それらの順序を変更することはできません。

既定で、 **ID**フィールドと、次の一覧に記載されている最初の 8 列トレース メッセージの一覧に表示されます。 表示する列の選択の詳細については、表示と非表示の列を参照してください。

<span id="ID"></span><span id="id"></span>**ID**  
**ID**ウィンドウ フレームのトレース メッセージの一覧に表示されます。 表示されます、*グループ ID*トレース セッションの識別子を traceview で割り当てますトレース セッションとトレース セッションのグループにします。 **グループ ID**の最初の列にも表示されます[トレース セッション リスト](trace-session-list.md)そのトレース メッセージをトレース セッションを関連付けることができます。

<span id="Msg_"></span><span id="msg_"></span><span id="MSG_"></span>**メッセージ\#**  
トレース メッセージのメッセージの数が表示されます。 既定では、トレース メッセージの一覧が値で並べ替えられた、 **Msg\#** 列。

<span id="Name"></span><span id="name"></span><span id="NAME"></span>**名**  
フレンドリ名を表示、 [GUID をメッセージ](message-guid.md)のトレース メッセージ。 既定では、メッセージの GUID のフレンドリ名は、トレース プロバイダーが構築されたディレクトリの名前です。

[トレース セッションの NT Kernel Logger](nt-kernel-logger-trace-session.md)、この列には、メッセージ (たとえば、"FileIo") を生成したカーネル トレース サブコンポーネントの名前が表示されます。

使用することができます、 **-p**実行のパラメーター\_WPP または Tracewpp メッセージの GUID のフレンドリ名の代替値を指定します。 については、実行を参照してください。\_WPP オプション。

<span id="Process_ID"></span><span id="process_id"></span><span id="PROCESS_ID"></span>**プロセス ID**  
トレース メッセージを生成したプロセスを識別します。

<span id="Thread_ID"></span><span id="thread_id"></span><span id="THREAD_ID"></span>**スレッド ID**  
トレース メッセージを生成したスレッドを識別します。

<span id="CPU_"></span><span id="cpu_"></span>**CPU\#**  
トレース メッセージが生成された CPU を識別します。

<span id="Sequence_"></span><span id="sequence_"></span><span id="SEQUENCE_"></span>**シーケンス\#**  
トレース メッセージのローカルまたはグローバルのシーケンス番号が表示されます。 ローカルのシーケンス番号がこのトレース セッションにのみ一意では、既定値です。

<span id="System_Time"></span><span id="system_time"></span><span id="SYSTEM_TIME"></span>**システム時刻**  
トレース メッセージが生成されたときに、システムのタイマー値が表示されます。 システム タイマーには、10 ミリ秒の解像度があるために、複数のイベントは同じシステム時刻の値を持つことができます。

<span id="Message"></span><span id="message"></span><span id="MESSAGE"></span>**メッセージ**  
トレース メッセージが表示されます。

<span id="File_Name"></span><span id="file_name"></span><span id="FILE_NAME"></span>**ファイル名**  
トレース メッセージを生成したソース ファイルの名前を表示します。

<span id="Line__"></span><span id="line__"></span><span id="LINE__"></span>**行 \#**  
トレース メッセージを生成したコードの行番号を表示します。

<span id="Func_Name"></span><span id="func_name"></span><span id="FUNC_NAME"></span>**Func 名**  
トレース メッセージを生成した関数の名前が表示されます。

<span id="Kernel_Time"></span><span id="kernel_time"></span><span id="KERNEL_TIME"></span>**カーネル時間**  
トレース メッセージが生成された時点で、CPU のティック単位で、カーネル モード命令の実行の経過時間を表示します。

<span id="User_Time"></span><span id="user_time"></span><span id="USER_TIME"></span>**ユーザー時間**  
トレース メッセージが生成された時点で、CPU のティック単位でユーザー モードについては、実行の経過時間を表示します。

<span id="Indent"></span><span id="indent"></span><span id="INDENT"></span>**インデント**  
テキスト ログに書き込まれるときにトレース メッセージはインデントされませんスペースの数が表示されます。

<span id="Flags_Name"></span><span id="flags_name"></span><span id="FLAGS_NAME"></span>**フラグ名**  
名前を表示、[トレース フラグ](trace-flags.md)トレース メッセージが生成されたときにプロバイダーを有効にされました。

<span id="Level_Name"></span><span id="level_name"></span><span id="LEVEL_NAME"></span>**レベル名**  
値を表示、[トレース レベル](trace-level.md)が有効になっている、プロバイダーのトレース メッセージが生成されたとき。

<span id="Component_Name"></span><span id="component_name"></span><span id="COMPONENT_NAME"></span>**コンポーネント名**  
トレース メッセージを生成したプロバイダーのコンポーネントの名前が表示されます。 コンポーネント名では、トレース コードで指定されている場合にのみ表示されます。

<span id="SubComponent_Name"></span><span id="subcomponent_name"></span><span id="SUBCOMPONENT_NAME"></span>**サブコンポーネント名**  
トレース メッセージを生成したプロバイダーのサブコンポーネントの名前が表示されます。 サブコンポーネント名には、トレース コードで指定されている場合にのみが表示されます。

<span id="Save_As_Default"></span><span id="save_as_default"></span><span id="SAVE_AS_DEFAULT"></span>**既定値として保存します。**  
このオプションは、列名ではありません。 これは、将来のトレース セッションの既定値として現在表示されている列の構成を保存するコマンドです。 詳細についてを参照してください「、列の構成を保存しています」[トレース メッセージの一覧機能](trace-message-list-features.md)します。

 

 





