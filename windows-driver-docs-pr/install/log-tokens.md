---
title: ログのトークン
description: ログのトークン
ms.assetid: f666d457-eb0a-4482-a8ac-e2921ab8c5a9
keywords:
- トークン WDK SetupAPI ログします。
- テキスト ログ WDK SetupAPI、トークンをログに記録します。
- セクションでは WDK SetupAPI ログ記録
- テキスト ログのセクションを識別します。
- SetupAPI WDK Windows Vista では、ログのトークンをログ記録
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec67e2d57826eb4c16336fc46e50414f2a355eff
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557564"
---
# <a name="log-tokens"></a>ログのトークン


SetupAPI テキスト ログは*トークンをログイン*でエントリを書き込む、 [SetupAPI テキスト ログ](setupapi-text-logs.md)します。

クラスのインストーラーまたは共同インストーラーがによって返されるログ トークンを使用する必要があります[ **SetupGetThreadLogToken** ](https://msdn.microsoft.com/library/windows/hardware/ff552211)でログ エントリを書き込む、[テキスト ログ] セクションで](format-of-a-text-log-section.md)が確立されましたSetupAPI インストール操作では、インストーラーを呼び出されます。 SetupAPI テキスト ログには、インストール アプリケーションは、テキスト ログのセクションの一部ではないログ エントリの作成に使用できるは、ログのシステム定義トークンも提供します。

SetupAPI テキスト ログでは、次のログのシステム定義のトークンが用意されています。

<a href="" id="logtoken-unspecified"></a>LOGTOKEN_UNSPECIFIED  
指定されていないテキスト ログの部分を表すの一部を[テキスト ログ セクション](format-of-a-text-log-section.md)します。 既定で、 [SetupAPI ログ関数で](https://msdn.microsoft.com/library/windows/hardware/ff550878)このトークンの値が指定されている場合は、アプリケーションのインストールのテキスト ログでログ エントリを記述します。

<a href="" id="logtoken-no-log"></a>LOGTOKEN_NO_LOG  
Null のログを表します。 SetupAPI ログ関数はログ エントリを記述しないこのトークンの値が指定されているかどうか。

<a href="" id="logtoken-setupapi-applog"></a>LOGTOKEN_SETUPAPI_APPLOG  
アプリケーションのテキスト ログの部分を表す (*SetupAPI.app.log)* 一部ではないテキスト ログのセクションの。 [SetupAPI ログ関数で](https://msdn.microsoft.com/library/windows/hardware/ff550878)このトークンの値が指定されている場合、アプリケーション インストールのテキスト ログでログ エントリを記述します。

<a href="" id="logtoken-setupapi-devlog"></a>LOGTOKEN_SETUPAPI_DEVLOG  
デバイス インストールのテキスト ログの部分を表す (*SetupAPI.dev.log)* 一部ではないテキスト ログのセクションの。 SetupAPI ログ関数は、このトークンの値が指定されている場合、デバイスのインストールのテキスト ログでログ エントリを記述します。

 

 





