---
title: スレッド用のログ トークンの設定と取得
description: スレッド用のログ トークンの設定と取得
ms.assetid: 6c701b91-ae0a-48ba-a1e0-711fc21eaf60
keywords:
- テキスト ログの WDK SetupAPI、ログのコンテキスト
- コンテキスト WDK SetupAPI ログします。
- SetupGetThreadLogToken
- SetupAPI WDK Windows Vista では、ログのコンテキストのログ記録
- トークン WDK SetupAPI ログします。
- スレッドのログは、WDK SetupAPI をトークンします。
- SetupSetThreadLogToken
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c540a0e182942d4ad980a4646d2cd9b32332e5ad
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386880"
---
# <a name="setting-and-getting-a-log-token-for-a-thread"></a>スレッド用のログ トークンの設定と取得


[SetupAPI ログ](setupapi-logging--windows-vista-and-later-.md)スレッドのログのコンテキストを確立するメカニズムをサポートしています。 設定によってこのコンテキストが確立されている、[ログ トークン](log-tokens.md)スレッド。 SetupAPI では、このメカニズムを提供するため、スレッドによって呼び出されるコードは、呼び出し元のスレッドのログのコンテキストにログ エントリを書き込むことができます。

たとえば、スレッドはクラス インストーラーまたは共同インストーラーを呼び出す前に、ログのコンテキストのログのトークンを設定できます。 インストーラーして、呼び出し元スレッドのログのトークンを取得がそのトークンを使用して、テキスト ログと、呼び出し元スレッドのログのコンテキストに関連付けられているセクションにログ エントリを書き込むことができます。

### <a href="" id="setting-a-log-token-for-a-thread"></a> スレッドのログのトークンの設定

[ **SetupSetThreadLogToken** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupsetthreadlogtoken)関数は、この関数の呼び出し元のスレッドのログのトークンを設定します。 ログのシステム定義トークンまたは呼び出すことによって取得されたログ トークンかまいませんログ トークン[ **SetupGetThreadLogToken**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupgetthreadlogtoken)します。

スレッドのログのコンテキストの確立方法の例を次に示します。

-   インストール アプリケーションを呼び出すことができます**SetupSetThreadLogToken**同じスレッド内で実行される他のインストール コードでログのコンテキストを確立します。 システム定義、アプリケーションで使用するスレッドのログのコンテキストを確立するにはとき、[ログ トークン](log-tokens.md)への呼び出しで、LOGTOKEN_SETUPAPI_APPLOG など**SetupSetThreadLogToken**します。

    **注**  システム定義を使用してログのコンテキストを設定するかどうか[ログ トークン](log-tokens.md)、以降への呼び出し、 [SetupAPI ログ記録関数を](https://docs.microsoft.com/previous-versions/ff550878(v=vs.85))そのログ コンテキストからに対して行われる、ログの書き込みインストールのテキスト ログにエントリの一部を[テキスト ログ セクション](format-of-a-text-log-section.md)します。

     

-   クラスのインストーラーまたは共同インストーラーは、新しいスレッドを起動する場合、インストーラーは親スレッドと同じにするには、そのスレッドのログのコンテキストを設定できます。 これは、次のように行います。
    1.  親スレッドが新しいスレッドを開始する前に呼び出すことによって、現在のログ トークンを獲得[ **SetupGetThreadLogToken**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupgetthreadlogtoken)します。
    2.  親スレッドは、新しいスレッドを開始し、グローバル変数に、トークンを保存するなど、実装固有メソッドを通じて現在のログのトークンを渡します。
    3.  スレッドの新しい呼び出し[ **SetupSetThreadLogToken** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupsetthreadlogtoken)ログの現在のトークンを使用します。 その結果、新しいスレッド""ログのコンテキストを継承親スレッド。

    **注**  クラス インストーラーまたは共同インストーラーのスレッドは、このメソッドは、後続の呼び出しを使用してログのコンテキストを設定する場合、 [SetupAPI ログ記録関数を](https://docs.microsoft.com/previous-versions/ff550878(v=vs.85))がそのコンテキスト書き込みログにログ エントリから行われる、インストールのテキスト ログの一部である可能性があります、[テキスト ログ セクション](format-of-a-text-log-section.md)します。 これは、テキストのログ セクションでは、インストーラーが呼び出される SetupAPI インストール操作によって確立された場合にのみ発生します。

     

呼び出しの例を次に**SetupSetThreadLogToken**デバイス インストールのテキスト ログに、現在のスレッドのログのコンテキストを設定する (*SetupAPI.app.log)* 指定することで、LOGTOKEN_SETUPAPI_APPLOG のログのシステム定義トークンです。 後続の呼び出しを[SetupAPI ログ記録関数を](https://docs.microsoft.com/previous-versions/ff550878(v=vs.85))ことはこのログのコンテキストはログ エントリの書き込みをデバイス インストールのテキスト ログがの一部ではなく、[テキスト ログ セクション](format-of-a-text-log-section.md)します。

```cpp
SP_LOG_TOKEN LogToken = LOGTOKEN_SETUPAPI_APPLOG;
SetupSetThreadLogToken(LogToken);
```

### <a href="" id="getting-a-log-token-for-a-thread"></a> スレッドのログをトークンの取得

[ **SetupGetThreadLogToken** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupgetthreadlogtoken)関数は、この関数の呼び出し元のスレッドのログのトークンを取得します。

たとえば、クラスのインストーラーを呼び出すことができます**SetupGetThreadLogToken**クラスのインストーラーと呼ばれる SetupAPI 操作に適用されるログ トークンを取得します。 クラスのインストーラーは、対応する SetupAPI 操作に適用されるテキスト ログのログ エントリにこのログを取得したトークンを使用できます。

**注**  への呼び出しによってスレッドのログのコンテキストが以前設定されていなかった場合[ **SetupSetThreadLogToken**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupsetthreadlogtoken)への呼び出し**SetupGetThreadLogToken**LOGTOKEN_UNSPECIFIED の値を持つログ トークンを返します。

 

呼び出しの例を次に**SetupGetThreadLogToken**現在のスレッドのログのトークンを取得します。

```cpp
SP_LOG_TOKEN LogToken = SetupGetThreadLogToken();
```

 

 





