---
title: NDIS のデータ センター ブリッジングの QoS 要件
description: NDIS のデータ センター ブリッジングの QoS 要件
ms.assetid: 09BEFF6C-6887-42BA-A44B-5BFE65DBD69E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: beceb7a133f96ae12a28458418786706ea0ed242
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369175"
---
# <a name="ndis-qos-requirements-for-data-center-bridging"></a>NDIS のデータ センター ブリッジングの QoS 要件


NDIS サービスの品質 (QoS) の IEEE 802.1 データ センター ブリッジング (DCB) をサポートするには、ミニポート ドライバーとネットワーク アダプターを次のサポートする必要があります。

-   ミニポート ドライバーとネットワーク アダプターは、優先度に基づくフロー制御 (PFC) IEEE 802.1 qbb で指定されたをサポートする必要がありますドラフト標準。

-   ミニポート ドライバーとネットワーク アダプターには、IEEE 802.1 qaz で指定された Enhanced Transmission Selection (ETS) アルゴリズムをサポートする必要がありますドラフト標準。

-   ミニポート ドライバーとネットワーク アダプター、3 つの NDIS QoS トラフィック クラスの最小値をサポートし、ETS ベースのトラフィックの 2 つのクラスの最小値をサポートする必要があります。 これらの 2 つの少なくとも 1 つの ETS ベースのトラフィック クラスは、PFC をサポートする必要があります。

    トラフィック クラスの詳細については、次を参照してください。 [NDIS QoS トラフィック クラス](ndis-qos-traffic-classes.md)します。

-   ミニポート ドライバーとネットワーク アダプターは、IEEE 802.1 q で指定された転送の選択範囲の優先アルゴリズムをサポートする必要があります-2005 standard。

NDIS QoS、ミニポート ドライバーとネットワーク アダプターは、IEEE で指定された Data Center Bridging Exchange (DCBX) プロトコルをサポート必要に応じて 802.1 qaz ドラフト標準にします。 DCBX をサポートするために、ミニポート ドライバーとアダプターする必要がありますもプロトコルをサポートして、リンク層探索プロトコル (LLDP) IEEE 802.1AB で指定されている-2005 standard。

さらに、ミニポート ドライバー自体では、NDIS QoS の次をサポートする必要があります。

-   NDIS 6.30 または以降のバージョンの NDIS ミニポート ドライバーをサポートする必要があります。

-   ミニポート ドライバーでのオブジェクト識別子 (OID) メソッドの要求をサポートする必要があります[OID\_QOS\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-parameters)の NDIS QoS パラメーターを設定します。 詳細については、次を参照してください。 [NDIS QoS パラメーターをローカル設定](setting-local-ndis-qos-parameters.md)します。

    **注**  NDIS ミニポート ドライバーは例外ですの NDIS QoS OID 要求のほとんどを処理する[OID\_QOS\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-parameters)します。

     

-   ミニポート ドライバーでは、リモート ピアから送信された DCBX フレーム経由で受信した NDIS QoS パラメーター設定の競合を解決できる必要があります。 ドライバーは、優先順位付きパケット転送のネットワーク アダプターを使用する運用上の NDIS QoS パラメーターを確認して、ローカルおよびリモートの NDIS QoS パラメーター間の競合を解決します。 このプロセスの詳細については、次を参照してください。[運用上の NDIS QoS パラメーターを解決する](resolving-operational-ndis-qos-parameters.md)します。

-   ミニポート ドライバーでは、その運用上の NDIS QoS パラメーターを変更するときに、NDIS 状態インジケーターを発行できる必要があります。 このプロセスの詳細については、次を参照してください。[運用上の NDIS QoS パラメーターを示す変更](indicating-changes-to-the-operational-ndis-qos-parameters.md)します。

-   ミニポート ドライバーでは、リモート ピアの NDIS QoS パラメーターで変更を検出した場合に、NDIS 状態インジケーターを発行できる必要があります。 このプロセスの詳細については、次を参照してください。[リモートの NDIS QoS パラメーターを示す変更](indicating-changes-to-the-remote-ndis-qos-parameters.md)します。

 

 





