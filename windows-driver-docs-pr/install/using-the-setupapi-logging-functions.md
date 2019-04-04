---
title: SetupAPI ログ関数の使用
description: SetupAPI ログ関数の使用
ms.assetid: a2ba0da4-b891-4ff9-827b-0d64a7a02c0d
keywords:
- SetupAPI WDK Windows Vista では、関数のログ記録
- WDK SetupAPI 関数
- テキスト ログの WDK SetupAPI、関数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a6d6fe0e7ab9212b359739931bf9be61f45e5bd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578413"
---
# <a name="using-the-setupapi-logging-functions"></a>SetupAPI ログ関数の使用


SetupAPI には、次のように、SetupAPI テキスト ログでログ エントリを記述するアプリケーションのインストール、クラスのインストーラー、および共同インストーラーを使用できる関数がサポートされています。

-   ログ エントリを書き込む、 [SetupAPI テキスト ログ](setupapi-text-logs.md)、インストール アプリケーションを呼び出す[ **SetupWriteTextLog**](https://msdn.microsoft.com/library/windows/hardware/ff552218)、 [ **SetupWriteTextLogError**](https://msdn.microsoft.com/library/windows/hardware/ff552232)、または[ **SetupWriteTextLogInfLine**](https://msdn.microsoft.com/library/windows/hardware/ff552236)します。 テキスト ログのエントリを記述する方法の詳細については、[テキスト ログのログ エントリの書き込み](writing-log-entries-in-a-text-log.md)を参照してください。

-   SetupAPI ログ スレッドのコンテキストを確立するためのメカニズムをサポートしています。 スレッドのログのトークンを設定してスレッドのログのコンテキストが確立されます。 スレッドのログのトークンを設定するには、インストール アプリケーションを呼び出す[ **SetupSetThreadLogToken**](https://msdn.microsoft.com/library/windows/hardware/ff552216)します。 インストール アプリケーションを呼び出すスレッドのログのトークンを取得する[ **SetupGetThreadLogToken**](https://msdn.microsoft.com/library/windows/hardware/ff552211)します。

    ログのトークンの詳細については、[ログ トークン](log-tokens.md)を参照してください。

    ログのトークンを使用する方法の詳細については、[設定とスレッドのログのトークン取得](setting-and-getting-a-log-token-for-a-thread.md)を参照してください。

 

 





