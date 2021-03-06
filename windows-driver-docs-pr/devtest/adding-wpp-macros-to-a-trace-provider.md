---
title: トレース プロバイダーへの WPP マクロの追加
description: トレース プロバイダーへの WPP マクロの追加
ms.assetid: fc6db47c-ef18-4454-a385-adee1858b9d4
keywords:
- Windows ソフトウェア トレース プリプロセッサ WDK、マクロ
- WDK、マクロをトレース WPP ソフトウェア
- WDK WPP マクロ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac55b640ebc38669e8754de2d192011356a216a3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371464"
---
# <a name="adding-wpp-macros-to-a-trace-provider"></a>トレース プロバイダーへの WPP マクロの追加


## <span id="ddk_adding_wpp_macros_to_a_driver_tools"></span><span id="DDK_ADDING_WPP_MACROS_TO_A_DRIVER_TOOLS"></span>


WPP ソフトウェア トレースの既定のフォームを追加する、[トレース プロバイダー](trace-provider.md)カーネル モード ドライバーまたはユーザー モード アプリケーションを追加、次の C# プリプロセッサ ディレクティブとプロバイダーのソース コードに WPP マクロの呼び出しなど。

-   **\#含める**WPP のすべてのマクロを含む各ソース ファイルに次の形式のディレクティブ。 このステートメントが含まれる、[トレース メッセージのヘッダー ファイル](trace-message-header-file.md)によって作成された、 [WPP プリプロセッサ](wpp-preprocessor.md)ソース ファイルごとに。

    ```
    #include <source-file-name.tmh>
    ```

    トレース メッセージのヘッダー ファイルは、WPP マクロ呼び出しの前に、定義した後は、ソース ファイルに含める必要がある、 [WPP\_コントロール\_GUID](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))マクロ。

-   A [WPP\_コントロール\_GUID](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))他 WPP マクロを含む各ソース ファイルにディレクティブを定義します。

    この定義は、ドライバーのコントロールの GUID とドライバー定義のトレース フラグの名前を指定します。 定義する前にソース ファイルに追加する必要があります、 **\#含める**ファイルのトレース メッセージのヘッダー ファイルを含むステートメント。

-   1 つ[WPP\_INIT\_トレース](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))マクロの呼び出し、ドライバーのソース コードにします。

    ドライバーは、このマクロは、ドライバーでのソフトウェアのトレースをアクティブにします。 このマクロは通常初期化中に呼び出さドライバー、たとえば、 [ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ルーチン。

    ユーザー モード アプリケーションでは、場所トレース試行以前加えられていない時点のソース コードでこのマクロを呼び出します。

    初期化後は、使用することができます[traceview で](traceview.md)または[Tracelog](tracelog.md)ソフトウェア トレース セッションを開始して、トレース メッセージを表示します。

-   1 つ[WPP\_クリーンアップ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556179(v=vs.85))マクロの呼び出し、[トレース プロバイダーの](trace-provider.md)ソース コード。 このマクロは、ドライバーでのソフトウェアのトレースを無効になります。

    ドライバーは、このマクロの呼び出しは通常、ドライバーに追加[**アンロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)ルーチン。

    ユーザー モード アプリケーションでは、トレースの最後の試行が行われた後、ソース コード内でこのマクロを呼び出します。

-   [**DoTraceMessage** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))マクロの呼び出しをトレース メッセージを記録します。

 

 





