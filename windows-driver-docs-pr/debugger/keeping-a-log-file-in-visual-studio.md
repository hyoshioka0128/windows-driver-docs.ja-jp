---
title: Visual Studio でのログ ファイルの保持
description: Windows デバッガーを記述できますログ ファイルを記録する、デバッグ セッション。
ms.assetid: 6A7588D0-A477-4BE9-874F-3AFB52561903
ms.date: 05/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: e8582538ca8d533a0d82f136d0a19b76ed339411
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361303"
---
# <a name="keeping-a-log-file-in-visual-studio"></a>Visual Studio でのログ ファイルの保持

> [!IMPORTANT]
> この機能は、Windows 10 バージョン 1507、以降のバージョンの WDK でご利用いただけません。
>


Windows デバッガーを記述できますログ ファイルを記録する、デバッグ セッション。 このログ ファイルには、すべてのコマンドを入力して、デバッガーからの応答が含まれています。 Microsoft Visual studio で、追加するを開いて、デバッガーのイミディ エイト ウィンドウでコマンドを入力してログ ファイルを閉じます。

このトピックで示す手順では、Visual Studio に統合された Windows Driver Kit が必要です。 統合環境を取得するには、最初に、Visual Studio をインストールし、Windows Driver Kit (WDK) をインストールします。 詳細については、次を参照してください。 [Windows ドライバー開発](https://docs.microsoft.com/windows-hardware/drivers/)します。

## <span id="ddk_keeping_a_log_file_dbg"></span><span id="DDK_KEEPING_A_LOG_FILE_DBG"></span>


デバッガーのイミディ エイト ウィンドウが開いてからない場合、**デバッグ** メニューの 選択**Windows&gt;イミディ エイト**します。

### <a name="span-idopeninganewlogfilespanspan-idopeninganewlogfilespanopening-a-new-log-file"></a><span id="opening_a_new_log_file"></span><span id="OPENING_A_NEW_LOG_FILE"></span>新しいログ ファイルを開く

新しいログ ファイルを開くには、入力、 [ **.logopen (ログ ファイルを開く)** ](-logopen--open-log-file-.md)コマンド。 使用する場合、 **/t**オプションでは、日付と時刻が、指定したファイル名に追加されます。 使用する場合、 **/u**オプション、ログ ファイルは ASCII ではなく、Unicode で書き込まれます。

### <a name="span-idappendingtoanexistinglogfilespanspan-idappendingtoanexistinglogfilespanappending-to-an-existing-log-file"></a><span id="appending_to_an_existing_log_file"></span><span id="APPENDING_TO_AN_EXISTING_LOG_FILE"></span>既存のログ ファイルに追加します。

既存のログ ファイルにテキストを追加するには、入力、 [ **.logappend (ログ ファイルの追加)** ](-logappend--append-log-file-.md)コマンド。 使用する必要があります Unicode のログ ファイルに追加する場合は、 **/u**オプション。

### <a name="span-idclosingalogfilespanspan-idclosingalogfilespanclosing-a-log-file"></a><span id="closing_a_log_file"></span><span id="CLOSING_A_LOG_FILE"></span>ログ ファイルを閉じる

開いているログ ファイルを閉じるには、入力、 [ **.logclose (ログ ファイルを閉じる)** ](-logclose--close-log-file-.md)コマンド。

### <a name="span-idcheckinglogfilestatusspanspan-idcheckinglogfilestatusspanchecking-log-file-status"></a><span id="checking_log_file_status"></span><span id="CHECKING_LOG_FILE_STATUS"></span>ログ ファイルの状態の確認

ログ ファイルの状態を判定するには、入力、 [ **.logfile (ログ ファイルの表示状態)** ](-logfile--display-log-file-status-.md)コマンド。

 

 





