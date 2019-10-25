---
title: ローカル DCBX Willing 状態の管理
description: ローカル DCBX Willing 状態の管理
ms.assetid: B37CA18B-FCCD-414D-95AB-0C54B9F1F421
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f03db930f80ecc48d5c4ab732619751f88c6f39
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844310"
---
# <a name="managing-the-local-dcbx-willing-state"></a>ローカル DCBX Willing 状態の管理


IEEE 802.1 Qaz draft 標準では、データセンターブリッジング (DCBX) プロトコルが定義されています。 このプロトコルを使用すると、ネットワークアダプター (ローカルピア) と直接接続されているリモートピア間で DCB 構成パラメーターを交換できます。 これにより、これらのピアは、サービスの品質 (QoS) パラメーターを調整および調整して、接続を介したデータ転送を最適化することができます。

ローカルおよびリモートの QoS パラメーター設定に基づき、ミニポートドライバーは競合を解決し、一連の動作 QoS パラメーターを派生します。 ネットワークアダプターは、これらの操作パラメーターを使用して、リモートピアにパケットを優先的に送信します。 ドライバーが動作している NDIS QoS パラメーター設定を解決する方法の詳細については、「[運用 Ndis Qos パラメーターの解決](resolving-operational-ndis-qos-parameters.md)」を参照してください。

DCBX は、DCB (TLV) の設定で構成されます。この設定は、リンクレイヤー検出プロトコル (LLDP) パケットを介して行われます。 次の種類の QoS パラメーターに対して、別の TLV が定義されています。

-   [拡張転送の選択 (送信)](enhanced-transmission-selection--ets--algorithm.md)

-   [優先順位ベースのフロー制御 (PFC)](priority-based-flow-control--pfc.md)

TLVs と PFC は、*受け入れ*ビットとして認識されるビットを定義します。 ネットワークアダプターが TLV の設定をリモートピアに送信し、受け入れビットを1に設定した場合は、アダプターがリモートピアからの QoS パラメーターを受け入れることを示します。

これらの TLVs ビットを個別に設定できるかどうかは、ミニポートドライバーによって管理されるローカルの DCBX の状態によって決まります。 ミニポートドライバーは、ローカルの DCBX の状態を管理するために、次のガイドラインに従う必要があります。

-   ローカルの DCBX が使用できない状態になっている場合は、DCBX TLVs でローカルの受け入れビットを0に設定する必要があります。 この場合、operational QoS パラメーターは常にローカルの QoS パラメーターから解決されます。 これらのパラメーターの詳細については、「[ローカル NDIS QoS パラメーターの設定](setting-local-ndis-qos-parameters.md)」を参照してください。

-   ローカルの DCBX が有効になっている場合は、DCBX TLVs でローカルの受け入れビットを1に設定する必要があります。 この場合、operational QoS パラメーターをリモート QoS パラメーターから解決する必要があります。 これらのパラメーターの詳細については、「[リモート NDIS QoS パラメーターの受信](receiving-remote-ndis-qos-parameters.md)」を参照してください。

    **注**  ローカルの dcbx が有効になっている場合、ミニポートドライバーは、独立系ハードウェアベンダー (IHV) によって定義されている独自の qos 設定に基づいて、その動作 qos パラメーターを解決することもできます。 ドライバーは、ピアによってリモートで構成されていない、またはオペレーティングシステムによってローカルに構成されていない QoS パラメーターに対してのみ、この操作を実行できます。

     

ミニポートドライバーは、次の方法でローカルの DCBX の状態を管理します。

-   ミニポートドライバーは、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数の呼び出しによって初期化されるときに、IHV によって定義された独自の QoS 設定に基づいて、ローカルの dcbx の状態を有効にする必要があります。

-   DCB コンポーネント (Msdcb) は、Oid のオブジェクト識別子 (OID) メソッドの要求を発行し、ネットワークアダプターでローカルの QoS パラメーターを構成するために[qos\_パラメーターを\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-parameters)します。 この OID 要求に対する[**ndis\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、 [**ndis\_QOS\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体へのポインターが含まれています。

    この構造体の**Flags**メンバーで、 **NDIS\_QOS\_パラメーター\_** 許可フラグが設定されている場合、ミニポートドライバーによって、dcbx が有効になります。 このビットが設定されていない場合、ミニポートドライバーは DCBX の状態を無効にします。

LLDP の詳細については、「IEEE 802.1 AB-2005 標準」を参照してください。

ローカルの DCBX 受け入れビットと TLVs の詳細については、「IEEE 802.1 Qaz draft standard」を参照してください。

**注**  Windows Server 2012 以降では、PowerShell コマンドレットを使用して、DCB コンポーネントを構成し、 **NDIS\_qos\_パラメーター\_** 、OID\_qos を発行するときにフラグを設定または解除することができ[\_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-parameters)要求。 これにより、ミニポートドライバーは、ローカルの DCBX の状態をそれぞれ有効または無効にします。

 

 

 





