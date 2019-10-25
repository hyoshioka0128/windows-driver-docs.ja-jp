---
title: WDI セレクティブ サスペンド機能登録
description: 次に、USB のセレクティブサスペンド機能を登録するためのフロー図を示します。
ms.assetid: E4AE424F-2017-4111-B4C7-DF0BA6A40A15
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85f29f6c50540707f1fe179c7ee51bc0981fcd9a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842902"
---
# <a name="wdi-selective-suspend-capability-registration"></a>WDI セレクティブ サスペンド機能登録


次に、USB のセレクティブサスペンド機能を登録するためのフロー図を示します。

![wdi 選択的中断機能の登録](images/wdi-register-usb-selective-suspend-flow.png)

AdapterCap (PM (ss))、\*SelectiveSuspend、 **LeIdleNotificationHandler**、 **LeCancelIdleNotificationHandler**は true であるか、または WDI が有効である必要があります。これは、WLAN が選択的中断をサポートしていることを登録するためです。

WDI によって選択的中断がサポートされていると判断された場合、WDI はオプションのハンドラーも NDIS に登録します。

## <a name="related-topics"></a>関連トピック


[*MiniportWdiCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_cancel_idle_notification)

[*MiniportWdiIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_idle_notification)

 

 






