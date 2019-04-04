---
title: いる CoNDIS WAN ドライバーの WAN 固有の機能
description: いる CoNDIS WAN ドライバーの WAN 固有の機能
ms.assetid: c4e8e0ae-7dd5-4c4e-900a-b1f7e5eecb16
keywords:
- いる CoNDIS WAN ドライバー WDK ネットワークの非-WAN いる CoNDIS ドライバーとの比較
- 非-WAN いる CoNDIS ドライバー WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa3de90c84344d699449cf7a8689001c260e9e7c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538790"
---
# <a name="wan-specific-capabilities-of-condis-wan-drivers"></a>いる CoNDIS WAN ドライバーの WAN 固有の機能





いる CoNDIS WAN ドライバーは、次のように、非-WAN いる CoNDIS ドライバーと異なります。

-   TAPI サービスをサポートしている CoNDIS WAN のドライバーを使用して、CO\_アドレス\_ファミリ\_TAPI\_プロキシ アドレス ファミリ。

-   いる CoNDIS WAN ドライバーでは、WAN に固有の Oid をサポートします。[OID\_WAN\_永続的な\_アドレス](https://msdn.microsoft.com/library/windows/hardware/ff561220)、 [OID\_WAN\_現在\_アドレス](https://msdn.microsoft.com/library/windows/hardware/ff561200)、および[OID\_WAN\_MEDIUM\_サブタイプ](https://msdn.microsoft.com/library/windows/hardware/ff561216)します。

-   セットおよびクエリの特性を操作するには、いる CoNDIS WAN Oid のセットをサポートしている CoNDIS WAN ミニポート ドライバー。 いる CoNDIS WAN Oid の詳細については、[いる CoNDIS WAN オブジェクト](https://msdn.microsoft.com/library/windows/hardware/ff545146)を参照してください。

-   TAPI サービスを提供している CoNDIS WAN ミニポート ドライバーでは、セットおよびクエリの特性を操作している CoNDIS TAPI Oid のセットをサポートします。 いる CoNDIS TAPI Oid の詳細については、[Connection-Oriented NDIS の TAPI 拡張](https://msdn.microsoft.com/library/windows/hardware/ff570924)を参照してください。

-   いる CoNDIS WAN ミニポート ドライバーでは、リンクの状態の変化を示す WAN に固有の状態インジケーターのセットをサポートします。 いる CoNDIS WAN ミニポート ドライバーの状態インジケーターの詳細については、[を示すいる CoNDIS WAN ミニポート ドライバー ステータス](indicating-condis-wan-miniport-driver-status.md)を参照してください。

-   いる CoNDIS WAN ミニポート ドライバーでは、WAN に固有の一連の統計を保持します。 [OID\_WAN\_CO\_取得\_STATS\_情報](https://msdn.microsoft.com/library/windows/hardware/ff569820)OID は、統計情報を返す、ミニポート ドライバーを要求します。

-   いる CoNDIS WAN ミニポート ドライバーがすべてのパケットにループに戻ってを試行しないでください。NDISWAN は、ループバックのサポートを提供します。

 

 





