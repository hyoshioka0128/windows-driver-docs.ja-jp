---
title: トレース プロバイダーへの WPP マクロの追加
description: トレース プロバイダーへの WPP マクロの追加
ms.assetid: fc6db47c-ef18-4454-a385-adee1858b9d4
keywords:
- Windows ソフトウェアトレースプリプロセッサ WDK、マクロ
- WPP ソフトウェアトレース WDK、マクロ
- マクロ WDK WPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a2fb3f21653112eee0199fbb05a07f8a102b6cb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840307"
---
# <a name="adding-wpp-macros-to-a-trace-provider"></a>トレース プロバイダーへの WPP マクロの追加


## <span id="ddk_adding_wpp_macros_to_a_driver_tools"></span><span id="DDK_ADDING_WPP_MACROS_TO_A_DRIVER_TOOLS"></span>


カーネルモードドライバーやユーザーモードアプリケーションなど、既定の形式の WPP ソフトウェアトレースを[トレースプロバイダー](trace-provider.md)に追加するには、次の C プリプロセッサディレクティブおよび WPP マクロ呼び出しをプロバイダーのソースコードに追加します。

-   すべての WPP マクロを含む各ソースファイルに、次の形式の **\#include**ディレクティブを含めます。 このステートメントには、各ソースファイルの[WPP プリプロセッサ](wpp-preprocessor.md)によって作成された[トレースメッセージヘッダーファイル](trace-message-header-file.md)が含まれています。

    ```
    #include <source-file-name.tmh>
    ```

    すべての WPP マクロがを呼び出してから、 [wpp\_CONTROL\_guid](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))マクロを定義した後に、トレースメッセージヘッダーファイルをソースファイルに含める必要があります。

-   Wpp\_は、他の WPP マクロを含む各ソースファイルに対して[\_guid](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))定義ディレクティブを制御します。

    この定義では、ドライバーのコントロール GUID とドライバー定義のトレースフラグ名を指定します。 この定義は、ファイルのトレースメッセージヘッダーファイルを含む **\#include**ステートメントの前に、ソースファイルに追加する必要があります。

-   1つの WPP\_、ドライバーのソースコードに対するトレースマクロ呼び出し[\_トレース](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))します。

    ドライバーの場合、このマクロはドライバーのソフトウェアトレースをアクティブにします。 通常、このマクロはドライバーの初期化中に、 [**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンなどで呼び出されます。

    ユーザーモードアプリケーションの場合は、トレースの試行が行われていないソースコードのポイントでこのマクロを呼び出します。

    初期化後、 [Traceview](traceview.md)または[traceview](tracelog.md)を使用して、ソフトウェアトレースセッションを開始し、トレースメッセージを表示することができます。

-   1つの[WPP\_クリーンアップ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556179(v=vs.85))マクロは、[トレースプロバイダーの](trace-provider.md)ソースコードに呼び出します。 このマクロは、ドライバーのソフトウェアトレースを非アクティブにします。

    ドライバーの場合、このマクロ呼び出しは通常、ドライバーの[**アンロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)ルーチンに追加されます。

    ユーザーモードアプリケーションの場合は、最後のトレース試行が行われた後に、ソースコード内の特定の時点でこのマクロを呼び出します。

-   [**DoTraceMessage**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))マクロは、ログトレースメッセージを呼び出します。

 

 





