---
title: ローカル DCBX Willing 状態の管理
description: ローカル DCBX Willing 状態の管理
ms.assetid: B37CA18B-FCCD-414D-95AB-0C54B9F1F421
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25805d3cac9ba70ceb59eac15e0151f371b8bfc1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379208"
---
# <a name="managing-the-local-dcbx-willing-state"></a>ローカル DCBX Willing 状態の管理


IEEE 802.1 qaz ドラフト標準には、Data Center Bridging Exchange (DCBX) プロトコルが定義されています。 このプロトコルは、ネットワーク アダプター (ローカル ピア) と直接接続されているリモート ピア間で交換される DCB 構成パラメーターです。 これにより、これらのピアに適応し、接続経由でデータ転送を最適化するためにサービスの品質 (QoS) パラメーターを調整できます。

ローカルおよびリモートの QoS パラメーターの設定に基づき、ミニポート ドライバーは、競合を解決し、一連の運用上の QoS パラメーターを派生します。 ネットワーク アダプターでは、リモート ピアにパケットの優先順位の送信のこれらのオペレーションのパラメーターを使用します。 ドライバーがその運用上の NDIS QoS パラメーター設定を解決する方法の詳細については、次を参照してください。[運用上の NDIS QoS パラメーターを解決する](resolving-operational-ndis-qos-parameters.md)します。

リンク層探索プロトコル (LLDP) パケットで実行される DCB 型の値の長さ (TLV) 設定 DCBX で構成されます。 個別の TLV は、次の種類の QoS パラメーターに対して定義されます。

-   [強化された転送の選択 (ETS)](enhanced-transmission-selection--ets--algorithm.md)

-   [優先順位に基づくフロー制御 (PFC)](priority-based-flow-control--pfc.md)

ETS と PFC TLVs 定義と少し呼ばれる、*許容*ビット。 ネットワーク アダプターでは、いずれかに設定可能ビットを使用して、その TLV 設定をリモート ピアに送信する場合は、アダプターはリモート ピアから QoS パラメーターを許容できることを示します。

これら TLVs で許容できる個別のビットを設定する機能は、ローカルの DCBX しようとして、ミニポート ドライバーで管理されている状態に依存します。 ミニポート ドライバーは、ローカルの DCBX しようとして状態を管理するための次のガイドラインに従う必要があります。

-   ローカルの DCBX しようとして状態が無効になっている場合、DCBX TLVs で 0 にしようとしてローカルのビットを設定する必要があります。 この場合は、運用上の QoS パラメーターは、ローカルの QoS パラメーターから常に解決されます。 これらのパラメーターの詳細については、次を参照してください。 [NDIS QoS パラメーターをローカル設定](setting-local-ndis-qos-parameters.md)します。

-   しようとして状態ローカル DCBX が有効になっている場合、DCBX TLVs でいずれかにしようとしてローカルのビットを設定する必要があります。 この場合は、QoS パラメーターをリモートから運用上の QoS パラメーターを解決する必要があります。 これらのパラメーターの詳細については、次を参照してください。[リモートの NDIS QoS パラメーターを受け取る](receiving-remote-ndis-qos-parameters.md)します。

    **注**  ミニポート ドライバーが、独立系ハードウェア ベンダー (IHV) で定義されている独自の QoS 設定に基づいて、運用の QoS パラメーターを解決できるもローカルの DCBX しようとして状態が有効になっている場合。 QoS パラメーターまたはローカル ピアが、オペレーティング システムによってリモートで構成されていないこのドライバーにはのみことができます。

     

ミニポート ドライバーでは、ローカルの DCBX しようとして次のように状態を管理します。

-   呼び出すことによって、ミニポート ドライバーが初期化される場合、 [ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数、しようとして状態を IHV で定義されている独自の QoS 設定に基づいてローカル DCBX を有効にする必要があります.

-   DCB コンポーネント (Msdcb.sys) のオブジェクト識別子 (OID) メソッド要求の発行[OID\_QOS\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-parameters)ネットワーク アダプターでローカルの QoS パラメーターを構成します。 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)この OID 要求、へのポインターが含まれている構造体[ **NDIS\_QOS\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体。

    場合、 **NDIS\_QOS\_パラメーター\_WILLING**フラグに設定されて、**フラグ**この構造体のメンバーは、有効にしようとして状態 DCBX ミニポート ドライバー。 このビットが設定されていない場合、ミニポート ドライバーには、状態のような場面 DCBX が無効になります。

LLDP の詳細については、IEEE 802.1AB を参照してください-2005 standard。

ローカルの DCBX 許容 bits と TLVs の詳細については、IEEE 802.1 qaz を参照してくださいドラフト標準。

**注**  以降 Windows Server 2012 では、DCB コンポーネントで構成できますオンまたはオフにするには、PowerShell コマンドレット、 **NDIS\_QOS\_パラメーター\_WILLING**フラグを発行するとき、 [OID\_QOS\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-parameters)要求。 これにより、それぞれ有効または無効にしようとして状態ローカル DCBX ミニポート ドライバーです。

 

 

 





