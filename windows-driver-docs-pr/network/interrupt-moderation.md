---
title: 割り込み節度
description: 割り込み節度
ms.assetid: 291f9606-6379-4b78-b388-ba663f84b431
keywords:
- 割り込み節度 WDK ネットワーク
- ネットワークの数を減らして、WDK を中断します。
- OID_GEN_INTERRUPT_MODERATION
- NDIS_INTERRUPT_MODERATION_PARAMETERS
- 割り込み WDK ネットワー キング、モデレート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93c0de142b47b8e84e9d52483b8bb635a8bbbf45
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573782"
---
# <a name="interrupt-moderation"></a>割り込み節度





複数の Nic を使用して、割り込みの数を減らすためには、*割り込み節度*します。 割り込み節度をで NIC ハードウェアは生成されません、割り込み、パケットを受信した後すぐに。 代わりに、ハードウェアは、詳細パケットの到着、または、割り込みを生成する前に、有効期限のタイムアウトを待機します。 ハードウェア ベンダーには、パケット、タイムアウト間隔、またはその他の割り込み節度アルゴリズムの最大数を指定します。

パケットの測定のラウンドト リップ時間では、2 つのエンドポイント間のネットワーク帯域幅を決定する最もよく使用される手法の 1 つです。 ただし、割り込み節度を有効にすると、パケットの受信、即時割り込みを生成しませんし、そのため、特定のパケットのラウンドト リップ時間の平均時間より大きくなります。 パケットのラウンド トリップ時間を正確に測定を許可するのには、NDIS は無効にして、オンデマンドでの割り込み節度を有効にする機能を提供します。

すべての NDIS 6.0 とそれ以降のミニポート ドライバーをサポートする必要があります、 [OID\_GEN\_INTERRUPT\_モデレート](https://msdn.microsoft.com/library/windows/hardware/ff569590)OID。 かどうか、ミニポート ドライバーは、割り込み節度をサポートしていない、ドライバーを指定する必要があります**NdisInterruptModerationNotSupported**で、 **InterruptModeration**のメンバー、 [ **NDIS\_INTERRUPT\_モデレート\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff565793)構造体。

NDIS 6.0 とそれ以降のミニポート ドライバーをサポートする必要があります、 [OID\_GEN\_INTERRUPT\_モデレート](https://msdn.microsoft.com/library/windows/hardware/ff569590)OID が設定され、要求のクエリを実行します。 セットの要求を有効にまたは割り込み節度を無効にするミニポート ドライバーに指示し、クエリ要求は、割り込み節度の現在の状態を報告します。

サポートの割り込み節度ミニポート ドライバーはこの機能既定でオンにしない限り、 **InterruptModeration**レジストリの標準のキーワードを無効にします。 標準のキーワードの詳細については、[ネットワーク デバイスの標準化された INF キーワード](standardized-inf-keywords-for-network-devices.md)を参照してください。

 

 





