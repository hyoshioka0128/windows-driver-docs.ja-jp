---
title: ユーザーモードの DLL で WPP ソフトウェアトレースを初期化操作方法には
description: ユーザーモードの DLL で WPP ソフトウェアトレースを初期化操作方法には
ms.assetid: 386ed1ba-8a6e-469d-9a03-c8879efd2613
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6fdda67c255e8e7c6fe0ff5e251546ddbb41a109
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769640"
---
# <a name="how-do-i-initialize-wpp-software-tracing-in-a-user-mode-dll"></a>ユーザー モード DLL で WPP ソフトウェア トレースを初期化する方法


Windows XP 以降では、wpp [ \_ INIT \_ tracing](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))マクロを呼び出して、wpp ソフトウェアトレースを初期化することにより、ユーザーモード DLL で wpp トレースを初期化できます。

エラーを回避するには、次のメソッドを使用します。

-   DLL の[DllMain](https://docs.microsoft.com/windows/win32/dlls/dllmain)関数で、 [WPP \_ INIT \_ TRACING](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))マクロを呼び出します。

-   DLL が C で記述されている場合は、 **WPP \_ oldcc**の** \# define**ステートメントをソースコードに追加します。 [トレースメッセージヘッダー (tmh) ファイル](trace-message-header-file.md)の** \# include**ステートメントの前に定義を配置します。 **WPP \_ oldcc**定義は、C コードにのみ必要です。 C++ には必要ありません。

    次に例を示します。

    ```
    #define WPP_OLDCC
    #include "init.tmh"
    ```

Microsoft Windows 2000 の**DllMain**関数で、WPP ソフトウェアトレースを初期化することはできません。 WPP は Windows 2000 のサービスの一部として実行されるため、ソフトウェアトレースを初期化すると、DLL の初期化中に使用できないリモートプロシージャコールが生成されます。

 

 





