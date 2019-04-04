---
title: XPSDrv ドライバー要件
description: XPSDrv ドライバー要件
ms.assetid: 382b53eb-a69a-452a-8403-876640a9129e
keywords:
- バージョン 3 XPS ドライバー WDK XPSDrv、要件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22c3efb47330018a2d1a4c37f27764cd215af6f8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581660"
---
# <a name="xpsdrv-driver-requirements"></a>XPSDrv ドライバー要件


ボックスで、 [Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)、XPSDrv 構成のモジュールは、次の要件を満たす必要があります。

-   XPSDrv プリンター ドライバーでは、バージョン 3 の印刷ドライバーの構成モジュールを実装する必要があります。

-   構成のモジュールには、すべての PrintTicket と PrintCapabilities 機能をサポートする必要があります。 Unidrv と Pscript5 プリンター ドライバーの Windows Vista のバージョンでは、自動的にこのサポートを提供します。 モノリシック、GDI ベースのバージョン 3 のプリンター ドライバーをこのサポートを追加する方法の詳細については、[モノリシック印刷ドライバーに印刷チケット サポートを追加する](adding-print-ticket-support-to-monolithic-print-drivers.md)を参照してください。

モジュールの構成要件の完全な一覧で、[Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)を参照してください。

 

 




