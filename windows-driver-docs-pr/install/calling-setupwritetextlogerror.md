---
title: SetupWriteTextLogError の呼び出し
description: SetupWriteTextLogError の呼び出し
ms.assetid: 55edc72a-2d53-4084-a1e4-e7e6515a4990
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a217ccd807c5903c1affb9ed2a0e66b0d280814
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385288"
---
# <a name="calling-setupwritetextlogerror"></a>SetupWriteTextLogError の呼び出し


[**SetupWriteTextLogError** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextlogerror) SetupAPI 固有のエラーまたは Win32 エラーに関する情報を書き込みます、 [SetupAPI テキスト ログ](setupapi-text-logs.md)します。 **SetupWriteTextLogError**テキスト ログに 2 つの連続するエントリが書き込まれます最初のエントリが書き込まれたのと同じ形式で同じ情報が含まれています[ **SetupWriteTextLog** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextlog)と。2 番目のエントリは、対応するエラー コードおよびエラーのわかりやすい説明を記録します。

呼び出す**SetupWriteTextLogError**、アプリケーションを呼び出すことが提供するのと同じ情報を提供する**SetupWriteTextLog**し、さらに、SetupAPI 固有のエラーの値を提供またはWin32 エラーがあります。

**SetupWriteTextLogError**次の形式で最初のログ エントリを書き込みます。

*entry_prefix time_stamp カテゴリ* * * * 形式のインデント-メッセージ *

**SetupWriteTextLogError**次の形式で 2 つ目のログ エントリを書き込みます。

*entry_prefix time_stamp カテゴリ* * *<strong>* インデント * **エラー:</strong>* エラー番号のエラーの説明 *

各項目の意味は次のとおりです。

-   *Entry_prefix*、*タイムスタンプ*、*カテゴリ*、*インデント*、および*書式設定されたメッセージ*フィールドは記載されているものと同じ[ログ セクションのテキスト本文の形式](format-of-a-text-log-section-body.md)します。

-   *エラー番号*フィールドには、エラー番号が含まれています。

-   *エラー説明*フィールドには、エラーのわかりやすい説明が含まれています。

次の例は、アプリケーションが呼び出す可能性があります通常方法[ **SetupWriteTextLogError** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextlogerror)テキスト ログのエラーに関する情報を記録します。 この例で使用されるエラーは、システム開始エラーです。 アプリケーション呼び出し**SetupWriteTextLogError**、次のパラメーター値を指定します。

- *LogToken*ログのトークン値を呼び出すことによって取得されたいずれかに設定されている[ **SetupGetThreadLogToken** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupgetthreadlogtoken) で説明されているトークンの値は、システム定義のログの1つまたは[ログイン トークン](log-tokens.md)します。

- *カテゴリ*TXTLOG_VENDOR で、ログ エントリがベンダーから提供されたアプリケーションによって行われたことを示しますに設定されます。 イベント カテゴリについては、後述[テキスト ログのイベント カテゴリを有効にする](enabling-event-categories-for-a-text-log.md)します。

- *LogFlags* TXTLOG_ERROR に設定されます。 この例は、タイムスタンプを含めるまたはインデントの深さの変更はできません。 現在のインデントの深さは 5 つの固定幅テキスト スペース以前に設定されています。 インデントの深さを変更する方法については、次を参照してください。[インデントのログ エントリの書き込み](writing-indented-log-entries.md)します。 イベント レベルが記載されて[テキスト ログのイベント レベルの設定](setting-the-event-level-for-a-text-log.md)します。

- *エラー* ERROR_SERVICE_ALREADY_RUNNING、Win32 エラー コードの値に設定されます。 このエラー コードの 10 進数の値は、1056 です。

- *MessageStr は*TEXT に設定 ("サービスの開始。サービス 'SomeService' を開始できませんでした")。

- パラメーターのコンマ区切りのリストが指定されていない<em>します。</em>

パラメーター *LogToken*、*カテゴリ*、および*LogFlags*の操作に影響を与える**SetupWriteTextLogError**と同じ方法でこれらのパラメーターの動作に影響する**SetupWriteTextLog**します。

次のコード呼び出し[ **SetupWriteTextLogError** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextlogerror)にこの例ではログ エントリを書き込みます。

```cpp
//The LogToken value was previously returned by call to
//SetupGetThreadLogToken or one of the system-defined log token values
DWORD Category = TXTLOG_VENDOR; 
DWORD Flags = TXTLOG_ERROR ;
DWORD ErrorCode = 1056; // The corresponding Win32 error code

SetupWriteTextLog(LogToken, Category, Flags, ErrorCode, TEXT("Start Service: Failed to start service 'SomeService'"),);
```

TXTLOG_VENDOR イベントのカテゴリが有効になっており、TXTLOG_ERROR イベントのレベルは、テキスト ログの設定の場合、このコードは次のように書式設定は、テキスト ログをエントリを作成しました。

```cpp
!!!     :  Start Service: Failed to start service 'SomeService' 
!!!   :  Error 1056: An instance of the service is already running.
```

注意を**SetupWriteTextLogError** 「サービスのインスタンスは既に実行中」です文字列を提供します。 値が 1056 Win32 エラーについて説明します。

 

 





