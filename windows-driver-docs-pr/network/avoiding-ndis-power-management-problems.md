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
ms.openlocfilehash: fbe1e28f0b61cf833cae2e14fdc48519fab449cf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367695"
---
# <a name="avoiding-ndis-power-management-problems"></a>NDIS 電源管理の問題の回避





次の規則を使用すると、ネットワーク アダプターに電源管理の問題を回避できます。

-   ネットワーク アダプターでは、バス ドライバーに電源管理機能を常に報告する必要があります。

-   有効またはレジストリ設定に基づいてネットワーク アダプターの電源管理を無効にしないでください。 NDIS は、ネットワーク アダプターのミニポート ドライバーが初期化される前に、バス ドライバーからネットワーク アダプターについて、電源管理情報を取得します。 場合は、バス ドライバーから取得した情報は、ネットワーク アダプターの電源はないことを示します管理機能を持つ、NDIS、ネットワーク アダプターとして扱い、古いネットワーク アダプターを発行しません、 [OID\_PNP\_機能](https://msdn.microsoft.com/library/windows/hardware/ff569774)ネットワーク アダプターのミニポート ドライバーに要求します。

-   ユーザー インターフェイスでカスタムの電源管理コントロールを提供しようとしないでください。

 

 





