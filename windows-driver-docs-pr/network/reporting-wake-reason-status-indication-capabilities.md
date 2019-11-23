---
title: NDIS ウェイク理由状態表示機能のレポート
description: NDIS ウェイク理由状態表示機能のレポート
ms.assetid: A72D04F7-EB09-4B1B-9AF5-7FEBC2514CE9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42accf8a97d710ba5eb3db13be6896ec8fb74a3a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842036"
---
# <a name="reporting-wake-reason-status-indication-capabilities"></a>NDIS ウェイク理由状態表示機能のレポート


NDIS 6.30 以降、ミニポートドライバーは、次のいずれかの原因で発生したウェイクアップイベントを報告するために、NDIS wake reason ステータスを示す ([**ndis\_status\_PM\_wake\_reason**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)) を発行できるかどうかを報告する必要があります。

-   ネットワークアダプターが wake on LAN (WOL) パターンに一致するパケットを受信しました。 これには、オブジェクト識別子 (OID) set 要求によって指定された受信フィルターに一致するパケットの受信が含まれます[\_GEN\_現在の\_パケット\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-packet-filter)です。

    **注**  この種類のウェイクステータスについては、ネットワークアダプターが受信したパケットを保存できる必要があります。 ドライバーは、受信したパケットをステータス表示内で返す必要があります。

     

-   ネットワークアダプターにより、802.11 アクセスポイント (AP) からの関連付け、モバイルブロードバンド (MB) ショートメッセージサービス (SMS) メッセージの受信など、メディア固有のイベントが検出されました。

-   ネットワークアダプターが、WOL パターンまたはメディアの種類 (*メディアに依存*しないイベント) に固有ではない別の有効なイベントを検出しました。 たとえば、デバイスの接続または切断を検出するためにネットワークアダプターが有効になっている場合、ミニポートドライバーは、 [**NDIS\_status\_PM\_WAKE\_REASON**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)ステータス表示を発行します。

**注:** モバイルブロードバンド (MB) ミニポートドライバーでは、NDIS wake reason ステータスの  のサポートは省略可能です。

 

NDIS がドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出すと、ミニポートドライバーは、次の手順に従って、ウェイクアップ理由の状態を示す機能を報告します。

1.  ミニポートドライバーは、基盤となるハードウェアの電源管理機能を使用して、 [**NDIS\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)構造を初期化します。

    Wake reason status 兆候のサポートを有効にするには、ミニポートドライバーで、次のように[**NDIS\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)構造のメンバーを設定する必要があります。

    -   ミニポートドライバーでは、ndis\_PM\_機能\_リビジョン\_2 および NDIS\_SIZEOF\_NDIS\_PM\_機能を指定する必要があります。また、構造体の**ヘッダー**メンバー内にある[**ndis\_pm\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)の構造のリビジョンと長さには、リビジョン\_2 を指定する必要があります。\_
    -   システムウェイクアップイベントの原因となった受信パケットをネットワークアダプターが格納できる場合、ミニポートドライバーは、この構造体の**Flags**メンバー内でサポートされているフラグ\_、NDIS\_PM\_WAKE\_パケット\_を設定します。

        このフラグが設定されている場合、ネットワークアダプターは、アダプターがウェイクアップイベントを生成する原因となった受信パケットを保存できる必要があります。 さらに、ネットワークアダプターがフルパワー状態に移行した後、このパケットでミニポートドライバーが次の操作を実行できる必要があります。

        -   ミニポートドライバーは、 [**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)を呼び出すことによってパケットを示すことができる必要があります。

        -   ミニポートドライバーは、 [**NDIS\_ステータス\_PM\_WAKE\_REASON**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)ステータス表示を発行できる必要があり、パケットに示されたを渡す必要があります。

    -   ミニポートドライバーは、システムのウェイクアップイベントの原因となった WOL パケットを含むバッファーの最大サイズ (バイト単位) に**MaxWoLPacketSaveBuffer**メンバーを設定します。

        **MaxWoLPacketSaveBuffer**メンバーの値は、ネットワークメディアの最大転送単位 (MTU) およびメディアアクセス制御 (MAC) ヘッダーのサイズ (バイト単位) 以下でなければなりません。 このドライバーは、Oid\_GEN の OID クエリ要求を使用して、[最大\_フレーム\_サイズ\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-maximum-frame-size)の MTU サイズを報告します。

    -   ミニポートドライバーは、アダプターがネットワークインターフェイスに接続されたときにウェイクアップイベントを生成するなど、ネットワークアダプターがサポートするメディアに依存しないウェイクアップイベントに**SupportedWakeUpEvents**を設定します。

    -   ミニポートドライバーは、ネットワークアダプターがサポートするメディア固有のウェイクアップイベントに**MediaSpecificWakeUpEvents**を設定します。 これらのイベントには、802.11 アダプターが AP との関連付けが解除されたときのウェイクアップイベントの生成が含まれます。

2.  ミニポートドライバーは、 [**ndis\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)の構造体を初期化し、**PowerManagementCapabilitiesEx**メンバーを、初期化された[**ndis\_PM\_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)構造体のアドレスに設定します。

3.  ミニポートドライバーは、 [**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)関数を呼び出して、その電源管理機能を登録します。 ミニポートドライバーは、この関数を呼び出すと、 *Miniportattributes*パラメーターを[**NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)構造のアドレスに設定します。

Wake reason ステータス表示機能を報告するためにミニポートドライバーによって使用される方法は、電源管理機能を報告するための NDIS 6.20 の方法に基づいています。 この方法の詳細については、「[電源管理機能のレポート](reporting-power-management-capabilities.md)」を参照してください。

アダプター初期化プロセスの詳細については、「[ミニポートアダプターの初期化](initializing-a-miniport-adapter.md)」を参照してください。

電源管理機能を報告する方法の詳細については、「[電源管理機能のレポート](reporting-power-management-capabilities.md)」を参照してください。

 

 





