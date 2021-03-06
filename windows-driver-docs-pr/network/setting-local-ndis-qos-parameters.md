---
title: ローカル NDIS QoS パラメーターの設定
description: ローカル NDIS QoS パラメーターの設定
ms.assetid: 7AB30829-16A0-46BF-8066-506E01E718A4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 240a51d2d434629e9d80160ea1605835f9e58950
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375142"
---
# <a name="setting-local-ndis-qos-parameters"></a>ローカル NDIS QoS パラメーターの設定


ローカルの NDIS サービスの品質 (QoS) パラメーターは、ミニポート ドライバーとそのネットワーク アダプターのプロビジョニングされたローカル QoS 設定を指定します。 ミニポート ドライバーでは、次の方法でローカルの NDIS QoS パラメーターを取得します。

-   オブジェクト識別子 (OID) メソッド要求を通じて[OID\_QOS\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-parameters)データ センター ブリッジング (DCB) コンポーネント (Msdcb.sys) によって発行されました。 この OID 要求に含まれる、 [ **NDIS\_QOS\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_qos_parameters)をローカルの NDIS QoS パラメーターを指定します。

    DCB のコンポーネントの詳細については、次を参照してください。[データ センター ブリッジングの NDIS QoS アーキテクチャ](ndis-qos-architecture-for-data-center-bridging.md)します。

    **注**  以降 Windows Server 2012 では、DCB コンポーネントはインストールされ、Microsoft データ センター ブリッジング (DCB) server の機能を有効にします。 既定では、この機能がインストールされていません。

     

-   独自の設定を使用するはシステム レジストリに格納され、ネットワーク アダプターの独立系ハードウェア ベンダー (IHV) で定義されています。 ミニポート ドライバーがこれらの設定を読み取るときにその[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize) NDIS によって呼び出されます。

-   独自の設定を IHV によって開発された管理アプリケーションを通じてミニポート ドライバーに発行します。

DCB のコンポーネントがの OID メソッド要求を発行したとき[OID\_QOS\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-parameters)、 **NDIS\_QOS\_パラメーター\_WILLING**のフラグ、 **NDIS\_QOS\_パラメーター。フラグ**メンバーは、ミニポート ドライバーがローカルの NDIS QoS パラメーターから、運用の QoS パラメーターを解決する方法を指定します。 このフラグに基づき、ドライバーは、次の方法でローカル QoS パラメーターを解決します。

-   場合、 **NDIS\_QOS\_パラメーター\_WILLING**フラグが設定されて、ミニポート ドライバーには、状態のような場面ローカル DCB Exchange (DCBX) が有効にする必要があります。 これにより、QoS パラメーターをリモートで構成するドライバーができます。 この場合、ドライバーは、リモートの QoS パラメーターに基づく運用 QoS パラメーターを解決します。

    ミニポート ドライバーでは、IHV によって定義されている独自の QoS 設定に基づいて、運用の QoS パラメーターを解決することもできます。 QoS パラメーターまたはローカル ピアが、オペレーティング システムによってリモートで構成されていないこのドライバーにはのみことができます。

    この手順の詳細については、次を参照してください。[リモートの NDIS QoS パラメーターを受け取る](receiving-remote-ndis-qos-parameters.md)します。

-   場合、 **NDIS\_QOS\_パラメーター\_WILLING**フラグが設定されていない、ミニポート ドライバーがローカルの DCBX しようとして状態を無効にする必要があります。 これにより、リモートの QoS パラメーターではなく、ローカルの QoS パラメーターから、運用の QoS パラメーターを解決するのには、ドライバーができます。

    **注**  ミニポート ドライバーがリモートの QoS パラメーターを受け付けることができますが、運用上の QoS パラメーターを解決するのには使用できないローカルの DCBX しようとして状態が無効になっている場合。

     

ローカルの DCBX しようとして状態が無効になっている場合、ミニポート ドライバーでは、そのローカル QoS パラメーターを管理する場合これらのガイドラインに従います。

-   ミニポート ドライバーは無効にする必要がありますか、または対象のローカルの QoS パラメーターを上書き関連**NDIS\_QOS\_パラメーター\_*Xxx*\_構成済み**フラグが設定されていない、 **NDIS\_QOS\_パラメーター。フラグ**メンバー。

    たとえば、ミニポート ドライバーは IHV によって定義されている QoS パラメーターに独自の設定を未構成のローカル QoS パラメーターをオーバーライドできます。 ローカルの QoS パラメーターで指定されていない独自の設定がない場合、 **NDIS\_QOS\_パラメーター\_*Xxx*\_構成済み**フラグ、ドライバーは、ネットワーク アダプターにこれらの QoS パラメーターを使用を無効にする必要があります。

    **注**  NDIS に必ず両方、 **NDIS\_QOS\_パラメーター\_ETS\_構成済み**と**NDIS\_QOS\_パラメーター\_PFC\_構成済み**フラグを設定または一緒にクリアします。

     

-   ミニポート ドライバーにする必要があります*適用*ローカル QoS パラメーターに含まれている、 [ **NDIS\_QOS\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体ときに、その運用上の NDIS QoS パラメーターを解決します。 ドライバーは、これらのローカル QoS パラメーターを適用するリモート ピアから受信したリモートの QoS パラメーターを使用する必要があります。

    この手順の詳細については、次を参照してください。[運用上の NDIS QoS パラメーターを解決する](resolving-operational-ndis-qos-parameters.md)します。

ローカル DCBX の詳細については、状態のような場面を参照してください[DCBX 許容状態のローカル管理](managing-the-local-dcbx-willing-state.md)します。

 

 





