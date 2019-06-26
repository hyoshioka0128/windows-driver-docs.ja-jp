---
title: WDI セレクティブ サスペンド機能登録
description: USB のセレクティブ サスペンドの機能を登録するためのフロー ダイアグラムを次に示します。
ms.assetid: E4AE424F-2017-4111-B4C7-DF0BA6A40A15
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5108c11e1832033fda4c92de96e0581a1c4cdc7f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384347"
---
# <a name="wdi-selective-suspend-capability-registration"></a>WDI セレクティブ サスペンド機能登録


USB のセレクティブ サスペンドの機能を登録するためのフロー ダイアグラムを次に示します。

![選択的 wdi 中断機能の登録](images/wdi-register-usb-selective-suspend-flow.png)

AdapterCap(PM(ss))、 \*SelectiveSuspend、 **LeIdleNotificationHandler**、および**LeCancelIdleNotificationHandler** true または WDI WLAN 選択をサポートしている登録を有効にする必要があります中断します。

WDI はセレクティブ サスペンドをサポートすることが決定したら、WDI も NDIS に省略可能なハンドラーを登録します。

## <a name="related-topics"></a>関連トピック


[*MiniportWdiCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-miniport_wdi_cancel_idle_notification)

[*MiniportWdiIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-miniport_wdi_idle_notification)

 

 






