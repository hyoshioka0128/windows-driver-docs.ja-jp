---
title: ユーザー モード DLL で WPP ソフトウェア トレースを初期化する方法
description: ユーザー モード DLL で WPP ソフトウェア トレースを初期化する方法
ms.assetid: 386ed1ba-8a6e-469d-9a03-c8879efd2613
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14d05ffa0b00b0d9d729ba44873347aae7bece58
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329931"
---
# <a name="how-do-i-initialize-wpp-software-tracing-in-a-user-mode-dll"></a>ユーザー モード DLL で WPP ソフトウェア トレースを初期化する方法


Windows XP 以降では、初期化できます WPP トレース ユーザー モード DLL で呼び出すことによって、 [WPP\_INIT\_トレース](https://msdn.microsoft.com/library/windows/hardware/ff556191)WPP ソフトウェア トレースを初期化するためにマクロ。

エラーを回避するには、次のメソッドを使用します。

-   呼び出す、 [WPP\_INIT\_トレース](https://msdn.microsoft.com/library/windows/hardware/ff556191)マクロで、 [DllMain](https://go.microsoft.com/fwlink/p/?linkid=179361) DLL の関数。

-   場合は、DLL は C で記述され、追加、 **\#定義**ステートメントの**WPP\_OLDCC**ソース コードにします。 配置する前に、定義、 **\#含める**のステートメント、[トレース メッセージのヘッダー (.tmh) ファイル](trace-message-header-file.md)します。 **WPP\_OLDCC**定義は C コードでのみ必要です。 C++ の必要はありません。

    次に、例を示します。

    ```
    #define WPP_OLDCC
    #include "init.tmh"
    ```

WPP ソフトウェア トレースを初期化することはできません、 **DllMain** Microsoft Windows 2000 で機能します。 WPP は、Windows 2000 では、サービスの一部として実行される、ので、ソフトウェア トレースの初期化と DLL の初期化中には禁止されていますが、リモート プロシージャ コールが生成されます。

 

 





