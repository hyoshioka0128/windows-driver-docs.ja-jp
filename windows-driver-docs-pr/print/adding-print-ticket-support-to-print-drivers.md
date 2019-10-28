---
title: 印刷ドライバーに印刷チケット サポートを追加する
description: 印刷ドライバーに印刷チケット サポートを追加する
ms.assetid: ef4db930-2b4c-40b9-b1f4-85767b7f6855
keywords:
- WDK、印刷チケットをカスタマイズするプリンタードライバー
- プリンタードライバーのカスタマイズ WDK、印刷チケット
- 印刷チケット WDK、サポートの追加
- IPrintTicketProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75be180509e4c22a8d1436eb2ed6ffb6745cb968
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843262"
---
# <a name="adding-print-ticket-support-to-print-drivers"></a>印刷ドライバーに印刷チケット サポートを追加する


印刷[チケットと印刷機能のテクノロジ](print-ticket-and-print-capabilities-technologies.md)を完全にサポートするには、次の印刷ドライバーが必要です。

-   必要に応じて、プリンターの[印刷機能](print-capabilities.md)ドキュメントを提供するために、 [IPrintTicketProvider インターフェイス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554375(v=vs.85))をサポートします。

-   印刷ドライバープラグインの[IPrintOemPrintTicketProvider インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintoemprintticketprovider)をサポートします。

-   印刷ジョブを処理するときに、[印刷チケット](print-ticket.md)情報を使用します。

IPrintTicketProvider インターフェイスをサポートする印刷ドライバーは、前の一覧の最初の2つの項目を行いますが、最後の項目には対応しません。 印刷ドライバーは、XPS ドキュメント内の印刷チケットの設定を読み取って処理し、これらの設定が印刷されたドキュメントに影響を与えるようにする必要があります。 このサポートの実装の詳細については、 [XPSDrv Render モジュールでの印刷チケットのサポートに関するページ](print-ticket-support-in-the-xpsdrv-render-module.md)を参照してください。

**注**   GDI ベース、バージョン3の印刷ドライバーでは、ドライバーに印刷チケットサポートを追加する必要はありません。これは、印刷サブシステムが、PrintTicket オブジェクトを、印刷ドライバーの同等の[**devmodew**](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)構造に変換するためです。

 

 

 




