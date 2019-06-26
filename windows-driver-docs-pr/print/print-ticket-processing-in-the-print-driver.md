---
title: 印刷ドライバーの印刷チケット処理
description: 印刷ドライバーの印刷チケット処理
ms.assetid: a7295632-0133-4133-b62e-5526dcc12c7d
keywords:
- チケットの WDK の印刷、印刷ドライバーの処理
- 印刷チケット WDK、XPSDrv
- 印刷チケット WDK、GDI ベースの印刷ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8aff80f8e99642a166167d3e564e9b515aa4f92c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354917"
---
# <a name="print-ticket-processing-in-the-print-driver"></a>印刷ドライバーの印刷チケット処理


PrintTicket オブジェクトで検証済みの設定は、XPSDrv プリンター ドライバーを実行する印刷処理の構成に使用されます。 印刷ドライバーのコンポーネントそのため、して読み取りが、ドライバーは、これらの設定に従ってドキュメントを処理できるように、ドライバーは処理を実行する前に、印刷チケットで設定を解釈する必要があります。

XPSDrv プリンター ドライバーでは、印刷ドライバーの印刷処理フィルターでこの処理を実行します。

GDI ベースの印刷ドライバーが引き続き使用する、 [ **DEVMODEW** ](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)設定、Windows Vista に組み込まれた互換性サポートのため印刷サブシステムを構造体します。 このサポートの詳細については、次を参照してください。 [Win 32 アプリケーション互換性の印刷チケット](print-ticket-compatibility-with-win-32-applications.md)します。

印刷チケットの印刷ドライバーの処理を実装する方法の詳細については、次を参照してください。 [XPSDrv 表示モジュールでの印刷チケット サポート](print-ticket-support-in-the-xpsdrv-render-module.md)します。

 

 




