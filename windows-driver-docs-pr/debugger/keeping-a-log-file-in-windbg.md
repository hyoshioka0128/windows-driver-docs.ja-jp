---
title: WinDbg でのログ ファイルの保持
description: WinDbg でのログ ファイルの保持
ms.assetid: 96CFF42B-CBBB-40F7-8CD3-1CF4A538A963
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f6ca3f6e9a3a129dde33f0ce5020793483c36df
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367404"
---
# <a name="keeping-a-log-file-in-windbg"></a>WinDbg でのログ ファイルの保持


## <span id="ddk_keeping_a_log_file_dbg"></span><span id="DDK_KEEPING_A_LOG_FILE_DBG"></span>


WinDbg を記述できますログ ファイルを記録する、デバッグ セッション。 このログ ファイルには、すべての内容が含まれています、[デバッガー コマンド ウィンドウ](debugger-command-window.md)コマンドを入力して、デバッガーからの応答を含めて、します。

### <a name="span-idopeninganewlogfilespanspan-idopeninganewlogfilespanopening-a-new-log-file"></a><span id="opening_a_new_log_file"></span><span id="OPENING_A_NEW_LOG_FILE"></span>新しいログ ファイルを開く

新しいログ ファイルを開くまたは以前のログ ファイルを上書きするには、次のいずれかの操作を行います。

-   選択**開く/閉じるログ ファイル**から、**編集**メニュー。

-   使用して、WinDbg をコマンド プロンプト ウィンドウを起動すると、 **-ロゴ**コマンド ライン オプション。

-   入力、 [ **.logopen (ログ ファイルを開く)** ](-logopen--open-log-file-.md)コマンド。 使用する場合、 **/t**オプションでは、日付と時刻が、指定したファイル名に追加されます。 使用する場合、 **/u**オプション、ログ ファイルは ASCII ではなく、Unicode で書き込まれます。

### <a name="span-idappendingtoanexistinglogfilespanspan-idappendingtoanexistinglogfilespanappending-to-an-existing-log-file"></a><span id="appending_to_an_existing_log_file"></span><span id="APPENDING_TO_AN_EXISTING_LOG_FILE"></span>既存のログ ファイルに追加します。

ログ ファイルにコマンド ウィンドウのテキストを追加するには、次のいずれかの操作を行います。

-   選択**開く/閉じるログ ファイル**から、**編集**メニュー。

-   使用して、WinDbg をコマンド プロンプト ウィンドウを起動すると、 **- loga**コマンド ライン オプション。

-   入力、 [ **.logappend (ログ ファイルの追加)** ](-logappend--append-log-file-.md)コマンド。 使用する必要があります Unicode のログ ファイルに追加する場合は、 **/u**オプション。

### <a name="span-idclosingalogfilespanspan-idclosingalogfilespanclosing-a-log-file"></a><span id="closing_a_log_file"></span><span id="CLOSING_A_LOG_FILE"></span>ログ ファイルを閉じる

開いているログ ファイルを閉じるには、次のいずれかの操作を行います。

-   選択**開く/閉じるログ ファイル**から、**編集**メニュー。

-   入力、 [ **.logclose (ログ ファイルを閉じる)** ](-logclose--close-log-file-.md)コマンド。

### <a name="span-idcheckinglogfilestatusspanspan-idcheckinglogfilestatusspanchecking-log-file-status"></a><span id="checking_log_file_status"></span><span id="CHECKING_LOG_FILE_STATUS"></span>ログ ファイルの状態の確認

ログ ファイルの状態を確認するのには、次のいずれかの操作を行います。

-   選択**開く/閉じるログ ファイル**から、**編集**] メニューの [ログ ファイルが表示されているかどうかを確認します。

-   入力、 [ **.logfile (ログ ファイルの表示状態)** ](-logfile--display-log-file-status-.md)コマンド。

 

 





