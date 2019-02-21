---
title: 印刷ドライバーに対して印刷チケットのサポートを追加します。
description: 印刷ドライバーに対して印刷チケットのサポートを追加します。
ms.assetid: ef4db930-2b4c-40b9-b1f4-85767b7f6855
keywords:
- プリンター ドライバーの WDK、印刷チケットをカスタマイズします。
- プリンター ドライバー WDK、印刷チケットをカスタマイズします。
- 印刷チケット WDK、サポートの追加
- IPrintTicketProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17456eaef415b5570a65695bca153e698f62c1e7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529179"
---
# <a name="adding-print-ticket-support-to-print-drivers"></a>印刷ドライバーに対して印刷チケットのサポートを追加します。


完全にサポートするために、[印刷チケットと印刷機能のテクノロジ](print-ticket-and-print-capabilities-technologies.md)、印刷ドライバーにする必要があります。

-   サポート、 [IPrintTicketProvider インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff554375)を提供する、必要に応じて、[印刷機能](print-capabilities.md)プリンターのドキュメント。

-   サポート、 [IPrintOemPrintTicketProvider インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff553174)で印刷ドライバーにプラグインします。

-   使用して、[印刷チケット](print-ticket.md)については、印刷ジョブを処理するときにします。

IPrintTicketProvider インターフェイスをサポートする印刷ドライバーでは、上記のリストの最初の 2 つの項目の実行が、最後の項目は扱いません。 印刷ドライバーの読み込みし、これらの設定が印刷されるドキュメントに影響するために、XPS ドキュメントの印刷チケットの設定を処理する必要があります。 このサポートの実装の詳細については、次を参照してください。 [XPSDrv 表示モジュールでサポートして印刷チケット](print-ticket-support-in-the-xpsdrv-render-module.md)します。

**注**   GDI ベース バージョン 3 の印刷ドライバー必要はありません、印刷サブシステムは、それと等価な PrintTicket オブジェクトを変換するため、ドライバーに印刷チケットのサポートを追加する[ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837)印刷ドライバーの構造体。

 

 

 




