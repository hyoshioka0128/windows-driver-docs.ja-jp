---
title: ウェイクアップ イベントの有効化
description: ウェイクアップ イベントの有効化
ms.assetid: 48ed0f41-efa0-4040-8589-8d477c5ddd0e
keywords:
- ウェイク アップ機能 WDK ネットワー キング、ウェイク アップのイベントを有効にします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26ce831906fac95a70a85e24273609bbfce8c565
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372501"
---
# <a name="enabling-wake-up-events"></a>ウェイクアップ イベントの有効化





プロトコル ドライバーに送信できる、 [OID\_PNP\_を有効にする\_WAKE\_を](https://msdn.microsoft.com/library/windows/hardware/ff569775)1 つまたは複数のネットワーク アダプターのウェイク アップ機能を有効にする要求。 NDIS はすぐにこれらのウェイク アップ機能を有効にします。 代わりに、NDIS の追跡、ウェイク アップ機能プロトコル ドライバーによって、スリープ状態に、ミニポート ドライバーの遷移が OID を送信する直前に有効になっている\_PNP\_を有効にする\_WAKE\_まで、ミニポート ドライバーが適切なウェイク アップ イベントを有効にします。 後、ミニポート ドライバーは、ネットワーク アダプターを初期化します。 または、ミニポート ドライバーがネットワーク アダプターに設定されているメソッドのスリープを無効にする必要があります低電力状態から再開するとき。

ミニポート ドライバーの遷移を低電力状態にする前に (NDIS OID、ミニポート ドライバーに送信する前に、\_PNP\_設定\_POWER 要求)、NDIS 送信ミニポート ドライバー OID\_PNP\_有効にする\_WAKE\_ネットワーク アダプターのウェイク アップ機能を有効にする要求を構成します。

 

 





