---
title: ローカル NDIS QoS パラメーターの設定
description: ローカル NDIS QoS パラメーターの設定
ms.assetid: 7AB30829-16A0-46BF-8066-506E01E718A4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b296c8de9238fc3cfe44256176306beefff090d9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841940"
---
# <a name="setting-local-ndis-qos-parameters"></a>ローカル NDIS QoS パラメーターの設定


ローカルの NDIS Quality Service (QoS) パラメーターでは、ミニポートドライバーとそのネットワークアダプターに対してローカルにプロビジョニングされた QoS 設定を指定します。 ミニポートドライバーは、次の方法でローカル NDIS QoS パラメーターを取得します。

-   データセンターブリッジング (DCB) コンポーネント (Msdcb) によって発行された、 [\_QOS\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-parameters)のオブジェクト識別子 (oid) メソッドの要求を介して実行します。 この OID 要求には、ローカル NDIS QoS パラメーターを指定する[**ndis\_QOS\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体が含まれています。

    DCB コンポーネントの詳細については、「[データセンターブリッジングの NDIS QoS アーキテクチャ](ndis-qos-architecture-for-data-center-bridging.md)」を参照してください。

    **注**  Windows Server 2012 以降では、DCB コンポーネントがインストールされ、Microsoft Data Center ブリッジング (DCB) サーバー機能が有効になっています。 既定では、この機能はインストールされません。

     

-   システムレジストリに保存され、ネットワークアダプター用の独立系ハードウェアベンダー (IHV) によって定義されている、独自の設定を使用します。 ミニポートドライバーは、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数が NDIS によって呼び出されたときに、これらの設定を読み取ります。

-   IHV によって開発された管理アプリケーションを通じてミニポートドライバーに発行された独自の設定を使用します。

DCB コンポーネントが oid\_の oid メソッド要求を発行するときに、 [qos\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-parameters)の場合、 **ndis\_qos\_パラメーター\_** 、 **NDIS\_QOS\_のパラメーターを受け入れます。Flags**メンバーは、ミニポートドライバーが、ローカルの NDIS qos パラメーターからの動作 QoS パラメーターをどのように解決するかを指定します。 このフラグに基づいて、ドライバーは次の方法でローカルの QoS パラメーターを解決します。

-   **NDIS\_QOS の\_パラメーター\_** 許可フラグが設定されている場合、ミニポートドライバーはローカル DCB Exchange (dcbx) の状態を有効にする必要があります。 これにより、QoS パラメーターを使用してドライバーをリモートで構成できるようになります。 この場合、ドライバーは、リモート QoS パラメーターに基づいて、操作の QoS パラメーターを解決します。

    また、ミニポートドライバーは、IHV によって定義されている独自の QoS 設定に基づいて、動作する QoS パラメーターを解決することもできます。 ドライバーは、ピアによってリモートで構成されていない、またはオペレーティングシステムによってローカルに構成されていない QoS パラメーターに対してのみ、この操作を実行できます。

    この手順の詳細については、「[リモート NDIS QoS パラメーターの受信](receiving-remote-ndis-qos-parameters.md)」を参照してください。

-   **NDIS\_QOS\_パラメーター\_** 許可フラグが設定されていない場合、ミニポートドライバーはローカルの dcbx の状態を無効にする必要があります。 これにより、ドライバーは、リモート QoS パラメーターではなく、ローカルの QoS パラメーターから操作 QoS パラメーターを解決できます。

    **注**  ローカルの dcbx 許可状態が無効になっている場合でも、ミニポートドライバーはリモート QoS パラメーターを受け入れることができますが、それを使用して操作の qos パラメーターを解決することはできません。

     

ローカルの DCBX の状態が無効になっている場合、ミニポートドライバーは、ローカルの QoS パラメーターを管理するときに、次のガイドラインに従う必要があります。

-   ミニポートドライバーは、関連する**ndis\_qos\_パラメーター\_*XXX*\_構成**フラグが**ndis\_qos\_パラメーターで設定されていないローカル qos パラメーターを無効にするか、上書きする必要があります。Flags**メンバー。

    たとえば、ミニポートドライバーは、構成されていないローカル QoS パラメーターを、IHV によって定義された QoS パラメーターの独自の設定で上書きすることができます。 **NDIS\_qos\_parameters\_*XXX*\_構成**されたフラグで指定されていないローカル qos パラメーターに固有の設定がない場合、ドライバーはネットワークでこれらの QoS パラメーターの使用を無効にする必要があります。アダプター.

    **  ndis**では、 **ndis\_qos\_パラメーター\_構成され**ていること、および**ndis\_qos\_パラメーター\_PFC\_構成されて**いるフラグが設定またはクリアされていることを保証します。一緒に。

     

-   ミニポートドライバーは、運用 NDIS QoS パラメーターを解決するときに、 [**ndis\_qos\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造に含まれるローカルの qos パラメーターを*適用*する必要があります。 ドライバーがこれらのローカル QoS パラメーターを適用する場合、リモートピアから受信したリモート QoS パラメーターを使用することはできません。

    この手順の詳細については、「[オペレーション NDIS QoS パラメーターの解決](resolving-operational-ndis-qos-parameters.md)」を参照してください。

ローカルの DCBX の状態の詳細については、「[ローカルの dcbx の状態の管理](managing-the-local-dcbx-willing-state.md)」を参照してください。

 

 





