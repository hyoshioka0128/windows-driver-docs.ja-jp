---
title: 情報ログ エントリの書き込み
description: 情報ログ エントリの書き込み
ms.assetid: 624d2a3e-2a11-47fd-941e-1ab59e299821
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34b9c2da14b013ff9fb2b1d9d812a54df0c64978
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538671"
---
# <a name="writing-an-information-log-entry"></a>情報ログ エントリの書き込み


次の例は、アプリケーションが呼び出す可能性があります通常方法[ **SetupWriteTextLog** ](https://msdn.microsoft.com/library/windows/hardware/ff552218)でが information のエントリを書き込む、 [SetupAPI テキスト ログ](setupapi-text-logs.md)が警告ではありませんメッセージまたはエラー メッセージ。

呼び出しについては**SetupWriteTextLog** 、エラー メッセージを記録するには、[エラーや警告のエントリを記録する呼び出し SetupWriteTextLog](writing-an-error-or-warning-log-entry.md)を参照してください。

アプリケーション呼び出し[ **SetupWriteTextLog**](https://msdn.microsoft.com/library/windows/hardware/ff552218)、次のパラメーター値を指定します。

-   *LogToken*ログのトークン値を呼び出すことによって取得されたいずれかに設定されている[ **SetupGetThreadLogToken** ](https://msdn.microsoft.com/library/windows/hardware/ff552211) で説明されているトークンの値は、システム定義のログの1つまたは[ログイン トークン](log-tokens.md)します。

-   *カテゴリ*TXTLOG_VENDOR で、ログ エントリがベンダーから提供されたアプリケーションによって行われたことを示しますに設定されます。 イベント カテゴリについては、後述[テキスト ログのイベント カテゴリを有効にする](enabling-event-categories-for-a-text-log.md)します。

-   *フラグ*TXTLOG_TIMESTAMP とビットごとの TXTLOG_DETAILS またはに設定されます。 この例では、インデント深度が変更されていないとインデントの現在の深さは 5 つの固定幅テキスト スペースに設定されていました。 インデントの深さを変更する方法については、[インデントのログ エントリの書き込み](writing-indented-log-entries.md)を参照してください。 イベント レベルが記載されて、[テキスト ログのイベント レベルの設定](setting-the-event-level-for-a-text-log.md)トピック。

-   *MessageStr*テキストに設定されている ("関心のある変数: %d を =")。

-   パラメーターのコンマ区切りの一覧は、変数を提供*SomeVariable*、"%d"フィールドに対応する*MessageStr*します。

```cpp
//The LogToken value was previously returned by call to
//SetupGetThreadLogToken or one of the system-defined log token values
DWORD Category = TXTLOG_VENDOR; 
DWORD Flags = TXTLOG_DETAILS | TXTLOG_TIMESTAMP;
DWORD SomeVariable = 1;   // The variable whose value will be logged

SetupWriteTextLog(LogToken, Category, Flags, TEXT("Variable of interest: = %d"), SomeVariable);
```

このコードは、タイムスタンプを実際に置き換えられます、次の形式でデバイスのインストール ログにエントリが作成 TXTLOG_VENDOR イベントのカテゴリが有効にし、TXTLOG_DETAILS イベント レベルがデバイスのインストールのテキスト ログの設定、時刻のタイムスタンプ。

```cpp
     2005/02/13 22:06:28.109:    :  Variable of interest: Abc = 1
```

 

 





