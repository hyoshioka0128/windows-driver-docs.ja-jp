---
title: 印刷チケットの印刷ドライバーの処理
description: 印刷チケットの印刷ドライバーの処理
ms.assetid: a7295632-0133-4133-b62e-5526dcc12c7d
keywords:
- チケットの WDK の印刷、印刷ドライバーの処理
- 印刷チケット WDK、XPSDrv
- 印刷チケット WDK、GDI ベースの印刷ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1bb37596b19b3f473a3d5159d40a797770017748
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553677"
---
# <a name="print-ticket-processing-in-the-print-driver"></a>印刷チケットの印刷ドライバーの処理


PrintTicket オブジェクトで検証済みの設定は、XPSDrv プリンター ドライバーを実行する印刷処理の構成に使用されます。 印刷ドライバーのコンポーネントそのため、して読み取りが、ドライバーは、これらの設定に従ってドキュメントを処理できるように、ドライバーは処理を実行する前に、印刷チケットで設定を解釈する必要があります。

XPSDrv プリンター ドライバーでは、印刷ドライバーの印刷処理フィルターでこの処理を実行します。

GDI ベースの印刷ドライバーが引き続き使用する、 [ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837)設定、Windows Vista に組み込まれた互換性サポートのため印刷サブシステムを構造体します。 このサポートの詳細については、[Win 32 アプリケーション互換性の印刷チケット](print-ticket-compatibility-with-win-32-applications.md)を参照してください。

印刷チケットの印刷ドライバーの処理を実装する方法の詳細については、[XPSDrv 表示モジュールでの印刷チケット サポート](print-ticket-support-in-the-xpsdrv-render-module.md)を参照してください。

 

 




