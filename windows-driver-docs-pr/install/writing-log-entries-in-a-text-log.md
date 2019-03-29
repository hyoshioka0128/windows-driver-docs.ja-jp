---
title: テキスト ログへのログ エントリの書き込み
description: テキスト ログへのログ エントリの書き込み
ms.assetid: e969f8dd-ad19-42d5-8218-3df0633cc304
keywords:
- テキスト ログのエントリの書き込みの WDK SetupAPI
- セクションでは WDK SetupAPI ログ記録
- テキスト ログの WDK SetupAPI、セクション
- テキスト ログのエントリを書き込む
- SetupAPI WDK Windows Vista では、ログのセクションではテキストをログ記録
- SetupAPI WDK Windows Vista をログ記録、テキスト ログのエントリを書き込む
- SetupWriteTextLog
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: faef4ed68c07f2bbf09f3564bc551cd868378764
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580972"
---
# <a name="writing-log-entries-in-a-text-log"></a>テキスト ログへのログ エントリの書き込み


アプリケーションの実行でログ エントリを書き込むには、次のいずれかを[SetupAPI テキスト ログ](setupapi-text-logs.md):

-   [呼び出す SetupWriteTextLog](calling-setupwritetextlog.md)インストール イベントに関する情報を含む 1 つのテキストのログ エントリの書き込みにします。

-   [呼び出す SetupWriteTextLogError](calling-setupwritetextlogerror.md) SetupAPI 固有のエラーまたは Win32 エラーに関する情報をテキスト ログに書き込めません。 **SetupWriteTextLogError**テキスト ログに 2 つの連続するエントリが書き込まれます最初のエントリが書き込まれたのと同じ形式で同じ情報が含まれています**SetupWriteTextLog** 、対応する 2 番目のエントリがログ記録。エラー コードとエラーのわかりやすい説明。

-   [呼び出す SetupWriteTextLogInfLine](calling-setupwritetextloginfline.md) INF ファイルの指定した行のテキストを含む 1 つのテキストのログ エントリの書き込みにします。

」の説明に従って[ログ セクションのテキスト本文の形式](format-of-a-text-log-section-body.md)、次の形式で関数書き込みエントリのログ記録 SetupAPI:

```cpp
entry_prefix time_stamp event_category indentation formatted_message
```

テキスト ログへの書き込みをさまざまな SetupAPI ログ関数で、エントリの主な違いは、特定の情報コンテンツとの形式、*書式設定されたメッセージ*フィールド。

設定する方法については、*インデント*インデントを設定するフィールド、*書式設定されたメッセージ*フィールドを参照してください[インデントのログ エントリの書き込み](writing-indented-log-entries.md)します。

 

 





