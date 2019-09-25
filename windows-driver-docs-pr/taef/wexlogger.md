---
title: WexLogger
description: WexLogger
ms.assetid: D9F4AD08-19EA-4a6c-AD25-886FBEA334B8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cfdf1d667701305d323c401cbb6c900e36b2f6c2
ms.sourcegitcommit: 96592088b276de87fc88dea3bb037654c9b31b11
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2019
ms.locfileid: "71248411"
---
# <a name="wexlogger"></a>WexLogger


WexLogger は、ネイティブコード、マネージコード、およびスクリプトにまたがるログ記録用の一貫した API を提供します。 また、コマンドプロンプトで実行されている単体テストを、長時間のストレステストまで拡大することもできます。

## <a name="logging-through-the-verify-framework"></a>検証フレームワークを使用したログ記録


テストケース内のほとんどのログ記録は、検証フレームワークを使用し[て](verify.md)実行する必要があります。 これにより、テストがより明確でわかりやすい方法で作成されます。 ただし、場合によっては、テストの作成者がログに書き込まれる内容をより細かく制御する必要があることが検出されることがあります。したがって、WexLogger API が必要になります。

## <a name="logging-within-taef"></a>TAEF でのログ記録


TAEF 内で実行されているテストケースの場合、テストの作成者はロガーの初期化を必要としません。 テストを作成している言語に公開されている Log API の使用をすぐに開始できます。

ネイティブC++コードでは、次のようになります。

```cpp
using namespace WEX::Logging;
using namespace WEX::Common;
Log::Comment(L"Rendering to the BufferView");
Log::Comment(L"Render succeeded");

Log::Comment(String().Format(L"Look, a number! %d", aNumber));

#define LOG_OUTPUT(fmt, ...) Log::Comment(String().Format(fmt, __VA_ARGS__))
LOG_OUTPUT(L"Look, a number! %d", aNumber);
```

マネージコードでは、次のようになります。

```cpp
Log.Comment("Rendering to the BufferView");
Log.Comment("Render succeeded");
```

JScript では、次のようになります。

```cpp
var log = new ActiveXObject("WEX.Logger.Log");
log.Comment("Rendering to the BufferView");
log.Comment("Render succeeded");
```

## <a name="logging-outside-taef"></a>TAEF 以外のログ記録


ほとんどの場合、ログの初期化と完了は TAEF によって実行されるため、前述のように、WexLogger はテストケースの継続時間に使用できるようになり、正常に終了します。 ただし、クライアントが TAEF 以外で WexLogger を使用する場合は、 **Logcontroller:: InitializeLogging ()** および**Logcontroller:: finalizelogging ()** を手動で呼び出す必要があります。 この要件は、ネイティブコードとマネージコードのみに存在します。スクリプトには、この追加の要件はありません。 LogController API の詳細については、次の「静的 LogController メソッド」の表を参照してください。

