---
title: システムの電源の変更の処理
description: システムの電源の変更の処理
ms.assetid: 80e36a23-8a41-46f0-a7cb-0039c306a695
keywords:
- 電源は、WDK ネットワークを変更します。
- Nic の WDK ネットワーク、電源のソースの変更
- ネットワーク インターフェイス カード WDK ネットワーク、電源のソースの変更
- プラグ アンド プレイ WDK NDIS ミニポート、電源のソースの変更
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84e4a474671dcecb722adfc96fd800e4c4f93dd6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349799"
---
# <a name="handling-a-change-in-the-systems-power-source"></a>システムの電源の変更の処理





システムは、AC 電源、またはその逆に、バッテリ電源から変更できます。

NDIS ミニポート ドライバーを初期化した後、ミニポート ドライバーが呼び出し[ *MiniportDevicePnPEventNotify* ](https://msdn.microsoft.com/library/windows/hardware/ff559369)システムの電源のミニポート ドライバーに通知します。 ミニポート ドライバーは、この情報を使用して、NIC の電力消費量を調整するには たとえば、ワイヤレス LAN (WLAN) デバイス用のミニポート ドライバーは、電力消費の削減、システムがバッテリ電源で実行されている場合や、システムが AC 電源で実行されている場合は、電力消費量を増やします。

 

 





