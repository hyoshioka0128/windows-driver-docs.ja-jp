---
title: WDI および WLAN セレクティブ サスペンド機能
description: このセクションは、USB セレクティブ サスペンド WDI ドライバーのサポートを有効にする方法を説明します
ms.assetid: 4FCF726B-4CCF-4F0F-9088-2EABA0DA7D3C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c73a3624c765a303ee0128d3904e7f037df8061
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384343"
---
# <a name="wdi-and-wlan-selective-suspend-capability"></a>WDI および WLAN セレクティブ サスペンド機能


USB のセレクティブ サスペンドのサポートを有効にするには、LE は、機能をレポートする必要があります。 NDIS は、この機能のキーワードを定義します。 詳細については、次を参照してください。 [NDIS セレクティブ サスペンドの標準化された INF キーワード](standardized-inf-keywords-for-ndis-selective-suspend.md)します。

-   \*SelectiveSuspend: {有効にする、無効にする}

-   \*SSIdleTimeout: アイドル状態のタイムアウト (秒)

WDI は、次のソースに基づくサポートを有効します。

-   デバイスの INF:これは、上記のキーワードからデバイスのセットアップでは、次の項目に書き込まれます。
-   レジストリ設定:これは、INF またはデバイス マネージャーでデバイスの高度なプロパティ シートから設定されます。
-   電源管理機能からの戻り値で[OID\_WDI\_取得\_アダプター\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-get-adapter-capabilities)します。
-   内のハンドラーをアイドル[ **NDIS\_ミニポート\_ドライバー\_WDI\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_ndis_miniport_driver_wdi_characteristics)します。
    -   [*MiniportWdiIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-miniport_wdi_idle_notification)

    -   [*MiniportWdiCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-miniport_wdi_cancel_idle_notification)

WDI ドライバーは、LE の 2 つのコールバック関数を公開します。

-   [**IdleNotificationComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-ndis_wdi_idle_notification_complete)

-   [**IdleNotificationConfirm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-ndis_wdi_idle_notification_confirm)

 

 





