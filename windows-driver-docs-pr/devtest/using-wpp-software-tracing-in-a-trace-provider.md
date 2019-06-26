---
title: トレース プロバイダーでの WPP ソフトウェア トレースの使用
description: トレース プロバイダーでの WPP ソフトウェア トレースの使用
ms.assetid: e215a99b-5082-4e81-84b6-184a2fd4e270
keywords:
- Windows ソフトウェア トレース プリプロセッサ WDK、WPP について
- WDK、WPP に関するトレース WPP ソフトウェア
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d0f5bda5d9026d4be87a79d2a31295f20a40006
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381818"
---
# <a name="using-wpp-software-tracing-in-a-trace-provider"></a>トレース プロバイダーでの WPP ソフトウェア トレースの使用


## <span id="ddk_using_wpp_software_tracing_in_a_driver_tools"></span><span id="DDK_USING_WPP_SOFTWARE_TRACING_IN_A_DRIVER_TOOLS"></span>


WPP ソフトウェア トレースの既定の形式を使用する、[トレース プロバイダー](trace-provider.md)カーネル モード ドライバーまたはユーザー モード アプリケーションを次の操作など。

-   コントロールを一意に識別する GUID 定義、[トレース プロバイダー](trace-provider.md)します。 プロバイダーの定義にこの GUID を指定する、 [WPP\_コントロール\_GUID](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))マクロや関連するコントロール ファイルで使用される[Tracelog](tracelog.md)します。

-   必要な追加 WPP に関連する C プリプロセッサ ディレクティブと WPP マクロの呼び出しをプロバイダーのソース、ファイル、」の説明に従って[WPP マクロをトレース プロバイダーを追加する](adding-wpp-macros-to-a-trace-provider.md)し、 [WPP ソフトウェア トレース参照](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556205(v=vs.85))。

-   」の説明に従って、ドライバーをビルド[WPP プリプロセッサ](wpp-preprocessor.md)します。

-   などのソフトウェア トレース、その他のツールを使用して[traceview で](traceview.md)、 [Tracelog](tracelog.md)、 [Tracefmt](tracefmt.md)、および[Tracepdb](tracepdb.md)構成、起動、および停止するにはセッションのトレースを表示し、トレース メッセージをフィルター処理するとします。 Windows Driver Kit (WDK) でこれらのツールが含まれて、\\ツール\\トレース ディレクトリ。

 

 





