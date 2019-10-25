---
title: プリンター ドライバー プラグイン サポート
description: プリンター ドライバー プラグイン サポート
ms.assetid: fa072fc9-66da-46c2-a270-6f604860aaff
keywords:
- 印刷機能 WDK、プラグイン
- IPrintOemPrintTicketProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf3864edb10125695e96dc9ea357f77e295af646
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842347"
---
# <a name="print-driver-plug-in-support"></a>プリンター ドライバー プラグイン サポート


ミニドライバーベースの印刷ドライバーに追加または変更された機能を提供する印刷ドライバープラグインは、 [IPrintOemPrintTicketProvider インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintoemprintticketprovider)をサポートして、Unidrv またはの印刷機能を完全かつ適切にサポートする必要があります。PScript5 ベースの印刷ドライバー。 プラグインが**IPrintOemPrintTicketProvider**をサポートしている場合、プラグインによって、PrintTicket ドキュメントを編集し、構成ユーザーインターフェイス (UI) を変更する機能が得られます。 ただし、このインターフェイスのサポートも、GPD ファイルまたは PPD ファイルを編集するだけではなく、はるかに多くの開発作業が必要です。

**IPrintOemPrintTicketProvider**インターフェイスをサポートしていないプラグインは、既存の[**devmodew**](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)サポートに限定されるため、プラグインによって提供される一部の関数は、PrintTicket ドキュメントまたは PrintCapabilities ドキュメントに含まれない可能性があります。

 

 




