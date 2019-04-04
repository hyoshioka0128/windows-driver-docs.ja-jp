---
title: スリープ状態に遷移します。
description: スリープ状態に遷移します。
ms.assetid: cea326dd-7235-41a3-ad37-19549533a8dd
keywords:
- ネットワーク インターフェイス カード WDK ネットワーク、電源の状態遷移
- Nic の WDK ネットワーク、電源の状態遷移
- スリープ状態の WDK ネットワーク
- 電源管理 WDK NDIS ミニポート、電源の状態遷移
- デバイスの電源状態が WDK ネットワーク
- WDK ネットワークの状態を電源します。
- WDK のネットワークの状態遷移の電源
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d907d88524f9e1296ab817e7f8eae494e3175acd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550779"
---
# <a name="transitioning-to-a-sleeping-state"></a>スリープ状態に遷移します。





NDIS ミニポート ドライバーは、ウェイク アップのイベントをサポートする、送信ドライバー、 [OID\_PNP\_を有効にする\_WAKE\_を](https://msdn.microsoft.com/library/windows/hardware/ff569775)要求を送信する前に、 [OID\_PNP\_設定\_POWER](https://msdn.microsoft.com/library/windows/hardware/ff569780)要求。 詳細については、[ウェイク アップのイベントを有効にする](enabling-wake-up-events.md)を参照してください。 ミニポート ドライバーに OID が失敗する必要がありますいない\_PNP\_設定\_POWER 要求。

NDIS を返す前に\_状態\_OID への応答の成功\_PNP\_設定\_POWER 要求、ミニポート ドライバーにする必要があります。

-   スリープ状態のネットワーク アダプターを準備するために必要なデバイスに依存する操作を実行します。

-   すべてのパケット フィルター、マルチキャスト アドレス、現在の MAC アドレス、ウェイク アップ パターン、およびネットワーク アダプターをスリープ状態に保持できません。 他のハードウェア コンテキストを保存します。

-   割り込みと DMA エンジンのネットワーク アダプターの無効にします。 ネットワーク アダプターは、バス ドライバーによって D3 の状態に設定された後、ミニポート ドライバーは、ネットワーク アダプターのハードウェアにアクセスできません。

 

 





