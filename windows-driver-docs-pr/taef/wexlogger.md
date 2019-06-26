---
title: WexLogger
description: WexLogger
ms.assetid: D9F4AD08-19EA-4a6c-AD25-886FBEA334B8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7dfce409c3ee6e3de49ac8ddf1ea8c308caa8c3d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384487"
---
# <a name="wexlogger"></a>WexLogger


WexLogger では、ネイティブ コード、マネージ コードおよびスクリプトにわたるログ記録を一貫性のある API を提供します。 また、長距離のストレス テストまで、コマンド プロンプトで単体テストの実行からも拡張できます。

## <a name="logging-through-the-verify-framework"></a>経由のログオン、フレームワークを確認します。


テスト ケース内のほとんどのログ記録を使用して実行する必要があります、[確認](verify.md)フレームワーク。 これにより、テストが、わかりやすくより順次、人間が判読できる方法で作成されたことが保証されます。 ただし、場合によっては、テストの作成者を見つけるために必要なログに書き込まれた内容の周囲をより細かく制御します。 そのため WexLogger API の必要性。

## <a name="logging-within-taef"></a>TAEF 内でログ記録


TAEF 内で実行されているテスト_ケースはありませんロガーの初期化に必要なテストの作成者です。 テストを作成している言語に公開されているログ API を使用してすぐに開始することができます。

ネイティブの C++ コードには、次のように表示されます。

```cpp
using namespace WEX::Logging;
using namespace WEX::Common;
Log::Comment(L"Rendering to the BufferView");
Log::Comment(L"Render succeeded");

Log::Comment(String().Format(L"Look, a number! %d", aNumber));

#define LOG_OUTPUT(fmt, ...) Log::Comment(String().Format(fmt, __VA_ARGS__))
LOG_OUTPUT(L"Look, a number! %d", aNumber);
```

マネージ コードには、次のように表示されます。

```cpp
Log.Comment("Rendering to the BufferView");
Log.Comment("Render succeeded");
```

JScript では、このようなに表示されます。

```cpp
var log = new ActiveXObject("WEX.Logger.Log");
log.Comment("Rendering to the BufferView");
log.Comment("Render succeeded");
```

## <a name="logging-outside-taef"></a>外部 TAEF をログ記録


初期化と完了のログ記録、時間の大部分は、WexLogger、前述のように、テスト_ケースの間使用できるようになり、適切に終了が TAEF で実行されます。 ただし場合は、クライアントは、外部 TAEF WexLogger を使用するには、それらを担当する手動で呼び出す**LogController::InitializeLogging()** と**LogController::FinalizeLogging()** します。 この要件が存在するネイティブおよびマネージ コードだけです。スクリプトでは、この追加要件はありません。 LogController API の詳細については、次の表 LogController の静的メソッドを参照してください。

