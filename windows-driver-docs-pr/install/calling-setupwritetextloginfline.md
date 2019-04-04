---
title: SetupWriteTextLogInfLine の呼び出し
description: SetupWriteTextLogInfLine の呼び出し
ms.assetid: 7b7a08bf-b97a-4dfe-8695-dc947481ad2b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c932f0b1c5d72d22a25404ab0577c0e4d5e3acaf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573231"
---
# <a name="calling-setupwritetextloginfline"></a>SetupWriteTextLogInfLine の呼び出し


アプリケーションが呼び出すことができます[ **SetupWriteTextLogInfLine** ](https://msdn.microsoft.com/library/windows/hardware/ff552236)でログ エントリを書き込む、 [SetupAPI テキスト ログ](setupapi-text-logs.md)INF ファイルの指定した行のテキストを格納しています。

呼び出す**SetupWriteTextLogInfLine**アプリケーションは、次の情報を提供します。

-   ログのトークンを呼び出すことによって取得されたテキスト ログのセクション[ **SetupGetThreadLogToken** ](https://msdn.microsoft.com/library/windows/hardware/ff552211)またはシステム定義の 1 つ[トークンをログイン](log-tokens.md)します。 ログのトークンは、テキスト ログ セクションに関連付けられた場合**SetupWriteTextLogInfLine**そのセクションにログ エントリを書き込みます。 それ以外の場合、 **SetupWriteTextLogInfLine**テキスト ログ セクションに含まれていないログの一部にログ エントリを追加します。

    さらに、かどうか**SetupWriteTextLogInfLine** 、ログ エントリを書き込みますとテキスト ログ**SetupWriteTextLogInfLine**エントリを書き込む、ログのシステム定義のトークン値に依存します。

    ログのトークンの詳細については、[設定とスレッドのログのトークン取得](setting-and-getting-a-log-token-for-a-thread.md)を参照してください。

-   イベント レベル、インデントの深さ、およびタイムスタンプを含めるかどうかを指定する定数をシステム定義のビットごとの OR のフラグ値します。 イベント レベルが記載されて[テキスト ログのイベント レベルの設定](setting-the-event-level-for-a-text-log.md)します。

    テキスト ログは、エントリのイベント レベル以上のイベント レベルを設定する場合[ **SetupWriteTextLogInfLine** ](https://msdn.microsoft.com/library/windows/hardware/ff552236)テキスト ログでログ エントリを書き込みます。 それ以外の場合、 **SetupWriteTextLogInfLine**テキスト ログでログ エントリは書き込まれません。 インデントを使用すると、セクションで、情報を読み、理解しやすくにように書式設定されたメッセージを配置できます。

    詳細については、[インデントのログ エントリの書き込み](writing-indented-log-entries.md)を参照してください。

-   INF ファイルの行を格納している INF ファイルへのハンドル。

-   INF ファイルの行のコンテキスト。

**SetupWriteTextLogInfLine**次の形式でログ エントリを書き込みます。

*entry_prefix time_stamp* **inf:**<em>インデント inf 行テキスト</em> **(**<em>inf ファイル名</em>**行** <em>行番号</em>**)**

各項目の意味は次のとおりです。

-   *Entry_prefix*、*タイムスタンプ*、および*インデント*フィールドは記載されているものと同じ[テキストログセクション本文の形式](format-of-a-text-log-section-body.md).

-   **Inf:** フィールドを TXTLOG_INF イベント カテゴリを指定します。 イベント カテゴリについては、後述[テキスト ログのイベント カテゴリを有効にする](enabling-event-categories-for-a-text-log.md)します。

-   *Inf を行テキスト*フィールドに指定した INF ファイルの行のテキストが含まれています。

-   *Inf ファイル名*フィールドに指定した INF ファイルの行を格納している INF ファイルの名前が含まれています。

-   **行**フィールドでは、次に示しますが、INF ファイル内の行番号であることを示します。

-   *行番号*フィールドには、INF ファイルで指定した行の行番号が含まれています。

ログインする方法をアプリケーションが通常、INF 行のテキスト テキスト ログの例は、次のとおりです。 この例では、INF 行は、INF **AddReg**行。 アプリケーション呼び出し[ **SetupWriteTextLogInfLine**](https://msdn.microsoft.com/library/windows/hardware/ff552236)、次の入力パラメーターの値を指定します。

-   *LogToken*によって返されたログ トークンに設定されている[ **SetupGetThreadLogToken** ](https://msdn.microsoft.com/library/windows/hardware/ff552211)またはシステム定義[ログ トークン](log-tokens.md)します。

-   *LogFlags* TXTLOG_DETAILS に設定されます。 この例は、タイムスタンプを含めるまたはインデントの深さの変更はできません。 例では、インデントの深さは 5 つの固定幅テキスト スペースが。

-   *InfHandle* INF ファイルへのハンドルに設定されている*hidserv.inf します。* このハンドルは呼び出すことによって取得、 **SetupOpenInfFile**関数で、プラットフォーム SDK に記載されています。

-   *コンテキスト*テキストを含む INF ファイルの行の INF ファイルのコンテキストに設定されている"AddReg HidServ_AddService_AddReg を = です"。 行に対して、INF ファイルのコンテキストが呼び出すことによって取得、 **SetupFind*Xxx*行**関数で、プラットフォーム SDK に記載されています。

値*LogToken*と*LogFlags*の操作に影響を与える[ **SetupWriteTextLogInfLine** ](https://msdn.microsoft.com/library/windows/hardware/ff552236)説明したものと同じ方法で[ **SetupWriteTextLog**](https://msdn.microsoft.com/library/windows/hardware/ff552218)します。 さらに、 **SetupWriteTextLogInfLine** TXTLOG_INF イベント カタログを使用します。

この例では、次に示しますログ エントリの種類を**SetupWriteTextLogInfLine**テキスト ログに書き込みます。

```cpp
   inf:      AddReg=HidServ_AddService_AddReg  (hidserv.inf line 98)
```

 

 





