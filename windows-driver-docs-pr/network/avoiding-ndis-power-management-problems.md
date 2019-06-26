---
title: NDIS 電源管理の問題の回避
description: NDIS 電源管理の問題の回避
ms.assetid: 58bd91d5-68bd-471d-a961-6e0676d4a352
keywords:
- WDK の NDIS ミニポート、問題の電源管理
- ネットワーク インターフェイス カード WDK ネットワーク、電源の問題
- Nic の WDK ネットワーク、電源の問題
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c218f5d28457c336a5ca24a5eaeecc8f7513fb7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384407"
---
# <a name="avoiding-ndis-power-management-problems"></a>NDIS 電源管理の問題の回避





次の規則を使用すると、ネットワーク アダプターに電源管理の問題を回避できます。

-   ネットワーク アダプターでは、バス ドライバーに電源管理機能を常に報告する必要があります。

-   有効またはレジストリ設定に基づいてネットワーク アダプターの電源管理を無効にしないでください。 NDIS は、ネットワーク アダプターのミニポート ドライバーが初期化される前に、バス ドライバーからネットワーク アダプターについて、電源管理情報を取得します。 場合は、バス ドライバーから取得した情報は、ネットワーク アダプターの電源はないことを示します管理機能を持つ、NDIS、ネットワーク アダプターとして扱い、古いネットワーク アダプターを発行しません、 [OID\_PNP\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-capabilities)ネットワーク アダプターのミニポート ドライバーに要求します。

-   ユーザー インターフェイスでカスタムの電源管理コントロールを提供しようとしないでください。

 

 