参照してください、 [WTT ログを生成する](#generating-wtt-logs)TAEF 外 WTT ログを生成する方法についてのセクション。

## <a name="wexlogger-api"></a>WexLogger API


**使用可能な C++ のログは、ネイティブ メソッドの一覧を次に示します。**

同等のバージョンはマネージ コードとスクリプトを使用できます。

| ネイティブ C++ のログ メソッド                                                                                                              | 機能                                                                                                                                                                                |
|-------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| アサート (const wchar\_t\* pszAssert)                                                                                                  | テストのアサートをログインします。                                                                                                                                                                           |
| Assert(const wchar\_t\* pszAssert, const wchar\_t\* pszContext)                                                                     | テスト アサートをコンテキストにログインします。                                                                                                                                                             |
| Assert(const wchar\_t\* pszAssert, const wchar\_t\* pszFile, const wchar\_t\* pszFunction, int line)                                | テストのログは、ファイル、関数、および行情報をアサートします。                                                                                                                                  |
| Assert(const wchar\_t\* pszAssert, const wchar\_t\* pszContext, const wchar\_t\* pszFile, const wchar\_t\* pszFunction, int line)   | テスト assert、コンテキスト、およびも、ファイルの関数と行情報をログに記録します。                                                                                                               |
| Bug(const wchar\_t\* pszBugDatabase, int bugId)                                                                                     | 既知のバグの数を記録します。                                                                                                                                                                      |
| Bug(const wchar\_t\* pszBugDatabase, int bugId, const wchar\_t\* pszContext)                                                        | 既知のバグ数をコンテキストにログインします。                                                                                                                                                        |
| コメント (const wchar\_t\* pszComment)                                                                                                | コメントのテストを記録します。                                                                                                                                                                          |
| Comment(const wchar\_t\* pszComment, const wchar\_t\* pszContext)                                                                   | ログのコンテキストでのテスト コメント                                                                                                                                                             |
| EndGroup (const wchar\_t\* pszGroupName)                                                                                             | テスト、または特定のテストのグループの最後にログインします。                                                                                                                                      |
| EndGroup(const wchar\_t\* pszGroupName, const wchar\_t\* pszContext)                                                                | テスト、または特定のテストのグループの末尾をコンテキストにログインします。                                                                                                                        |
| Error(const wchar\_t\* pszError)                                                                                                    | テストのエラー ログに記録します。                                                                                                                                                                            |
| Error(const wchar\_t\* pszError, const wchar\_t\* pszContext)                                                                       | テスト エラーをコンテキストにログインします。                                                                                                                                                              |
| Error(const wchar\_t\* pszError, const wchar\_t\* pszFile, const wchar\_t\* pszFunction, int line)                                  | テスト エラーをログ ファイル、関数、および行情報を使用します。                                                                                                                                   |
| Error(const wchar\_t\* pszError, const wchar\_t\* pszContext, const wchar\_t\* pszFile, const wchar\_t\* pszFunction, int line)     | テスト エラーをコンテキスト、およびも、ファイルの関数と行情報でログインします。                                                                                                                |
| File(const wchar\_t\* pszFileName)                                                                                                  | テスト ファイルを保存するログに記録します。 ファイルがいずれかに保存&lt;WTTRunWorkingDir&gt;\\WexLogFileOutput (WTTRunWorkingDir が設定されている) 場合、または&lt;CurrentDirectory\\&gt;WexLogFileOutput します。               |
| File(const wchar\_t\* pszFileName, const wchar\_t\* pszContext)                                                                     | ログのコンテキストに保存するテスト ファイルです。 ファイルがいずれかに保存&lt;WTTRunWorkingDir&gt;\\WexLogFileOutput (WTTRunWorkingDir が設定されている) 場合、または&lt;CurrentDirectory\\&gt;WexLogFileOutput します。 |
| Property(const wchar\_t\* pszName, const wchar\_t\* pszValue)                                                                       | プロパティの名前と値のペアにログインします。 値は、xml 形式であることができます。                                                                                                                              |
| Property(const wchar\_t\* pszName, const wchar\_t\* pszValue, const wchar\_t\* pszContext)                                          | 名前/値のプロパティのペアをコンテキストにログインします。 値は、xml 形式であることができます。                                                                                                                |
| 結果 (TestResults::Result testResult)                                                                                              | テストの結果をログに記録します。                                                                                                                                                                           |
| Result(TestResults::Result testResult, const wchar\_t\* pszComment)                                                                 | テスト結果を関連付けられているコメントにログインします。                                                                                                                                                |
| Result(TestResults::Result testResult, const wchar\_t\* pszComment, const wchar\_t\* pszContext)                                    | テスト結果をログイン コンテキストに関連付けられているコメントを使用します。                                                                                                                                  |
| StartGroup (const wchar\_t\* pszGroupName)                                                                                           | テスト、または特定のテストのグループの先頭にログインします。                                                                                                                                    |
| StartGroup(const wchar\_t\* pszGroupName, TestResults::Result defaultTestResult)                                                    | ログのテスト、または特定のテストのグループの開始また、既定のテスト結果を設定します。                                                                                                 |
| StartGroup(const wchar\_t\* pszGroupName, const wchar\_t\* pszContext)                                                              | テスト、または特定のテストのグループの開始をコンテキストにログインします。                                                                                                                      |
| StartGroup(const wchar\_t\* pszGroupName, const wchar\_t\* pszContext, TestResults::Result defaultTestResult)                       | ログのテスト、または特定のテストのグループの開始また、既定のテスト結果を設定します。                                                                                                 |
| 警告 (const wchar\_t\* pszWarning)                                                                                                | テストの警告を記録します。                                                                                                                                                                          |
| Warning(const wchar\_t\* pszWarning, const wchar\_t\* pszContext)                                                                   | テストの警告をコンテキストにログインします。                                                                                                                                                            |
| Warning(const wchar\_t\* pszWarning, const wchar\_t\* pszFile, const wchar\_t\* pszFunction, int line)                              | テストの警告をファイル、関数と行情報でログインします。                                                                                                                                 |
| Warning(const wchar\_t\* pszWarning, const wchar\_t\* pszContext, const wchar\_t\* pszFile, const wchar\_t\* pszFunction, int line) | コンテキスト、およびも、ファイルの関数と行情報をテストの警告では、ログに記録します。                                                                                                              |
| Xml (const wchar\_t\* pszXml)                                                                                                        | Xml データを記録します。 適切な形式であることを確認するチェックは行われません。                                                                                                                             |
| Xml(const wchar\_t\* pszXml, const wchar\_t\* pszContext)                                                                           | Xml データをコンテキストにログインします。 適切な形式であることを確認するチェックは行われません。                                                                                                               |
| MiniDump()                                                                                                                          | 現在のプロセスのミニ ダンプをログインします。                                                                                                                                                           |



**注:** 「コンテキスト」を行うことができます必要に応じて追加の文字列とは、 **WexLogger**コンテキストまたは詳細の詳細を提供する API 呼び出し。 たとえば、することができます"ImageComparator"で、常に渡すのコンテキストとしていずれかを行うときに**WexLogger** ImageComparator クラスのメソッドからの API 呼び出し。

ネイティブ C++ の有効な値をここでは**TestResults::Result**列挙体。 同等のバージョンはマネージ コードとスクリプトを使用できます。

| ネイティブの C++ TestResults::Result 列挙型 | 機能        |
|--------------------------------------------|----------------------|
| 渡されました。                                     | テストに合格しました      |
| NotRun                                     | テストが実行されていません |
| スキップされました                                    | テストがスキップされました |
| ブロック                                    | テストがブロックされました |
| Failed                                     | テストが失敗しました      |



**使用可能なネイティブの C++ LogContoller メソッドの一覧を次に示します。**

| ネイティブの C++ LogController メソッド                                                                       | 機能                                                                                                                                                                                                                                                                                                   |
|--------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 静的な HRESULT InitializeLogging()                                                                     | ログ記録機能を初期化します。                                                                                                                                                                                                                                                                               |
| 静的な HRESULT InitializeLogging(WexLoggerErrorCallback pfnErrorCallback)                              | ログ記録の機能を初期化し、ロガーの内部エラーの通知を使用する WexLoggerErrorCallback 関数を指定します。                                                                                                                                                               |
| 静的な HRESULT InitializeLogging(const wchar\_t\* pszLogName)                                          | ログ記録の機能を初期化し、使用するには、ログ ファイルの名前を指定します。 **注:** 場合、アカウントにログの名前が考慮のみ[WttLogging が有効になっている](#generating-wtt-logs)します。                                                                                                             |
| 静的な HRESULT InitializeLogging(const wchar\_t\* pszLogName, WexLoggerErrorCallback pfnErrorCallback) | ログ記録機能を初期化、ロガーの内部エラーの通知を使用する WexLoggerErrorCallback 関数を指定し、使用するログ ファイルの名前を指定します。 **注:** 場合、アカウントにログの名前が考慮のみ[WttLogging が有効になっている](#generating-wtt-logs)します。 |
| static bool IsInitialized()                                                                            | このプロセスの LogController が初期化されているかどうかを返します。                                                                                                                                                                                                                                 |
| static const unsigned short\* GetLogName()                                                             | (ある場合)、InitializeLogging 呼び出しのログで指定された名前を返します。                                                                                                                                                                                                                         |
| 静的な HRESULT FinalizeLogging()                                                                       | ログ記録機能を完了します。                                                                                                                                                                                                                                                                                   |



**注:** 詳細については以下の C++ エラー処理セクションを参照してください、 **WexLoggerErrorCallback**メカニズムと TAEF framework 外の使用方法。

**注:** 使用する場合は、InitializeLogging/FinalizeLogging を呼び出す必要は、 **WexLogger** TAEF framework の外部 TAEF として既に処理初期化/補完がログ記録します。

**注:** 完了に必要な初期化/ログ記録機能を使用する場合は、 **WexLogger**スクリプトから。

**使用可能なネイティブの C++ RemoteLogContoller メソッドの一覧を次に示します。**

| ネイティブの C++ RemoteLogController メソッド                                                                             | 機能                                                                                                                                                                                                |
|--------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 静的な HRESULT GenerateConnectionData(WEX::Common::NoThrowString& connectionData)                                  | 子プロセスは、親プロセスにログインできるようにする、親と子のプロセス内で使用する必要があります接続データを生成します。                                                          |
| 静的な HRESULT GenerateConnectionData(const wchar\_t\* pszMachineName, WEX::Common::NoThrowString& connectionData) | リモート コンピューター上の子プロセスを起動するときに使用されます。 子プロセスは、親プロセスにログインできるようにする、親と子のプロセス内で使用する必要があります接続データを生成します。 |
| 静的な HRESULT InitializeLogging(WEX::Common::NoThrowString connectionData)                                        | 子プロセスは、返送にログインできるように、親プロセス内の機能をログ記録を初期化します。                                                                                                         |



**注:** 参照してください、[リモート ログ記録から子プロセス](#remote-logging-from-child-processes)リモート ログ記録の詳細については後述します。

使用可能なログの管理対象のメソッドの一覧を次に示します。

| 管理対象のログ メソッド                                                             | 機能                                                                                                                                                                |
|---------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| アサート (IFormatProvider プロバイダー、文字列の形式、params オブジェクト\[\] args)         | カルチャに固有の書式設定情報プロバイダー、書式指定文字列、および書式指定する 0 個以上のオブジェクトを格納しているオブジェクト配列を使用して、テストのアサートのログです。               |
| アサート (IFormatProvider プロバイダー、文字列の形式、params オブジェクト\[\] args)         | カルチャに固有の書式設定情報プロバイダー、書式指定文字列、および書式指定する 0 個以上のオブジェクトを格納しているオブジェクト配列を使用して、テストのアサートのログです。               |
| (文字列メッセージ) のアサートします。                                                          | テストのアサートをログインします。                                                                                                                                                           |
| (文字列の形式、オブジェクトの arg0) をアサートします。                                              | テストのログをアサートする書式指定文字列とオブジェクトを使用してフォーマットします。                                                                                                             |
| アサート (文字列の形式、params オブジェクト\[\] args)                                   | ログ形式の文字列を使用して、テストのアサートと書式指定する 0 個以上のオブジェクトを格納しているオブジェクト配列。                                                                   |
| (文字列コンテキストで、文字列メッセージ) のアサートします。                                          | テスト アサートをコンテキストにログインします。                                                                                                                                             |
| Assert (メッセージ文字列、文字列のファイル、文字列関数、int 行)                  | テスト、assert ともファイル、関数と行情報をログに記録します。                                                                                                             |
| Assert (メッセージ文字列、文字列のコンテキスト、文字列のファイル、文字列関数、int 行)  | テスト assert、コンテキスト、およびも、ファイルの関数と行情報をログに記録します。                                                                                               |
| バグ (文字列 bugDatabase、int 型には)                                              | 既知のバグの数を記録します。                                                                                                                                                      |
| Bug(string bugDatabase, int bugId, string context)                              | 既知のバグ数をコンテキストにログインします。                                                                                                                                        |
| コメント (IFormatProvider プロバイダー、文字列の形式、params オブジェクト\[\] args)        | コメントをカルチャに固有の書式設定情報プロバイダー、書式指定文字列、および書式指定する 0 個以上のオブジェクトを格納しているオブジェクト配列を使用してテスト ログに記録します。              |
| コメント (文字列メッセージ)                                                         | コメントは、テストのログ                                                                                                                                                           |
| コメント (文字列の形式、オブジェクトの arg0)                                             | 書式指定文字列とオブジェクトを使用してフォーマットするコメントのテストを記録します。                                                                                                            |
| コメント (文字列の形式、params オブジェクト\[\] args)                                  | コメントを書式指定文字列と書式指定する 0 個以上のオブジェクトを格納しているオブジェクト配列を使用してテスト ログに記録します。                                                                   |
| コメント (メッセージ文字列, 文字列コンテキストで)                                         | ログのコンテキストでのテスト コメント                                                                                                                                             |
| EndGroup (文字列 groupName)                                                      | テスト、または特定のテストのグループの最後にログインします。                                                                                                                      |
| EndGroup (文字列のグループ名、文字列のコンテキスト)                                      | テスト、または特定のテストのグループの末尾をコンテキストにログインします。                                                                                                        |
| エラー (IFormatProvider プロバイダー、文字列の形式、params オブジェクト\[\] args)          | カルチャに固有の書式設定情報プロバイダー、書式指定文字列、および書式指定する 0 個以上のオブジェクトを格納しているオブジェクト配列を使用して、テストのエラー ログに記録します。                |
| エラー (文字列メッセージ)                                                           | テストのエラー ログに記録します。                                                                                                                                                            |
| エラー (文字列の形式、オブジェクトの arg0)                                               | 書式指定文字列とオブジェクトを使用してフォーマットするテストのエラー ログに記録します。                                                                                                              |
| エラー (メッセージ文字列, 文字列コンテキストで)                                           | テスト エラーをコンテキストにログインします。                                                                                                                                              |
| エラー (IFormatProvider プロバイダー、文字列の形式、params オブジェクト\[\] args)          | 書式指定文字列と書式指定する 0 個以上のオブジェクトを格納しているオブジェクト配列を使用して、テストのエラー ログに記録します。                                                                     |
| エラー (メッセージ文字列, 文字列ファイル、文字列関数, int 行)                   | テスト エラーをログ ファイル、関数、および行情報を使用します。                                                                                                                   |
| エラー (メッセージ文字列、文字列のコンテキスト、文字列のファイル、文字列関数、int 行)   | テスト エラーをコンテキスト、およびも、ファイルの関数と行情報でログインします。                                                                                                |
| File(string fileName)                                                           | テスト ファイルを保存するログに記録します。 ファイルか WTTRunWorkingDir に保存されます\\WexLogFileOutput (WTTRunWorkingDir が設定されている) 場合、または CurrentDirectory\\WexLogFileOutput します。               |
| File(string fileName, string context)                                           | ログのコンテキストに保存するテスト ファイルです。 ファイルか WTTRunWorkingDir に保存されます\\WexLogFileOutput (WTTRunWorkingDir が設定されている) 場合、または CurrentDirectory\\WexLogFileOutput します。 |
| MiniDump()                                                                      | 現在のプロセスのミニ ダンプをログインします。                                                                                                                                           |
| プロパティ (文字列名、文字列値)                                             | プロパティの名前と値のペアにログインします。 値は、xml 形式であることができます。                                                                                                              |
| プロパティ (文字列名、文字列値、文字列のコンテキスト)                             | 名前/値のプロパティのペアをコンテキストにログインします。 値は、xml 形式であることができます。                                                                                                |
| 結果 (TestResult testResult)                                                   | テストの結果をログに記録します。                                                                                                                                                           |
| 結果 (TestResult testResult、文字列のコメント)                                   | テスト結果を関連付けられているコメントにログインします。                                                                                                                                |
| 結果 (TestResult testResult、文字列のコメント、文字列のコンテキスト)                   | テスト結果をログイン コンテキストに関連付けられているコメントを使用します。                                                                                                                  |
| StartGroup (文字列 groupName)                                                    | テスト、または特定のテストのグループの先頭にログインします。                                                                                                                    |
| StartGroup (文字列のグループ名、文字列のコンテキスト)                                    | テスト、または特定のテストのグループの開始をコンテキストにログインします。                                                                                                      |
| 警告 (IFormatProvider プロバイダー、文字列の形式、params オブジェクト\[\] args)        | カルチャに固有の書式設定情報プロバイダー、書式指定文字列、および書式指定する 0 個以上のオブジェクトを格納しているオブジェクト配列を使用して、テスト警告を記録します。              |
| 警告 (メッセージの文字列)                                                         | テストの警告を記録します。                                                                                                                                                          |
| 警告 (文字列の形式、オブジェクトの arg0)                                             | 書式指定文字列とオブジェクトを使用してフォーマットするテストの警告をログします。                                                                                                            |
| 警告 (文字列の形式、params オブジェクト\[\] args)                                  | 書式指定文字列と書式指定する 0 個以上のオブジェクトを格納しているオブジェクト配列を使用してテストの警告を記録します。                                                                   |
| 警告 (メッセージ文字列, 文字列コンテキストで)                                         | テストの警告をコンテキストにログインします。                                                                                                                                            |
| 警告 (メッセージ文字列, 文字列ファイル、文字列関数, int 行)                 | テストの警告をファイル、関数と行情報でログインします。                                                                                                                 |
| 警告 (メッセージ文字列、文字列のコンテキスト、文字列のファイル、文字列関数、int 行) | コンテキスト、およびも、ファイルの関数と行情報をテストの警告では、ログに記録します。                                                                                              |
| Xml(string xmlData)                                                             | Xml データを記録します。 適切な形式であることを確認するチェックは行われません。                                                                                                             |
| Xml (文字列 xmlData、文字列のコンテキスト)                                             | Xml データをコンテキストにログインします。 適切な形式であることを確認するチェックは行われません。                                                                                               |



**使用可能なマネージ LogContoller メソッドの一覧を次に示します。**

| マネージ LogController メソッド                 | 機能                                                                                                                                                                                       |
|-----------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| static void InitializeLogging()               | ログ記録機能を初期化します。                                                                                                                                                                   |
| static void InitializeLogging (文字列 logName) | ログ記録の機能を初期化し、使用するには、ログ ファイルの名前を指定します。 **注:** 場合、アカウントにログの名前が考慮のみ[WttLogging が有効になっている](#generating-wtt-logs)します。 |
| static bool IsInitialized()                   | このプロセスの LogController が初期化されているかどうかを返します。                                                                                                                     |
| static String GetLogName()                    | (ある場合)、InitializeLogging 呼び出しのログで指定された名前を返します。                                                                                                             |
| static void FinalizeLogging()                 | ログ記録機能を完了します。                                                                                                                                                                       |



**注:** 管理対象レイヤーを使用する場合、エラーと例外を処理する方法の詳細については、以下の「マネージ コードのエラーと例外を参照してください、 **WexLogger** TAEF framework 外です。

**注:** 使用する場合は、InitializeLogging/FinalizeLogging を呼び出す必要は、 **WexLogger** TAEF framework の外部 TAEF として既に処理初期化/補完がログ記録します。

**注:** 完了に必要な初期化/ログ記録機能を使用する場合は、 **WexLogger**スクリプトから。

**使用可能なマネージ RemoteLogContoller メソッドの一覧を次に示します。**

| マネージ RemoteLogController メソッド                      | 機能                                                                                                                                                                                                |
|----------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 静的文字列 GenerateConnectionData()                   | 子プロセスは、親プロセスにログインできるようにする、親と子のプロセス内で使用する必要があります接続データを生成します。                                                          |
| 静的文字列 GenerateConnectionData(string machineName) | リモート コンピューター上の子プロセスを起動するときに使用されます。 子プロセスは、親プロセスにログインできるようにする、親と子のプロセス内で使用する必要があります接続データを生成します。 |
| static void InitializeLogging (文字列 connectionData)     | 子プロセスは、返送にログインできるように、親プロセス内の機能をログ記録を初期化します。                                                                                                         |



**注:** 参照してください、[リモート ログ記録から子プロセス](#remote-logging-from-child-processes)リモート ログ記録の詳細については後述します。

## <a name="remote-logging-from-child-processes"></a>子プロセスからリモート ログ記録


ログに複数の子プロセスが 1 つのログ ファイル内で統合されたテスト結果の生成の結果として、1 つの親プロセスをまたは WexLogger が 1 つの機能を提供します。

子プロセスを親プロセスと同じコンピューター上または別のコンピューターにリモートで実行できることができます。 リモート コンピューターを操作するログに記録、リモート コンピューターのすべての子プロセスの TCP ファイアウォールの除外を追加する WexLogger クライアントの責任です。 ただし、子プロセスを親と同じコンピューターで実行している場合は、ファイアウォールの変更は必要ありません。

次の手順では、各リモート ログ記録の接続を設定する必要があります。

**親プロセス**

1.  呼び出す**RemoteLogController::GenerateConnectionData()** ログ接続を開始するプロセスの両方で使用する必要があります接続データを生成します。

    **注:** この呼び出しの戻り値を確認してください。

    ```cpp
        NoThrowString connectionData;
        Throw::IfFailed(RemoteLogController::GenerateConnectionData(connectionData));

    ```

2.  その環境ブロックに設定することで、またはコマンド プロンプトの引数として渡すことによって、子プロセスと接続データを通信します。 例:

    **WexLogger で認識されるコマンド プロンプトで名前付き引数として渡します。**  
    /wexlogger\_connectiondata = *\[接続データ\]*

    **注:** 場合、このオプションを使用し、手順 1、**子プロセス**以下のセクション**ない**必要です。

    **WexLogger を認識する名前付きの環境変数として渡します。**  
    \[YourAppName\_cmd\]=/wexlogger\_connectiondata = *\[接続データ\]*

    **注:** 場合、このオプションを使用し、手順 1、**子プロセス**以下のセクション**ない**必要です。

    **(いくつかその他のコマンドのパラメーター、環境変数など) は任意の形式でのプロセスに渡す**  
    **注:** 場合、このオプションを使用し、手順 1、**子プロセス**以下のセクション**は**必要です。

    **注:** 便宜上、値"/wexlogger\_connectiondata ="はネイティブおよびマネージの両方の RemoteLogControllers 内で定数として定義されます。

    -   **WEX::Logging::c\_szWexLoggerRemoteConnectionData**LogController.h で

    -   **RemoteLogController.WexLoggerRemoteConnectionData**Wex.Logger.Interop.dll で

3.  接続データを持つ子プロセスを起動します。
4.  呼び出す**RemoteLogController::InitalizeLogging ( *\[手順 1. で作成された接続データ\]* )** します。 タイムアウト値は、子が要求されていない場合があるため、子プロセスの起動後に、この呼び出しを行う必要があります**LogController::InitializeLogging()** 適切なタイミングでします。

    **注:** この呼び出しの戻り値を確認してください。

    ```cpp
    // ...launch child process with connection data...
    Throw::IfFailed(RemoteLogController::InitializeLogging(connectionData));
    ```

5.  子プロセスなどで待機します。

**子プロセス**

1.  接続データが場合は**いない**コマンド プロンプトで名前付き引数と子プロセスには、その WexLogger は (上記の手順 2 を参照してください) を理解、渡されたし、そのため、環境変数を設定する必要があります。

    \[YourAppName\_cmd\]=/wexlogger\_connectiondata = *\[接続データ\]*

    **例えば：**

    ```cpp
    // App name is mytestapp.exe
    ::SetEnvironmentVariable(L"mytestapp_cmd", String(c_szWexLoggerRemoteConnectionData).Append(connectionData));
    ```

2.  呼び出す**LogController::InitializeLogging()** このプロセスのログを初期化します。 内部的には、上記の手順 1 に設定する環境変数を利用してこれが (またはの手順 2 で、**親プロセス**セクション) 親プロセスにログ記録の接続を開始します。
3.  ログなどです。すべてのトレースは、親プロセスに送信されます。
4.  呼び出す**LogController::FinalizeLogging()** このプロセスのログ記録を完了します。

## <a name="determining-test-outcome"></a>テスト結果を決定します。


テスト_ケースの目的の結果を明示的に提供されるメソッドがありますが (**ログ:: Result()** ) がない**必要があります**ほとんどの場合、このメソッドを使用するテスト_ケースの。

テスト_ケースが明示的に呼び出していない場合など、**ログ:: Result()** 、および**しない**エラー ログに記録 (を使用して**ログ:: Error()** )、既定と見なされます成功テスト_ケース;その**は**エラー ログに記録、失敗したテストの場合は。

ただし場合、テスト ケース**は**を明示的に呼び出す**Log::Result(TestResults::TestPassed)** も**は**テスト ケース内でエラーのログ、テストもカウントされますとしてテスト内でエラーが発生したため失敗します。

TAEF フレームワーク内でタグ付けする別の既定のテスト結果と共に、テストでこの動作をオーバーライドできます。 これの詳細については、「TAEF テストの作成」のドキュメントで参照できます。

明示的に呼び出すことでこの動作を上書きすることができますも**ログ:: StartGroup()** 独自テスト グループ/テストの場合、既定値のテスト、任意の結果。

## <a name="generating-wtt-logs"></a>WTT ログを生成します。


WTT を使用してログを生成する 3 つのメソッドの存在、 **WexLogger**します。 それらのすべてを必要とする**WttLog.dll**実行のディレクトリまたはパスに存在します。

-   Wtt クライアントをインストールするには、ラボでは、実行している場合が wtt ログが自動的に生成されます。 これは、ラボ環境でしか存在しない 2 つの環境変数の存在を探し、WexLogger という事実が原因です。'WttTaskGuid' と 'WTTRunWorkingDir'。 これらの両方が存在しない場合は、wtt ログ自動的に有効にします。
-   ラボ環境の外部 TAEF 内で実行中の場合、/enablewttlogging をコマンド プロンプトで、テスト_ケースに渡します。 以下に例を示します。

    ``` syntax
    te my.test.dll /enablewttlogging
    ```

-   設定する必要があります、TAEF framework の外部 WexLogger を消費しているラボ環境で実行していない場合は、  **&lt;、\_プロセス\_名前&gt;\_CMD**環境変数を呼び出す前に、このオプションを含める**LogController::InitializeLogging()** します。 以下に例を示します。
    ```cpp
    Environment.SetEnvironmentVariable("<YOUR_PROCESS_NAME>_CMD", "/enablewttlogging");
    LogController.InitializeLogging();
    ```

    ```cpp
    Environment.SetEnvironmentVariable("consoleapplication4_cmd", "/enablewttlogging");
    LogController.InitializeLogging();
    ```

-   上書きするのではなく、既存の wtt ログ ファイルに追加する場合は、また/enablewttlogging に加えて/appendwttlogging オプションを指定します。

    ``` syntax
    te my.test.dll /enablewttlogging /appendwttlogging
    ```

    ```cpp
    Environment.SetEnvironmentVariable("<YOUR_PROCESS_NAME>_CMD", "/enablewttlogging /appendwttlogging");
    LogController.InitializeLogging();
    ```

    ```cpp
    Environment.SetEnvironmentVariable("consoleapplication4_cmd", "/enablewttlogging /appendwttlogging");
    LogController.InitializeLogging();
    ```

完全に上書きまたは次のコマンド オプションのいずれかを指定することによって WttLogger デバイスの既定の文字列に追加することです。

/WttDeviceString:&lt;新しいデバイスの文字列&gt;   
WexLogger WttLogger を初期化するときに使用する WttDeviceString を完全に上書きします。

/WttDeviceStringSuffix:&lt;デバイスの文字列に追加する値&gt;   
既定 WttDeviceString WexLogger WttLogger を初期化するときに使用するには、指定した値を追加します。 場合は無視されます '/WttDeviceString' も指定します。

次の表では、WexLogger TestResults が WttLogger 結果にどのようにマップする方法を示します。

| WexLogger | WttLogger                      |
|-----------|--------------------------------|
| 渡されました。    | WTT\_TESTCASE\_結果\_を渡す    |
| NotRun    | WTT\_TESTCASE\_結果\_ブロック |
| スキップされました   | WTT\_TESTCASE\_結果\_スキップ |
| ブロック   | WTT\_TESTCASE\_結果\_ブロック |
| Failed    | WTT\_TESTCASE\_結果\_失敗    |



## <a name="logger-dependencies"></a>ロガーの依存関係


ネイティブの C++ ロガー (**Wex.Logger.dll**) が依存**Wex.Common.dll**と**Wex.Communication.dll**します。

管理対象のロガー (**Wex.Logger.Interop.dll**) が依存**Wex.Logger.dll**、 **Wex.Common.dll**と**Wex.Communication.dll**.

さらに、 **WttLog.dll** Wtt によってログ記録が有効になっている場合に必要です。

## <a name="additional-error-data"></a>追加のエラー データ


エラーがログに記録するエラー自体だけでなく、次のものの 1 つ以上を含める WexLogger が有効にできます。

-   ミニダンプ
-   スクリーン キャプチャ
-   スタック トレース

``` syntax
te my.test.dll /minidumponerror
```

``` syntax
te my.test.dll /screencaptureonerror /stacktraceonerror
```

1 つまたは複数のこれらのオプションを有効になっているが表示されます余分なログ:: Error() が呼び出されるたびを出力します。

注:設定する必要があります、TAEF framework の外部 WexLogger を利用する場合、  **&lt;、\_プロセス\_名前&gt;\_CMD**これらのオプションを格納する環境変数呼び出しの前に**LogController::InitializeLogging()** します。 以下に例を示します。

```cpp
Environment.SetEnvironmentVariable("<YOUR_PROCESS_NAME>_CMD", "/screencaptureonerror /minidumponerror /stacktraceonerror");
LogController.InitializeLogging();
```

```cpp
Environment.SetEnvironmentVariable("consoleapplication4_cmd", "/screencaptureonerror /minidumponerror /stacktraceonerror");
LogController.InitializeLogging();
```

## <a name="c-error-handling"></a>C++ のエラー処理


各ログ API 呼び出しの戻り値をチェックする負担からテスト_ケースの作成者を保護するために、WexLogger は、省略可能なコールバック機構を使用して、予期しないエラー状態を報告します。**WexLoggerErrorCallback**関数。 Initializaiton 時に、 **WexLogger** (を使用して**LogController::InitializeLogging()** )、クライアントを指定することもできます、 **WexLoggerErrorCallback**に呼び出す関数内で予期しないエラー状態が発生する、 **WexLogger**します。 **WexLoggerErrorCallback**関数は、次のシグネチャを使用する必要があります。

```cpp
void __stdcall MyLoggerErrorCallback(const unsigned short* pszMessage, HRESULT hr);
```

WexLoggerErrorCallback 関数の一般的な用途は、(テスト ハーネスがコンソール アプリケーションの場合)、コンソールにエラー メッセージを記述することです。 TAEF フレームワークのクライアントは、たとえば、 **WexLogger**、実装して、 **WexLoggerErrorCallback** WexLogger エラーが発生したときに、コンソールに赤いテキストを書き込みますが。

## <a name="net-40-compatibility"></a>.NET 4.0 の互換性


読み込むことができます NetFx 3.5 2/3/と NetFx 4 の両方を処理できるように、Wex.Logger.Interop として NetFx 2/3/3.5、バイナリにコンパイルされます。 これにより、TAEF NetFx 2 上のすべてのマネージ アセンブリを実行できます。 Wex.Logger TAEF、以外を使用しているかどうかは、追加する必要がある、[構成ファイル](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/ms229689(v=vs.90))は exe に NetFx 3.5 2/3/バイナリを読み込む NetFx 4 ランタイムを構成するプロセスです。 構成ファイルには、次が含まれます。

```cpp
<configuration> 
    <startup useLegacyV2RuntimeActivationPolicy="true">
        <supportedRuntime version="v4.0"/>
    </startup>
</configuration>
```

## <a name="managed-code-error-and-exception-handling"></a>マネージ コードのエラーと例外処理


それぞれの戻り値をチェックする負担からテスト_ケースの作成者をシールドするには**ログ**の API 呼び出しを使用して、予期しないエラー状態を報告する、WexLogger の管理対象レイヤー、 **LoggerController.WexLoggerError**イベント。 独自の実装によって、いつでもこのイベントにサブスクライブすることがあります**WexLoggerErrorEventHandler**に対して次の使い慣れた構文を使用して、C#イベント サブスクリプション。

```cpp
LogController.WexLoggerError += new WexLoggerEventHandler(My_WexLoggerErrorHandler);
```

イベント ハンドラーの例を次に示します。

```cpp
static void LogController_WexLoggerError(object sender, WexLoggerErrorEventArgs e)
{
    ConsoleColor originalColor = Console.ForegroundColor;
    Console.ForegroundColor = ConsoleColor.Red;
    Console.WriteLine("LogController_WexLoggerError: " + e.Message);
    Console.ForegroundColor = originalColor;
}
```

さらに、 **LogController::InitializeLogging()** と**LogController::FinalizeLogging()** メソッド自体は、障害発生時 WexLoggerException をスローします。 これは、エラーの詳細な情報を提供し、テストの実行を開始する前に中止することもできます。 テスト_ケースの作成者がこれらの例外をキャッチについて心配する必要はありません - 必要がある想定処理 WexLogger initializaiton/終了時のみです。









