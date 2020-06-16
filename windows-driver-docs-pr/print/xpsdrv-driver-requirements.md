---
title: XPSDrv ドライバー要件
description: XPSDrv ドライバー要件
ms.assetid: 382b53eb-a69a-452a-8403-876640a9129e
keywords:
- バージョン 3 XPS ドライバーの WDK XPSDrv、要件
ms.date: 06/15/2020
ms.localizationpriority: medium
ms.openlocfilehash: 266e48a77fbe1542094a4b50ebd75ea44984f2ae
ms.sourcegitcommit: 77c63789350cfc1dc740baaafdef64803d86217f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/16/2020
ms.locfileid: "84793740"
---
# <a name="xpsdrv-driver-requirements"></a>XPSDrv ドライバー要件

インボックスおよび[Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)の場合、XPSDrv 構成モジュールは次の要件を満たしている必要があります。

- XPSDrv プリンタードライバーは、バージョン3の印刷ドライバー構成モジュールを実装する必要があります。

- 構成モジュールは、すべての PrintTicket および PrintCapabilities 機能をサポートする必要があります。 Windows Vista バージョンの Unidrv および Pscript5 プリンタードライバーは、このサポートを自動的に提供します。 このサポートをモノリシックの GDI ベースバージョン3プリンタードライバーに追加する方法の詳細については、「[モノリシック印刷ドライバーへの印刷チケットサポートの追加](adding-print-ticket-support-to-monolithic-print-drivers.md)」を参照してください。

構成モジュールの要件の完全な一覧については、「 [Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)」を参照してください。
