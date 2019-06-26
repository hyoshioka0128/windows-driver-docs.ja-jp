---
title: SetupWriteTextLog の呼び出し
description: SetupWriteTextLog の呼び出し
ms.assetid: a07118ae-bef6-4d01-94d9-98587cbff863
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f773a992c586959a5c2e976132b8e1b03e0665f3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385281"
---
# <a name="calling-setupwritetextlog"></a>SetupWriteTextLog の呼び出し


[**SetupWriteTextLog** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextlog)インストール イベントに関する情報を含む 1 つのエントリを追加、 [SetupAPI テキスト ログ](setupapi-text-logs.md)します。

」の説明に従って[ログ セクションのテキスト本文の形式](format-of-a-text-log-section-body.md)、ログ エントリの形式は次のフィールドで構成されます。

```cpp
entry_prefix time_stamp event_category indentation formatted_message
```

呼び出す**SetupWriteTextLog**、次の情報をアプリケーションに渡します。

-   ログのトークンを呼び出すことによって取得されたテキスト ログのセクション[ **SetupGetThreadLogToken**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupgetthreadlogtoken)、またはシステム定義の 1 つ[トークンをログイン](log-tokens.md)します。 ログのトークンは、テキスト ログ セクションに関連付けられた場合**SetupWriteTextLog**そのセクションにログ エントリを書き込みます。 それ以外の場合、 **SetupWriteTextLog**テキスト ログ セクションに含まれていないログの一部にログ エントリを追加します。 さらに、かどうか**SetupWriteTextLog** 、ログ エントリを書き込みますとテキスト ログ**SetupWriteTextLog**エントリを書き込む、ログのシステム定義のトークン値に依存します。

    ログのトークンの詳細については、次を参照してください。[設定とスレッドのログのトークン取得](setting-and-getting-a-log-token-for-a-thread.md)します。

-   記載されているイベントのカテゴリの 1 つ[テキスト ログのイベント カテゴリを有効にする](enabling-event-categories-for-a-text-log.md)します。 テキスト ログのエントリのイベント カテゴリが有効になっている場合[ **SetupWriteTextLog** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextlog)テキスト ログにエントリを追加しますそれ以外の場合、 **SetupWriteTextLog**書き込みません、。テキスト ログにエントリ。

-   イベント レベル、インデントの深さ、およびタイムスタンプを含めるかどうかを指定する定数をシステム定義のビットごとの OR のフラグ値します。 イベント レベルが記載されて[テキスト ログのイベント レベルの設定](setting-the-event-level-for-a-text-log.md)します。 テキスト ログは、エントリのイベント レベル以上のイベント レベルを設定する場合**SetupWriteTextLog**ログ エントリを書き込むテキスト ログですそれ以外の場合、 **SetupWriteTextLog**ログは書き込まれません。テキスト ログにエントリ。 インデントを使用すると、セクションで、情報を読み、理解しやすくにように書式設定されたメッセージを配置できます。 詳細については、次を参照してください。[インデントのログ エントリの書き込み](writing-indented-log-entries.md)します。

-   A **printf**-互換性のある形式の文字列メッセージと書式指定文字列に続く変数のコンマ区切りの一覧の両方の形式を設定します。

-   値が書式設定される変数のコンマ区切りの一覧、 **printf**-互換性のある形式の文字列。

呼び出す方法の例については[ **SetupWriteTextLog** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextlog)エラーまたは警告以外のイベントに関する情報をログに次を参照してください。[情報ログ エントリの書き込み](writing-an-information-log-entry.md)します。

呼び出す方法の例については**SetupWriteTextLog**エラーまたは警告に関する情報を記録するを参照してください。[エラーまたは警告のログ エントリの書き込み](writing-an-error-or-warning-log-entry.md)します。

 

 





