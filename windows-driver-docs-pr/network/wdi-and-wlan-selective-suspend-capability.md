---
title: WDI および WLAN セレクティブ サスペンド機能
description: このセクションでは、WDI ドライバーの USB セレクティブサスペンドサポートを有効にする方法について説明します。
ms.assetid: 4FCF726B-4CCF-4F0F-9088-2EABA0DA7D3C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 516723b367dbc1e311439fe191e970262fa4dde6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842933"
---
# <a name="wdi-and-wlan-selective-suspend-capability"></a>WDI および WLAN セレクティブ サスペンド機能


USB のセレクティブサスペンドのサポートを有効にするには、LE が機能を報告する必要があります。 NDIS は、この機能のキーワードを定義します。 詳細については、「 [NDIS 選択的中断の標準化](standardized-inf-keywords-for-ndis-selective-suspend.md)された INF キーワード」を参照してください。

-   \*SelectiveSuspend: {Enable, Disable}

-   \*SSIdleTimeout: アイドルタイムアウト (秒)

WDI は、次のソースに基づいたサポートを有効にします。

-   デバイス INF: これは、上記のキーワードからデバイス設定の次の項目に書き込まれます。
-   レジストリ設定: デバイスマネージャーのデバイスの INF または詳細プロパティシートから設定します。
-   OID\_WDI から返される電源管理機能は、 [\_アダプターの\_機能を取得\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-get-adapter-capabilities)ます。
-   NDIS のアイドルハンドラー [ **\_ミニポート\_ドライバー\_WDI\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_miniport_driver_wdi_characteristics)。
    -   [*MiniportWdiIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_idle_notification)

    -   [*MiniportWdiCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_cancel_idle_notification)

WDI ドライバーは、LE の2つのコールバック関数を公開します。

-   [**IdleNotificationComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_idle_notification_complete)

-   [**IdleNotificationConfirm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_idle_notification_confirm)

 

 





