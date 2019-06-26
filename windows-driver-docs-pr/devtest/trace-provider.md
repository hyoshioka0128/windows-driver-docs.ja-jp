---
title: トレース プロバイダー
description: トレース プロバイダー
ms.assetid: 06fcb37b-6cc3-4e64-8f53-86634836c7bd
keywords:
- トレース プロバイダー WDK
- イベント トレースの Windows WDK、プロバイダー
- WDK ETW プロバイダー
- プロバイダーの WDK ソフトウェア トレース
- WDK、プロバイダーのセッションをトレースします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f49b596c93436c90cede7302749bc09fb0f852c9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381905"
---
# <a name="trace-provider"></a>トレース プロバイダー


## <span id="ddk_trace_provider_tools"></span><span id="DDK_TRACE_PROVIDER_TOOLS"></span>


A*トレース プロバイダー*トレース メッセージまたはトレース イベントを生成するには、Event Tracing for Windows (ETW) テクノロジを使用してユーザー モード アプリケーションまたはカーネル モード ドライバーのコンポーネントです。 通常、トレース イベントとメッセージは、プロバイダーの個別のアクションを報告します。 イベントのレコードを読み取ると、実際の動作条件で、プロバイダーの実行内容を理解するのに役立ちます。

A[トレース セッション](trace-session.md)トレース プロバイダーの 1 つ以上を含めることができます。 これは、トレースのドライバーやアプリケーションは、複数のプロバイダー コンポーネントを実装すると複数のドライバーまたは対話するアプリケーションをトレースするために特に便利です。

1 つ以上のトレース プロバイダーのトレース セッションを開始するに指定する必要があります、[制御 Guid](control-guid.md)のすべての必要なプロバイダーに送信した GUID (.guid 拡張子) またはコントロール ファイルで、[トレース コント ローラー](trace-controller.md). イベントのトレース ログ (.etl) ファイルには、プロバイダーによって生成されたトレース メッセージが挿入されました。

カーネル モード ドライバーまたはユーザー モードのアプリケーションは、1 つのソース ファイル内であっても、1 つ以上のトレース プロバイダー コンポーネントをサポートできます。 この機能は、ドライバーまたはアプリケーションで特定の操作をトレースする場合に便利です。 複数のトレース プロバイダーを実装する必要があります使用する、異なる[コントロール GUID](control-guid.md)で、 [WPP\_コントロール\_GUID](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))プロバイダーごとにマクロ。

同様に、複数のドライバーやアプリケーション、1 つのトレース プロバイダーの一部であるでき、リソースを共有できます。 この機能は、関連アプリケーションとドライバー、ポートおよびミニポートのドライバーなどをトレースする場合に便利です。 この機能を実装するには、WPP で同じコントロールの GUID を指定します。\_コントロール\_プロバイダーごとに GUID マクロ。