TAEF の外部で WTT ログを生成する方法については、「 [WTT ログの生成](#generating-wtt-logs)」セクションを参照してください。

## <a name="wexlogger-api"></a>WexLogger API


**使用可能なネイティブC++ログメソッドの一覧を次に示します。**

マネージコードとスクリプトには、同等のバージョンが用意されています。

| ネイティブC++ログのメソッド                                                                                                              | 機能                                                                                                                                                                                |
|-------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Assert (const wchar\_t\* pszassert)                                                                                                  | テストアサートをログに記録します。                                                                                                                                                                           |
| Assert (const wchar\_t\* pszassert、const wchar\_t\* pszassert)                                                                     | コンテキストを使用してテストアサートをログに記録します。                                                                                                                                                             |
| Assert (const wchar\_t\* pszassert、const wchar\_t\* pszassert、const wchar\_t\* pszassert、int line)                                | ファイル、関数、および行の情報を使用して、テストアサートをログに記録します。                                                                                                                                  |
| Assert (const wchar\_t\* pszassert、const wchar\_t\* pszassert、const wchar\_\* t pszassert、const wchar\_t\* pszassert、int line)   | コンテキストを使用してテストアサートをログに記録し、ファイル、関数、および行の情報も記録します。                                                                                                               |
| バグ (const wchar\_t\* pszbug database、int のバグ id)                                                                                     | 既知のバグ番号をログに記録します。                                                                                                                                                                      |
| バグ (const wchar\_t\* pszbug database、int のバグ id、const\_wchar\* t pszcontext)                                                        | コンテキストを使用して既知のバグ番号をログに記録します。                                                                                                                                                        |
| Comment (const wchar\_t\* pszcomment)                                                                                                | テストコメントをログに記録します。                                                                                                                                                                          |
| Comment (const wchar\_t\* pszcomment、const wchar\_t\* pszcomment)                                                                   | コンテキストを使用してテストコメントを記録する                                                                                                                                                             |
| Endgroup (const wchar\_t\* pszgroupname)                                                                                             | テストのグループまたは特定のテストのグループの終了をログに記録します。                                                                                                                                      |
| Endgroup (const wchar\_t\* pszgroupname、const wchar\_t\* pszgroupname)                                                                | コンテキストを使用して、テストのグループまたは特定のテストのグループの終了をログに記録します。                                                                                                                        |
| エラー (const wchar\_t\* pszerror)                                                                                                    | テストエラーをログに記録します。                                                                                                                                                                            |
| エラー (const wchar\_t\* pszerror、const wchar\_t\* pszerror)                                                                       | コンテキストを使用してテストエラーをログに記録します。                                                                                                                                                              |
| エラー (const wchar\_t\* pszerror、const wchar\_t\* pszerror、const wchar\_t\* pszerror、int line)                                  | ファイル、関数、および行の情報を含むテストエラーをログに記録します。                                                                                                                                   |
| エラー (const wchar\_t\* pszerror、const wchar\_t\* pszerror、const wchar\_t\* pszerror、const wchar\_t\* pszerror、int line)     | コンテキストを使用してテストエラーをログに記録し、ファイル、関数、および行の情報も記録します。                                                                                                                |
| File (const wchar\_t\* pszfilename)                                                                                                  | 保存するテストファイルをログに記録します。 ファイルは&lt;、WTTRunWorkingDir&gt; &lt;&gt;wexlogfileoutput (WTTRunWorkingDir が設定されている場合) または\\currentdirectory wexlogfileoutput のいずれかに保存されます。\\               |
| File (const wchar\_t\* pszfilename、const wchar\_t\* pszfilename)                                                                     | コンテキストを使用して、保存するテストファイルをログに記録します。 ファイルは&lt;、WTTRunWorkingDir&gt; &lt;&gt;wexlogfileoutput (WTTRunWorkingDir が設定されている場合) または\\currentdirectory wexlogfileoutput のいずれかに保存されます。\\ |
| Property (const wchar\_t\* pszname、const wchar\_t\* pszname)                                                                       | 名前/値プロパティのペアをログに記録します。 値は xml 形式で指定できます。                                                                                                                              |
| Property (const wchar\_t\* pszname、const wchar\_t\* pszname、const wchar\_t\* pszname)                                          | コンテキストを使用して、名前と値のプロパティのペアをログに記録します。 値は xml 形式で指定できます。                                                                                                                |
| Result (TestResults:: Result testResult)                                                                                              | テスト結果をログに記録します。                                                                                                                                                                           |
| Result (TestResults:: Result testresult、const wchar\_t\* pszcomment)                                                                 | 関連するコメントを使用してテスト結果をログに記録します。                                                                                                                                                |
| Result (TestResults:: Result testresult、const wchar\_t\* pszcomment、const wchar\_t\* pszcomment)                                    | コンテキストで、関連付けられているコメントを使用してテスト結果をログに記録します。                                                                                                                                  |
| Startgroup (const wchar\_t\* pszgroupname)                                                                                           | テストのグループまたは特定のテストのグループの開始をログに記録します。                                                                                                                                    |
| Startgroup (const wchar\_t\* pszgroupname, TestResults:: Result defaulttestresult)                                                    | テストのグループまたは特定のテストのグループの開始をログに記録します。既定のテスト結果も設定します。                                                                                                 |
| Startgroup (const wchar\_t\* pszgroupname, const wchar\_t\* pszgroupname)                                                              | コンテキストを使用して、テストのグループまたは特定のテストのグループの開始をログに記録します。                                                                                                                      |
| Startgroup (const wchar\_t\* pszgroupname、const wchar\_t\* pszgroupname、TestResults:: result defaulttestresult)                       | テストのグループまたは特定のテストのグループの開始をログに記録します。既定のテスト結果も設定します。                                                                                                 |
| 警告 (const wchar\_t\* pszwarning)                                                                                                | テスト警告をログに記録します。                                                                                                                                                                          |
| 警告 (const wchar\_t\* pszwarning、const wchar\_t\* pszwarning)                                                                   | コンテキストを使用してテスト警告をログに記録します。                                                                                                                                                            |
| 警告 (const wchar\_t\* pszwarning、const wchar\_t\* pszwarning、const wchar\_t\* pszwarning、int line)                              | ファイル、関数、および行の情報を含むテスト警告をログに記録します。                                                                                                                                 |
| 警告 (const wchar\_t\* pszwarning、const wchar\_t\* pszwarning、const wchar\_\* t pszwarning、const wchar\_t\* pszwarning、int line) | コンテキストを使用してテスト警告をログに記録し、ファイル、関数、および行の情報も記録します。                                                                                                              |
| Xml (const wchar\_t\* pszxml)                                                                                                        | Xml データをログに記録します。 適切な形式であるかどうかの確認は行われません。                                                                                                                             |
| Xml (const wchar\_t\* pszxml、const wchar\_t\* pszxml)                                                                           | コンテキストを使用して xml データをログに記録します。 適切な形式であるかどうかの確認は行われません。                                                                                                               |
| ミニダンプ ()                                                                                                                          | 現在のプロセスミニダンプをログに記録します。                                                                                                                                                           |



**注:** "Context" は余分な文字列であり、必要に応じて、より多くのコンテキストや詳細を提供するために**Wexlogger** API 呼び出しを指定できます。 たとえば、ImageComparator クラスのメソッドから**Wexlogger** API 呼び出しを行う場合、コンテキストとして常に "ImageComparator" を渡すことを選択できます。

Native C++ **TestResults:: Result**列挙型に使用できる有効な値を次に示します。 マネージコードとスクリプトには、同等のバージョンが用意されています。

| Native C++ TestResults:: Result 列挙型 | 機能        |
|--------------------------------------------|----------------------|
| 渡し                                     | テストが成功しました      |
| NotRun                                     | テストは実行されませんでした |
| 読み                                    | テストがスキップされました |
| ブロック                                    | テストはブロックされました |
| Failed                                     | テストに失敗しました      |



**使用可能なネイティブC++ logcontroller メソッドの一覧を次に示します。**

| ネイティブC++ Logcontroller メソッド                                                                       | 機能                                                                                                                                                                                                                                                                                                   |
|--------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| static HRESULT InitializeLogging ()                                                                     | ログ記録機能を初期化します。                                                                                                                                                                                                                                                                               |
| static HRESULT InitializeLogging (WexLoggerErrorCallback pfnErrorCallback)                              | ログ記録機能を初期化し、内部ロガーエラーを通知するために使用する WexLoggerErrorCallback 関数を指定します。                                                                                                                                                               |
| static HRESULT initializelogging (const wchar\_t\* pszlogname)                                          | ログ記録機能を初期化し、使用するログファイルの名前を指定します。 **注:** ログ名は、 [WttLogging が有効になって](#generating-wtt-logs)いる場合にのみ考慮されます。                                                                                                             |
| static HRESULT initializelogging (const wchar\_t\* pszlogname, WexLoggerErrorCallback pfnerrorcallback) | ログ記録機能を初期化し、使用するログファイルの名前を指定します。また、内部ロガーエラーを通知するために使用する WexLoggerErrorCallback 関数を指定します。 **注:** ログ名は、 [WttLogging が有効になって](#generating-wtt-logs)いる場合にのみ考慮されます。 |
| static bool IsInitialized ()                                                                            | このプロセスに対して LogController が初期化されているかどうかを返します。                                                                                                                                                                                                                                 |
| static const unsigned short\* getlogname ()                                                             | InitializeLogging 呼び出しでログに指定された名前を返します (存在する場合)。                                                                                                                                                                                                                         |
| static HRESULT FinalizeLogging ()                                                                       | ログ記録機能を終了します。                                                                                                                                                                                                                                                                                   |



**注:** WexLoggerErrorCallback メカニズムC++の詳細および taef フレームワーク外での使用方法については、以下の「エラー処理」セクションを参照してください。

**注:** TAEF フレームワークの外部で**Wexlogger**を使用する場合は、既にログの初期化/完了を処理するので、Initializelogging/finalizelogging を呼び出す必要があるだけです。

**注:** スクリプトから**Wexlogger**を使用する場合は、ログ機能を初期化/完了する必要はありません。

**使用可能なネイティブC++ remotelogcontrol メソッドの一覧を次に示します。**

| ネイティブC++ remotelogcontroller メソッド                                                                             | 機能                                                                                                                                                                                                |
|--------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| static HRESULT GenerateConnectionData (WEX:: Common:: NoThrowString & connectionData)                                  | 子プロセスが親プロセスに再びログインできるようにするために、親プロセスと子プロセス内で使用する必要がある接続データを生成します。                                                          |
| static HRESULT GenerateConnectionData (const wchar\_t\* pszmachinename, wex:: Common:: NoThrowString & connectiondata) | リモートコンピューターで子プロセスを起動するときに使用されます。 子プロセスが親プロセスに再びログインできるようにするために、親プロセスと子プロセス内で使用する必要がある接続データを生成します。 |
| static HRESULT InitializeLogging (WEX:: Common:: NoThrowString connectionData)                                        | 親プロセス内のログ記録機能を初期化して、子プロセスがそれに再びログインできるようにします。                                                                                                         |



**注:** リモートログの詳細については、以下の「[子プロセスからのリモートログ](#remote-logging-from-child-processes)」セクションを参照してください。

使用可能なマネージログのメソッドの一覧を次に示します。

| マネージログのメソッド                                                             | 機能                                                                                                                                                                |
|---------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Assert (IFormatProvider provider、string format、params オブジェクト\[ \]引数)         | カルチャ固有の書式情報プロバイダー、書式指定文字列、および0個以上の書式設定対象オブジェクトを含むオブジェクト配列を使用して、テストアサートをログに記録します。               |
| Assert (IFormatProvider provider、string format、params オブジェクト\[ \]引数)         | カルチャ固有の書式情報プロバイダー、書式指定文字列、および0個以上の書式設定対象オブジェクトを含むオブジェクト配列を使用して、テストアサートをログに記録します。               |
| Assert (文字列メッセージ)                                                          | テストアサートをログに記録します。                                                                                                                                                           |
| Assert (文字列形式、オブジェクト arg0)                                              | 書式指定文字列と書式設定するオブジェクトを使用して、テストアサートをログに記録します。                                                                                                             |
| Assert (文字列形式、params オブジェクト\[ \]引数)                                   | 書式指定文字列と、0個以上の書式設定対象オブジェクトを含むオブジェクト配列を使用して、テストアサートをログに記録します。                                                                   |
| Assert (文字列メッセージ、文字列コンテキスト)                                          | コンテキストを使用してテストアサートをログに記録します。                                                                                                                                             |
| Assert (文字列メッセージ、文字列ファイル、文字列関数、int 行)                  | テストアサートをログに記録し、ファイル、関数、行の情報も記録します。                                                                                                             |
| Assert (文字列メッセージ、文字列コンテキスト、文字列ファイル、文字列関数、int 行)  | コンテキストを使用してテストアサートをログに記録し、ファイル、関数、および行の情報も記録します。                                                                                               |
| バグ (文字列バグデータベース、int バグ Id)                                              | 既知のバグ番号をログに記録します。                                                                                                                                                      |
| バグ (文字列バグデータベース、int バグ Id、文字列コンテキスト)                              | コンテキストを使用して既知のバグ番号をログに記録します。                                                                                                                                        |
| Comment (IFormatProvider provider, string format, params object\[ \] args)        | カルチャ固有の書式情報プロバイダー、書式指定文字列、および0個以上の書式設定対象オブジェクトを含むオブジェクト配列を使用して、テストコメントを記録します。              |
| Comment (文字列メッセージ)                                                         | テストコメントをログに記録する                                                                                                                                                           |
| Comment (文字列形式、オブジェクト arg0)                                             | 書式指定文字列と書式設定するオブジェクトを使用して、テストコメントをログに記録します。                                                                                                            |
| Comment (文字列形式、params オブジェクト\[ \]引数)                                  | 書式指定文字列と、0個以上の書式設定対象オブジェクトを含むオブジェクト配列を使用して、テストコメントを記録します。                                                                   |
| Comment (文字列メッセージ、文字列コンテキスト)                                         | コンテキストを使用してテストコメントを記録する                                                                                                                                             |
| EndGroup (文字列 groupName)                                                      | テストのグループまたは特定のテストのグループの終了をログに記録します。                                                                                                                      |
| EndGroup (文字列 groupName、文字列コンテキスト)                                      | コンテキストを使用して、テストのグループまたは特定のテストのグループの終了をログに記録します。                                                                                                        |
| エラー (IFormatProvider provider、string format、params オブジェクト\[ \]引数)          | カルチャ固有の書式情報プロバイダー、書式指定文字列、および0個以上の書式設定対象オブジェクトを含むオブジェクト配列を使用して、テストエラーをログに記録します。                |
| エラー (文字列メッセージ)                                                           | テストエラーをログに記録します。                                                                                                                                                            |
| エラー (文字列形式、オブジェクト arg0)                                               | 書式指定文字列と書式設定するオブジェクトを使用して、テストエラーをログに記録します。                                                                                                              |
| エラー (文字列メッセージ、文字列コンテキスト)                                           | コンテキストを使用してテストエラーをログに記録します。                                                                                                                                              |
| エラー (IFormatProvider provider、string format、params オブジェクト\[ \]引数)          | 書式指定文字列と、0個以上の書式設定対象オブジェクトを含むオブジェクト配列を使用して、テストエラーをログに記録します。                                                                     |
| エラー (文字列メッセージ、文字列ファイル、文字列関数、int 行)                   | ファイル、関数、および行の情報を含むテストエラーをログに記録します。                                                                                                                   |
| エラー (文字列メッセージ、文字列コンテキスト、文字列ファイル、文字列関数、int 行)   | コンテキストを使用してテストエラーをログに記録し、ファイル、関数、および行の情報も記録します。                                                                                                |
| ファイル (文字列ファイル名)                                                           | 保存するテストファイルをログに記録します。 ファイルは、WTTRunWorkingDir\\wexlogfileoutput (WTTRunWorkingDir が設定されている場合) または currentdirectory\\wexlogfileoutput のいずれかに保存されます。               |
| File (文字列ファイル名、文字列コンテキスト)                                           | コンテキストを使用して、保存するテストファイルをログに記録します。 ファイルは、WTTRunWorkingDir\\wexlogfileoutput (WTTRunWorkingDir が設定されている場合) または currentdirectory\\wexlogfileoutput のいずれかに保存されます。 |
| ミニダンプ ()                                                                      | 現在のプロセスミニダンプをログに記録します。                                                                                                                                           |
| Property (文字列名、文字列値)                                             | 名前/値プロパティのペアをログに記録します。 値は xml 形式で指定できます。                                                                                                              |
| Property (文字列名、文字列値、文字列コンテキスト)                             | コンテキストを使用して、名前と値のプロパティのペアをログに記録します。 値は xml 形式で指定できます。                                                                                                |
| Result (TestResult testResult)                                                   | テスト結果をログに記録します。                                                                                                                                                           |
| Result (TestResult testResult、文字列コメント)                                   | 関連するコメントを使用してテスト結果をログに記録します。                                                                                                                                |
| Result (TestResult testResult、string comment、string context)                   | コンテキストで、関連付けられているコメントを使用してテスト結果をログに記録します。                                                                                                                  |
| StartGroup (文字列 groupName)                                                    | テストのグループまたは特定のテストのグループの開始をログに記録します。                                                                                                                    |
| StartGroup (文字列 groupName、文字列コンテキスト)                                    | コンテキストを使用して、テストのグループまたは特定のテストのグループの開始をログに記録します。                                                                                                      |
| Warning (IFormatProvider provider、string format、params object\[ \] args)        | カルチャ固有の書式情報プロバイダー、書式指定文字列、および0個以上の書式設定対象オブジェクトを含むオブジェクト配列を使用して、テスト警告をログに記録します。              |
| 警告 (文字列メッセージ)                                                         | テスト警告をログに記録します。                                                                                                                                                          |
| 警告 (文字列形式、オブジェクト arg0)                                             | 書式指定文字列と書式設定するオブジェクトを使用して、テスト警告をログに記録します。                                                                                                            |
| Warning (文字列形式、params オブジェクト\[ \]引数)                                  | 書式指定文字列と、0個以上の書式設定対象オブジェクトを含むオブジェクト配列を使用して、テスト警告をログに記録します。                                                                   |
| 警告 (文字列メッセージ、文字列コンテキスト)                                         | コンテキストを使用してテスト警告をログに記録します。                                                                                                                                            |
| 警告 (文字列メッセージ、文字列ファイル、文字列関数、int 行)                 | ファイル、関数、および行の情報を含むテスト警告をログに記録します。                                                                                                                 |
| 警告 (文字列メッセージ、文字列コンテキスト、文字列ファイル、文字列関数、int 行) | コンテキストを使用してテスト警告をログに記録し、ファイル、関数、および行の情報も記録します。                                                                                              |
| Xml (文字列 xmlData)                                                             | Xml データをログに記録します。 適切な形式であるかどうかの確認は行われません。                                                                                                             |
| Xml (文字列 xmlData、文字列コンテキスト)                                             | コンテキストを使用して xml データをログに記録します。 適切な形式であるかどうかの確認は行われません。                                                                                               |



**使用できる管理された Logcontrol メソッドの一覧を次に示します。**

| 管理された LogController メソッド                 | 機能                                                                                                                                                                                       |
|-----------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| static void InitializeLogging ()               | ログ記録機能を初期化します。                                                                                                                                                                   |
| static void InitializeLogging (文字列 logName) | ログ記録機能を初期化し、使用するログファイルの名前を指定します。 **注:** ログ名は、 [WttLogging が有効になって](#generating-wtt-logs)いる場合にのみ考慮されます。 |
| static bool IsInitialized ()                   | このプロセスに対して LogController が初期化されているかどうかを返します。                                                                                                                     |
| 静的文字列 GetLogName ()                    | InitializeLogging 呼び出しでログに指定された名前を返します (存在する場合)。                                                                                                             |
| 静的 void FinalizeLogging ()                 | ログ記録機能を終了します。                                                                                                                                                                       |



**注:** TAEF フレームワーク外で**Wexlogger**のマネージレイヤーを使用する場合のエラーと例外の処理方法の詳細については、後述の「マネージコードエラーと例外」セクションを参照してください。

**注:** TAEF フレームワークの外部で**Wexlogger**を使用する場合は、既にログの初期化/完了を処理するので、Initializelogging/finalizelogging を呼び出す必要があるだけです。

**注:** スクリプトから**Wexlogger**を使用する場合は、ログ機能を初期化/完了する必要はありません。

**使用可能なマネージ Remotelogcontrol メソッドの一覧を次に示します。**

| マネージ RemoteLogController メソッド                      | 機能                                                                                                                                                                                                |
|----------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| static String GenerateConnectionData ()                   | 子プロセスが親プロセスに再びログインできるようにするために、親プロセスと子プロセス内で使用する必要がある接続データを生成します。                                                          |
| static String GenerateConnectionData (文字列 machineName) | リモートコンピューターで子プロセスを起動するときに使用されます。 子プロセスが親プロセスに再びログインできるようにするために、親プロセスと子プロセス内で使用する必要がある接続データを生成します。 |
| static void InitializeLogging (文字列 connectionData)     | 親プロセス内のログ記録機能を初期化して、子プロセスがそれに再びログインできるようにします。                                                                                                         |



**注:** リモートログの詳細については、以下の「[子プロセスからのリモートログ](#remote-logging-from-child-processes)」セクションを参照してください。

## <a name="remote-logging-from-child-processes"></a>子プロセスからのリモートログ


WexLogger を使用すると、1つ以上の子プロセスが1つの親プロセスに再度ログインできるようになり、結果として1つのログファイル内に統合されたテスト結果が生成されます。

子プロセスは、親プロセスと同じコンピューター上で実行するか、別のコンピューターでリモートで実行できます。 リモートコンピューターのログ記録を機能させるには、WexLogger クライアントを使用して、リモートコンピューター上のすべての子プロセスに対して TCP ファイアウォールの除外を追加します。 ただし、子プロセスが親と同じコンピューター上で実行されている場合は、ファイアウォールの変更は必要ありません。

各リモートログ接続を設定するには、次の手順を実行する必要があります。

**親プロセス**

1.  両方のプロセスでログ接続を開始するために使用する必要がある接続データを生成するには、 **Remotelogcontroller:: GenerateConnectionData ()** を呼び出します。

    **注:** この呼び出しの戻り値を必ず確認してください。

    ```cpp
        NoThrowString connectionData;
        Throw::IfFailed(RemoteLogController::GenerateConnectionData(connectionData));

    ```

2.  接続データを環境ブロックで設定するか、コマンドプロンプトで引数として渡すことによって、接続データを子プロセスと通信します。 以下に例を示します。

    **WexLogger が理解するコマンドプロンプトで、名前付き引数としてを渡します。**  
    /wexlogger\_connectiondata = *\[接続データ\]*

    **注:** このオプションを使用する場合は、下の「**子プロセス**」セクションの手順1を実行する必要**はありません**。

    **WexLogger によって認識される名前付き環境変数としてを渡します。**  
    \[自分の\_appname\]cmd =\_/wexlogger connectiondata = *\[接続\]データ*

    **注:** このオプションを使用する場合は、下の「**子プロセス**」セクションの手順1を実行する必要**はありません**。

    **任意の形式 (他のコマンドパラメーター、環境変数など) でプロセスに渡す**  
    **注:** このオプションを使用する場合は、下の「**子プロセス**」セクションの手順 1. を実行する必要**が**あります。

    **注:** 便宜上、値 "/wexlogger\_connectiondata =" は、ネイティブとマネージ remotelogcontrollers の両方で定数として定義されています。

    -   Logcontroller. h の**wex:\_: Logging:: c szWexLoggerRemoteConnectionData**

    -   **WexLoggerRemoteConnectionData**の (Wex. Interop. .dll)

3.  接続データを使用して子プロセスを起動する
4.  **Remotelogcontroller:: InitalizeLogging ( *\[手順 1\]で作成した接続データ*)** を呼び出します。 子プロセスの起動後にこの呼び出しを行う必要があります。これは、子が**Logcontroller:: InitializeLogging ()** を適切なタイミングで呼び出さない場合にタイムアウトになるためです。

    **注:** この呼び出しの戻り値を必ず確認してください。

    ```cpp
    // ...launch child process with connection data...
    Throw::IfFailed(RemoteLogController::InitializeLogging(connectionData));
    ```

5.  子プロセスなどを待機します。

**子プロセス**

1.  接続データが、WexLogger で認識されるコマンドプロンプトで名前付き引数として子プロセス**に渡され**なかった場合 (上記の手順2を参照)、環境変数を次のように設定する必要があります。

    \[自分の\_appname\]cmd =\_/wexlogger connectiondata = *\[接続\]データ*

    **例えば：**

    ```cpp
    // App name is mytestapp.exe
    ::SetEnvironmentVariable(L"mytestapp_cmd", String(c_szWexLoggerRemoteConnectionData).Append(connectionData));
    ```

2.  **Logcontroller:: initializelogging ()** を呼び出して、このプロセスのログを初期化します。 内部的には、これにより、上記の手順 1 (または**親プロセス**セクションの手順 2) で設定された環境変数を利用し、親プロセスへのログ接続を開始します。
3.  ログなどすべてのトレースが親プロセスに送り返されます。
4.  **Logcontroller:: FinalizeLogging ()** を呼び出して、このプロセスのログ記録を終了します。

## <a name="determining-test-outcome"></a>テスト結果の特定


テストケースの意図した結果 (**Log:: Result ()** ) を明示的に指定するためのメソッドが用意されていますが、ほとんどの場合、このメソッドを使用するテストケースは**必要**ありません。

たとえば、テストケースで**log:: Result ()** が明示的に呼び出されず、エラー ( **Log:: error ()** によって) がログに記録**され**ない場合、既定では合格テストケースと見なされます。エラーが**ログに**記録される場合は、失敗しているテストケースです。

ただし、テストケース**が明示的**に**Log:: Result (TestResults:: testpassed)** を呼び出すが、テストケース内でエラーがログに記録される場合**でも、** テスト内でエラーが発生したため、テストはエラーとしてカウントされます。

TAEF フレームワーク内では、別の既定のテスト結果でテストにタグを付けて、この動作をオーバーライドできます。 詳細については、「TAEF テストの作成」ドキュメントを参照してください。

この動作は、独自のテストグループ/テストケースに対して**Log:: startgroup ()** を明示的に呼び出すことによってオーバーライドすることもできます。また、選択した既定のテスト結果を使用します。

## <a name="generating-wtt-logs"></a>WTT ログの生成


**Wexlogger**を使用して wtt ログを生成するには、次の3つの方法があります。 すべてのユーザーが、実行ディレクトリまたはパスに**WttLog**が存在している必要があります。

-   ラボでを実行していて、wtt クライアントがインストールされている場合は、wtt ログが自動的に生成されます。 これは、WexLogger がラボ環境に存在する必要がある2つの環境変数の存在を検索するためです。' WttTaskGuid ' と ' WTTRunWorkingDir '。 これらの両方が存在する場合は、wtt ログ記録が自動的に有効になります。
-   ラボ環境外で TAEF 内で実行されている場合は、コマンドプロンプトで/enablewttlogging をテストケースに渡します。 例:

    ``` syntax
    te my.test.dll /enablewttlogging
    ```

-   Taef フレームワーク以外で wexlogger を使用していて、ラボ環境で実行されていない場合は、  **&lt;\_\_プロセス名&gt;\_CMD**環境変数をに設定する必要があります。**Logcontroller:: InitializeLogging ()** を呼び出す前に、このオプションを含めます。 例:
    ```cpp
    Environment.SetEnvironmentVariable("<YOUR_PROCESS_NAME>_CMD", "/enablewttlogging");
    LogController.InitializeLogging();
    ```

    ```cpp
    Environment.SetEnvironmentVariable("consoleapplication4_cmd", "/enablewttlogging");
    LogController.InitializeLogging();
    ```

-   既存の wtt ログファイルを上書きせずに追加する場合は、/enablewttlogging. に加えて/appendwttlogging オプションも指定します。

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

また、次のいずれかのコマンドオプションを指定して、既定の WttLogger デバイス文字列を完全にオーバーライドしたり、追加したりすることもできます。

/WttDeviceString:&lt;新しいデバイス文字列&gt;   
WttLogger を初期化するときに、WexLogger によって使用される WttDeviceString を完全にオーバーライドします。

/WttDeviceStringSuffix:&lt;デバイス文字列に追加する値&gt;   
指定された値を、WexLogger が WttLogger を初期化するときに使用する既定の WttDeviceString に追加します。 '/WttDeviceString ' も指定されている場合は無視されます。

次の表は、WexLogger TestResults が WttLogger の結果にマップする方法を示しています。

| WexLogger | WttLogger                      |
|-----------|--------------------------------|
| 渡し    | WTT\_TESTCASE\_の\_結果パス    |
| NotRun    | WTT\_TESTCASE\_の\_結果がブロックされました |
| 読み   | WTT\_TESTCASE\_の\_結果がスキップされました |
| ブロック   | WTT\_TESTCASE\_の\_結果がブロックされました |
| Failed    | WTT\_TESTCASE\_の\_結果失敗    |



## <a name="logger-dependencies"></a>Logger の依存関係


ネイティブC++ Logger (**wex .dll**) は、 **Wex. .Dll**および**wex. com .dll**に依存しています。

マネージ logger (**wex**) は、 **wex (logger**)、Wex、および**wex**(.dll)**に依存**しています。また、

また、Wtt ログが有効になっている場合は、 **WttLog**が必要です。

## <a name="additional-error-data"></a>追加のエラーデータ


エラーがログに記録された場合は、エラー自体に加えて、WexLogger で次の項目を1つ以上含めることができます。

-   ミニダンプ
-   ScreenCapture
-   StackTrace

``` syntax
te my.test.dll /minidumponerror
```

``` syntax
te my.test.dll /screencaptureonerror /stacktraceonerror
```

これらのオプションのうち1つ以上を有効にすると、Log:: Error () が呼び出されるたびに、追加の出力が得られます。

メモ:Taef フレームワークの外部で wexlogger を使用し **&lt;て\_\_&gt;\_** いる場合は、を呼び出す**前に、プロセス名 CMD 環境変数にこれらのオプションが含まれるように設定する必要があります。LogController:: InitializeLogging ()** 。 例:

```cpp
Environment.SetEnvironmentVariable("<YOUR_PROCESS_NAME>_CMD", "/screencaptureonerror /minidumponerror /stacktraceonerror");
LogController.InitializeLogging();
```

```cpp
Environment.SetEnvironmentVariable("consoleapplication4_cmd", "/screencaptureonerror /minidumponerror /stacktraceonerror");
LogController.InitializeLogging();
```

## <a name="c-error-handling"></a>C++エラー処理


テストケースの作成者を、各 Log API 呼び出しの戻り値をチェックする負担からシールドするために、WexLogger は、オプションのコールバック機構を使用して予期しないエラー状態を報告します。**WexLoggerErrorCallback**関数。 **Wexlogger** ( **Logcontroller:: initializelogging ()** を介して) を初期化すると、クライアントは、 **wexlogger**内で予期しないエラー状態が発生した場合に呼び出す**WexLoggerErrorCallback**関数を指定することができます。 **WexLoggerErrorCallback**関数は、次のシグネチャを使用する必要があります。

```cpp
void __stdcall MyLoggerErrorCallback(const unsigned short* pszMessage, HRESULT hr);
```

WexLoggerErrorCallback 関数の一般的な使用方法は、エラーメッセージをコンソールに書き込むことです (テストハーネスがコンソールアプリケーションの場合)。 たとえば、TAEF フレームワークは**wexlogger**のクライアントであり、wexlogger エラーが発生したときに赤いテキストをコンソールに書き込む**WexLoggerErrorCallback**を実装します。

## <a name="net-40-compatibility"></a>.NET 4.0 の互換性


Wex. Logger は NetFx 2/3/3.5 バイナリとしてコンパイルされるため、NetFx 2/3/3.5 と NetFx 4 の両方のプロセスに読み込むことができます。 これにより、NetFx 2 の上にあるすべてのマネージアセンブリを TAEF で実行できるようになります。 TAEF の外部で Wex ロガーを使用している場合は、NetFx 4 ランタイムが NetFx 2/3/3.5 バイナリをプロセスに読み込むように構成するために、exe の[構成ファイル](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/ms229689(v=vs.90))を追加する必要があります。 構成ファイルには、次のものが含まれている必要があります。

```cpp
<configuration> 
    <startup useLegacyV2RuntimeActivationPolicy="true">
        <supportedRuntime version="v4.0"/>
    </startup>
</configuration>
```

## <a name="managed-code-error-and-exception-handling"></a>マネージコードエラーと例外処理


テストケースの作成者を、各**Log** API 呼び出しの戻り値をチェックする負担からシールドするために、WexLogger のマネージ層は、 **LoggerController. WexLoggerError**イベントを使用して予期しないエラー状態を報告します。 独自の**WexLoggerErrorEventHandler**を実装し、イベントサブスクリプションに対しC#て次の使い慣れた構文を使用することによって、いつでもこのイベントにサブスクライブできます。

```cpp
LogController.WexLoggerError += new WexLoggerEventHandler(My_WexLoggerErrorHandler);
```

イベントハンドラーの例を次に示します。

```cpp
static void LogController_WexLoggerError(object sender, WexLoggerErrorEventArgs e)
{
    ConsoleColor originalColor = Console.ForegroundColor;
    Console.ForegroundColor = ConsoleColor.Red;
    Console.WriteLine("LogController_WexLoggerError: " + e.Message);
    Console.ForegroundColor = originalColor;
}
```

さらに、 **Logcontroller:: InitializeLogging (** ) および**Logcontroller:: finalizelogging ()** メソッド自体は、障害が発生した場合に WexLoggerException をスローします。 これにより、エラーに関する詳細情報が提供されます。また、テストの実行を開始する前に中止することもできます。 テストケースの作成者は、これらの例外をキャッチすることを心配する必要はありません。 WexLogger の初期化時または完了時にのみ、予期または処理される必要があります。









