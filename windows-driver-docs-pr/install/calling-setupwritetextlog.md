---
title: SetupWriteTextLog を呼び出す
description: SetupWriteTextLog を呼び出す
ms.assetid: a07118ae-bef6-4d01-94d9-98587cbff863
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57a0c11671f5735c740c0dd08026b166277e01c0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536383"
---
# <a name="calling-setupwritetextlog"></a>SetupWriteTextLog を呼び出す


[**SetupWriteTextLog** ](https://msdn.microsoft.com/library/windows/hardware/ff552218)インストール イベントに関する情報を含む 1 つのエントリを追加、 [SetupAPI テキスト ログ](setupapi-text-logs.md)します。

」の説明に従って[ログ セクションのテキスト本文の形式](format-of-a-text-log-section-body.md)、ログ エントリの形式は次のフィールドで構成されます。

```cpp
entry_prefix time_stamp event_category indentation formatted_message
```

呼び出す**SetupWriteTextLog**、次の情報をアプリケーションに渡します。

-   ログのトークンを呼び出すことによって取得されたテキスト ログのセクション[ **SetupGetThreadLogToken**](https://msdn.microsoft.com/library/windows/hardware/ff552211)、またはシステム定義の 1 つ[トークンをログイン](log-tokens.md)します。 ログのトークンは、テキスト ログ セクションに関連付けられた場合**SetupWriteTextLog**そのセクションにログ エントリを書き込みます。 それ以外の場合、 **SetupWriteTextLog**テキスト ログ セクションに含まれていないログの一部にログ エントリを追加します。 さらに、かどうか**SetupWriteTextLog** 、ログ エントリを書き込みますとテキスト ログ**SetupWriteTextLog**エントリを書き込む、ログのシステム定義のトークン値に依存します。

    ログのトークンの詳細については、[設定とスレッドのログのトークン取得](setting-and-getting-a-log-token-for-a-thread.md)を参照してください。

-   記載されているイベントのカテゴリの 1 つ[テキスト ログのイベント カテゴリを有効にする](enabling-event-categories-for-a-text-log.md)します。 テキスト ログのエントリのイベント カテゴリが有効になっている場合[ **SetupWriteTextLog** ](https://msdn.microsoft.com/library/windows/hardware/ff552218)テキスト ログにエントリを追加しますそれ以外の場合、 **SetupWriteTextLog**書き込みません、。テキスト ログにエントリ。

-   イベント レベル、インデントの深さ、およびタイムスタンプを含めるかどうかを指定する定数をシステム定義のビットごとの OR のフラグ値します。 イベント レベルが記載されて[テキスト ログのイベント レベルの設定](setting-the-event-level-for-a-text-log.md)します。 テキスト ログは、エントリのイベント レベル以上のイベント レベルを設定する場合**SetupWriteTextLog**ログ エントリを書き込むテキスト ログですそれ以外の場合、 **SetupWriteTextLog**ログは書き込まれません。テキスト ログにエントリ。 インデントを使用すると、セクションで、情報を読み、理解しやすくにように書式設定されたメッセージを配置できます。 詳細については、[インデントのログ エントリの書き込み](writing-indented-log-entries.md)を参照してください。

-   A **printf**-互換性のある形式の文字列メッセージと書式指定文字列に続く変数のコンマ区切りの一覧の両方の形式を設定します。

-   値が書式設定される変数のコンマ区切りの一覧、 **printf**-互換性のある形式の文字列。

呼び出す方法の例については[ **SetupWriteTextLog** ](https://msdn.microsoft.com/library/windows/hardware/ff552218)エラーまたは警告以外のイベントに関する情報をログに[情報ログ エントリの書き込み](writing-an-information-log-entry.md)を参照してください。

呼び出す方法の例については**SetupWriteTextLog**エラーまたは警告に関する情報を記録するを参照してください。[エラーまたは警告のログ エントリの書き込み](writing-an-error-or-warning-log-entry.md)します。

 

 





