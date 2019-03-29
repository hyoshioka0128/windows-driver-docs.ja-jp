---
title: トレース プロバイダーでの WPP ソフトウェア トレースの使用
description: トレース プロバイダーでの WPP ソフトウェア トレースの使用
ms.assetid: e215a99b-5082-4e81-84b6-184a2fd4e270
keywords:
- Windows ソフトウェア トレース プリプロセッサ WDK、WPP について
- WDK、WPP に関するトレース WPP ソフトウェア
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79be44e1a36d0108ec7c9017f6f1a1a043dce07c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570582"
---
# <a name="using-wpp-software-tracing-in-a-trace-provider"></a>トレース プロバイダーでの WPP ソフトウェア トレースの使用


## <span id="ddk_using_wpp_software_tracing_in_a_driver_tools"></span><span id="DDK_USING_WPP_SOFTWARE_TRACING_IN_A_DRIVER_TOOLS"></span>


WPP ソフトウェア トレースの既定の形式を使用する、[トレース プロバイダー](trace-provider.md)カーネル モード ドライバーまたはユーザー モード アプリケーションを次の操作など。

-   コントロールを一意に識別する GUID 定義、[トレース プロバイダー](trace-provider.md)します。 プロバイダーの定義にこの GUID を指定する、 [WPP\_コントロール\_GUID](https://msdn.microsoft.com/library/windows/hardware/ff556186)マクロや関連するコントロール ファイルで使用される[Tracelog](tracelog.md)します。

-   必要な追加 WPP に関連する C プリプロセッサ ディレクティブと WPP マクロの呼び出しをプロバイダーのソース、ファイル、」の説明に従って[WPP マクロをトレース プロバイダーを追加する](adding-wpp-macros-to-a-trace-provider.md)し、 [WPP ソフトウェア トレース参照](https://msdn.microsoft.com/library/windows/hardware/ff556205)。

-   」の説明に従って、ドライバーをビルド[WPP プリプロセッサ](wpp-preprocessor.md)します。

-   などのソフトウェア トレース、その他のツールを使用して[traceview で](traceview.md)、 [Tracelog](tracelog.md)、 [Tracefmt](tracefmt.md)、および[Tracepdb](tracepdb.md)構成、起動、および停止するにはセッションのトレースを表示し、トレース メッセージをフィルター処理するとします。 Windows Driver Kit (WDK) でこれらのツールが含まれて、\\ツール\\トレース ディレクトリ。

 

 





