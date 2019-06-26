---
title: エラーや警告ログ エントリの書き込み
description: エラーや警告ログ エントリの書き込み
ms.assetid: 80393368-7430-46ca-a53e-c94b7e8acfa0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b561f3e9d26b96fec0f7d5f70e136e1c1fe2437b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363498"
---
# <a name="writing-an-error-or-warning-log-entry"></a>エラーや警告ログ エントリの書き込み


次の例は、アプリケーションが呼び出す可能性があります通常方法[ **SetupWriteTextLog** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextlog)エラーまたは警告のエントリを書き込む、 [SetupAPI テキスト ログ](setupapi-text-logs.md)します。 ただし、イベントが SetupAPI 固有のエラーまたは Win32 エラーに関連付けられている場合は、アプリケーションが呼び出して[ **SetupWriteTextLogError** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextlogerror)代わりにします。 **SetupWriteTextLogError**ログ記録とこれらの種類のエラーについての情報の解釈が容易になります。

呼び出しについては**SetupWriteTextLog** 、エラー メッセージを記録するには、次を参照してください[エラー メッセージをログ記録](#logging-an-error-message)呼び出しについては、 **SetupWriteTextLog**ログ。警告メッセージを参照してください[警告メッセージをログ記録](#logging-a-warning-message)します。

### <a href="" id="logging-an-error-message"></a> エラー メッセージをログ記録

この例で、アプリケーションを呼び出す[ **SetupWriteTextLog**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextlog)、次のパラメーター値を指定します。

-   *LogToken*ログのトークン値を呼び出すことによって取得されたいずれかに設定されている[ **SetupGetThreadLogToken** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupgetthreadlogtoken) で説明されているトークンの値は、システム定義のログの1つまたは[ログイン トークン](log-tokens.md)します。

-   *カテゴリ*TXTLOG_VENDOR で、ログ エントリがベンダーから提供されたアプリケーションによって行われたことを示しますに設定されます。 イベント カテゴリについては、後述[テキスト ログのイベント カテゴリを有効にする](enabling-event-categories-for-a-text-log.md)します。

-   *フラグ*TXTLOG_TIMESTAMP とビットごとの TXTLOG_ERROR またはに設定されます。 この例では、インデント深度が変更されていないとインデントの現在の深さは 5 つの固定幅テキスト スペースに設定されていました。 インデントの深さを変更する方法については、次を参照してください。[インデントのログ エントリの書き込み](writing-indented-log-entries.md)します。 イベント レベルが記載されて、[テキスト ログのイベント レベルの設定](setting-the-event-level-for-a-text-log.md)トピック。

-   *MessageStr*テキスト (「アプリケーション エラー (%d)」) に設定されます。

-   コンマ区切りのリストには、変数のエラー コードが用意されています。

次のコード呼び出し[ **SetupWriteTextLog** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextlog)例ではこのログ エントリの書き込みに。

```cpp
//The LogToken value was previously returned by call to
//SetupGetThreadLogToken or one of the system-defined log token values
DWORD Category = TXTLOG_VENDOR; 
DWORD Flags = TXTLOG_ERROR | TXTLOG_TIMESTAMP;
DWORD ErrorCode = 1111; // An error code value

SetupWriteTextLog(LogToken, Category, Flags, TEXT("Application Error (%d)"),ErrorCode);
```

TXTLOG_VENDOR イベントのカテゴリが有効になっており、TXTLOG_ERROR イベントのレベルは、テキスト ログの設定の場合、このコードは次のように書式設定は、テキスト ログをエントリを作成しました。

```cpp
!!!  2005/02/13 22:06:28.109:    :  Application error (1111) 
```

*Entry_prefix*フィールド"!!! "ログ エントリが、エラー メッセージであることを示します。

### <a href="" id="logging-a-warning-message"></a> 警告メッセージをログ記録

警告メッセージをログ記録は、エラー メッセージをログ記録とほぼ同じです。 違いは、イベント レベルの設定です。 設定*フラグ*TXTLOG_WARNING TXTLOG_ERROR の代わりにします。 場合**SetupWriteTextLog** 」の説明に従ってと呼びます[エラー メッセージをログ記録](#logging-an-error-message)ことを除いて、*フラグ*ビットごとの TXTLOG_WARNING またはと TXTLOG_TIMESTAMP に設定されている[**SetupWriteTextLog** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextlog)は次のログ エントリを記述します。

```cpp
!  2005/02/13 22:06:28.109:    :  Application error (1111) 
```

*Entry_prefix*ログ エントリのフィールドが"です。 "ではなく、警告メッセージがこの"!!! "、これはエラー メッセージを示します。

 

 





