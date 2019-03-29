---
title: プリンター ドライバー プラグイン サポート
description: プリンター ドライバー プラグイン サポート
ms.assetid: fa072fc9-66da-46c2-a270-6f604860aaff
keywords:
- 印刷機能の WDK、プラグイン
- IPrintOemPrintTicketProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4edb3b4df5a265e22c8a97f07da02336b20ef474
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581618"
---
# <a name="print-driver-plug-in-support"></a>プリンター ドライバー プラグイン サポート


ミニドライバー ベースの印刷ドライバーを追加または変更された機能をサポートする必要がありますを提供するドライバー プラグインを印刷、 [IPrintOemPrintTicketProvider インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff553174)を完了し、適切な印刷機能がサポートを提供するにはUnidrv または PScript5 ベースのプリンター ドライバー。 場合、プラグインがサポート**IPrintOemPrintTicketProvider**、プラグインは PrintTicket ドキュメントを編集し、構成ユーザー インターフェイス (UI) を変更することができます。 サポートしてこのインターフェイスでは、GPD または PPD ファイルを編集するだけよりもはるかに多くの開発作業も必要です。

プラグインをサポートしていない、 **IPrintOemPrintTicketProvider**インターフェイスは、既存に制限されます[ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837)サポートするため、一部の関数をプラグイン。可能性を提供するか、PrintTicket と PrintCapabilities ドキュメントには含まれません。

 

 




