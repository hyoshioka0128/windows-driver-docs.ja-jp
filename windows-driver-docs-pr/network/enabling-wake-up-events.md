---
title: ウェイクアップ イベントの有効化
description: ウェイクアップ イベントの有効化
ms.assetid: 48ed0f41-efa0-4040-8589-8d477c5ddd0e
keywords:
- ウェイク アップ機能 WDK ネットワー キング、ウェイク アップのイベントを有効にします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44d6d12847f8dc7c463329715170cdaea89883d4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354589"
---
# <a name="enabling-wake-up-events"></a>ウェイクアップ イベントの有効化





プロトコル ドライバーに送信できる、 [OID\_PNP\_を有効にする\_WAKE\_を](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-enable-wake-up)1 つまたは複数のネットワーク アダプターのウェイク アップ機能を有効にする要求。 NDIS はすぐにこれらのウェイク アップ機能を有効にします。 代わりに、NDIS の追跡、ウェイク アップ機能プロトコル ドライバーによって、スリープ状態に、ミニポート ドライバーの遷移が OID を送信する直前に有効になっている\_PNP\_を有効にする\_WAKE\_まで、ミニポート ドライバーが適切なウェイク アップ イベントを有効にします。 後、ミニポート ドライバーは、ネットワーク アダプターを初期化します。 または、ミニポート ドライバーがネットワーク アダプターに設定されているメソッドのスリープを無効にする必要があります低電力状態から再開するとき。

ミニポート ドライバーの遷移を低電力状態にする前に (NDIS OID、ミニポート ドライバーに送信する前に、\_PNP\_設定\_POWER 要求)、NDIS 送信ミニポート ドライバー OID\_PNP\_有効にする\_WAKE\_ネットワーク アダプターのウェイク アップ機能を有効にする要求を構成します。

 

 





