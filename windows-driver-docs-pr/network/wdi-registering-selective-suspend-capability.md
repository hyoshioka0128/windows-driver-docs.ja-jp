---
title: WDI セレクティブ サスペンド機能の登録
description: USB のセレクティブ サスペンドの機能を登録するためのフロー ダイアグラムを次に示します。
ms.assetid: E4AE424F-2017-4111-B4C7-DF0BA6A40A15
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a94fb85f459820e5b0f250e4be2ba443e4deae7c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558730"
---
# <a name="wdi-selective-suspend-capability-registration"></a>WDI セレクティブ サスペンド機能の登録


USB のセレクティブ サスペンドの機能を登録するためのフロー ダイアグラムを次に示します。

![選択的 wdi 中断機能の登録](images/wdi-register-usb-selective-suspend-flow.png)

AdapterCap(PM(ss))、 \*SelectiveSuspend、 **LeIdleNotificationHandler**、および**LeCancelIdleNotificationHandler** true または WDI WLAN 選択をサポートしている登録を有効にする必要があります中断します。

WDI はセレクティブ サスペンドをサポートすることが決定したら、WDI も NDIS に省略可能なハンドラーを登録します。

## <a name="related-topics"></a>関連トピック


[*MiniportWdiCancelIdleNotification*](https://msdn.microsoft.com/library/windows/hardware/mt297560)

[*MiniportWdiIdleNotification*](https://msdn.microsoft.com/library/windows/hardware/mt297563)

 

 






