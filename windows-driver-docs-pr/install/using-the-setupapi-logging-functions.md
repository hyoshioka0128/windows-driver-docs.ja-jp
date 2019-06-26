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
ms.openlocfilehash: 2a114b1790abe06c0a57947c678e962329bb6026
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384745"
---
# <a name="using-the-setupapi-logging-functions"></a>SetupAPI ログ関数の使用


SetupAPI には、次のように、SetupAPI テキスト ログでログ エントリを記述するアプリケーションのインストール、クラスのインストーラー、および共同インストーラーを使用できる関数がサポートされています。

-   ログ エントリを書き込む、 [SetupAPI テキスト ログ](setupapi-text-logs.md)、インストール アプリケーションを呼び出す[ **SetupWriteTextLog**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextlog)、 [ **SetupWriteTextLogError**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextlogerror)、または[ **SetupWriteTextLogInfLine**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextloginfline)します。 テキスト ログのエントリを記述する方法の詳細については、次を参照してください。[テキスト ログのログ エントリの書き込み](writing-log-entries-in-a-text-log.md)します。

-   SetupAPI ログ スレッドのコンテキストを確立するためのメカニズムをサポートしています。 スレッドのログのトークンを設定してスレッドのログのコンテキストが確立されます。 スレッドのログのトークンを設定するには、インストール アプリケーションを呼び出す[ **SetupSetThreadLogToken**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupsetthreadlogtoken)します。 インストール アプリケーションを呼び出すスレッドのログのトークンを取得する[ **SetupGetThreadLogToken**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupgetthreadlogtoken)します。

    ログのトークンの詳細については、次を参照してください。[ログ トークン](log-tokens.md)します。

    ログのトークンを使用する方法の詳細については、次を参照してください。[設定とスレッドのログのトークン取得](setting-and-getting-a-log-token-for-a-thread.md)します。

 

 





