---
title: WDI および WLAN セレクティブ サスペンドの機能
description: このセクションは、USB セレクティブ サスペンド WDI ドライバーのサポートを有効にする方法を説明します
ms.assetid: 4FCF726B-4CCF-4F0F-9088-2EABA0DA7D3C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2c250d0be241b1f12e69199cf92cf082168bd48
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530990"
---
# <a name="wdi-and-wlan-selective-suspend-capability"></a>WDI および WLAN セレクティブ サスペンドの機能


USB のセレクティブ サスペンドのサポートを有効にするには、LE は、機能をレポートする必要があります。 NDIS は、この機能のキーワードを定義します。 詳細については、[NDIS セレクティブ サスペンドの標準化された INF キーワード](standardized-inf-keywords-for-ndis-selective-suspend.md)を参照してください。

-   \*SelectiveSuspend: {有効にする、無効にする}

-   \*SSIdleTimeout: アイドル状態のタイムアウト (秒)

WDI は、次のソースに基づくサポートを有効します。

-   デバイスの INF:これは、上記のキーワードからデバイスのセットアップでは、次の項目に書き込まれます。
-   レジストリ設定:これは、INF またはデバイス マネージャーでデバイスの高度なプロパティ シートから設定されます。
-   電源管理機能からの戻り値で[OID\_WDI\_取得\_アダプター\_機能](https://msdn.microsoft.com/library/windows/hardware/dn925838)します。
-   内のハンドラーをアイドル[ **NDIS\_ミニポート\_ドライバー\_WDI\_特性**](https://msdn.microsoft.com/library/windows/hardware/mt297617)します。
    -   [*MiniportWdiIdleNotification*](https://msdn.microsoft.com/library/windows/hardware/mt297563)

    -   [*MiniportWdiCancelIdleNotification*](https://msdn.microsoft.com/library/windows/hardware/mt297560)

WDI ドライバーは、LE の 2 つのコールバック関数を公開します。

-   [**IdleNotificationComplete**](https://msdn.microsoft.com/library/windows/hardware/mt297600)

-   [**IdleNotificationConfirm**](https://msdn.microsoft.com/library/windows/hardware/mt297601)

 

 





