---
title: 割り込み節度
description: 割り込み節度
ms.assetid: 291f9606-6379-4b78-b388-ba663f84b431
keywords:
- 割り込みモデレーションの WDK ネットワーク
- WDK ネットワークを中断し、
- OID_GEN_INTERRUPT_MODERATION
- NDIS_INTERRUPT_MODERATION_PARAMETERS
- WDK ネットワークの割り込み、モデレーション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc017c850a98171a37098b82358d070a0f8c865e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844175"
---
# <a name="interrupt-moderation"></a>割り込み節度





割り込みの数を減らすために、多くの Nic は*割り込みモデレーション*を使用します。 割り込みモデレーションを使用すると、NIC ハードウェアはパケットを受信した直後に割り込みを生成しません。 代わりに、割り込みを生成する前に、より多くのパケットが到着するまで、またはタイムアウトになるまで、ハードウェアは待機します。 ハードウェアベンダーは、パケットの最大数、タイムアウト期間、またはその他の割り込みモデレーションアルゴリズムを指定します。

パケットの測定ラウンドトリップ時間は、2つのエンドポイント間のネットワーク帯域幅を決定するために最もよく使用される手法の1つです。 ただし、割り込みのモデレーションが有効になっている場合、パケットを受信しても即時割り込みが生成されないため、特定のパケットに対して認識されるラウンドトリップ時間が平均時間よりも長くなります。 パケットのラウンドトリップ時間を正確に測定するために、NDIS は必要に応じて割り込みモデレーションを無効にし、有効にする機能を提供します。

すべての NDIS 6.0 およびそれ以降のミニポートドライバーは、 [oid\_GEN\_割り込み\_モデレーション](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-interrupt-moderation)oid をサポートする必要があります。 ミニポートドライバーで割り込みモデレーションがサポートされていない場合、ドライバーは 、 [**NDIS\_interrupt\_モデレーション\_パラメーターの InterruptModeration メンバーに NdisInterruptModerationNotSupported を指定する必要があります。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_interrupt_moderation_parameters)構造体。

NDIS 6.0 以降のミニポートドライバーは、 [oid\_GEN\_割り込み\_モデレーション](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-interrupt-moderation)oid セットとクエリ要求の両方をサポートする必要があります。 設定要求は、ミニポートドライバーに対して、割り込みモデレーションを有効または無効にするように指示します。クエリ要求は、割り込みモデレーションの現在の状態を報告します。

割り込みモデレーションをサポートするミニポートドライバーは、レジストリの**InterruptModeration** standard キーワードで無効にされていない限り、既定でこの機能を有効にする必要があります。 標準のキーワードの詳細については、「[ネットワークデバイスの標準化](standardized-inf-keywords-for-network-devices.md)された INF キーワード」を参照してください。

 

 





