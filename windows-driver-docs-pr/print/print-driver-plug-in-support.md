---
title: プリンター ドライバー プラグイン サポート
description: プリンター ドライバー プラグイン サポート
ms.assetid: fa072fc9-66da-46c2-a270-6f604860aaff
keywords:
- 印刷機能の WDK、プラグイン
- IPrintOemPrintTicketProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 380f79f6f43ad1b369ef15574678c53155fcd2ee
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354924"
---
# <a name="print-driver-plug-in-support"></a>プリンター ドライバー プラグイン サポート


ミニドライバー ベースの印刷ドライバーを追加または変更された機能をサポートする必要がありますを提供するドライバー プラグインを印刷、 [IPrintOemPrintTicketProvider インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nn-prcomoem-iprintoemprintticketprovider)を完了し、適切な印刷機能がサポートを提供するにはUnidrv または PScript5 ベースのプリンター ドライバー。 場合、プラグインがサポート**IPrintOemPrintTicketProvider**、プラグインは PrintTicket ドキュメントを編集し、構成ユーザー インターフェイス (UI) を変更することができます。 サポートしてこのインターフェイスでは、GPD または PPD ファイルを編集するだけよりもはるかに多くの開発作業も必要です。

プラグインをサポートしていない、 **IPrintOemPrintTicketProvider**インターフェイスは、既存に制限されます[ **DEVMODEW** ](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)サポートするため、一部の関数をプラグイン。可能性を提供するか、PrintTicket と PrintCapabilities ドキュメントには含まれません。

 

 




