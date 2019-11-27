---
title: NDIS ウェイク理由状態表示の発行
description: NDIS ウェイク理由状態表示の発行
ms.assetid: F3DBE0DB-9787-4C3D-8DE3-AD47E5778B21
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5989c7469feb469662614271a5f4ace83cec5ef6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844155"
---
# <a name="issuing-ndis-wake-reason-status-indications"></a>NDIS ウェイク理由状態表示の発行


ミニポートドライバーが NDIS wake reason status ([**ndis\_status\_PM\_wake\_reason**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)) をサポートしている場合、ネットワークアダプターがウェイクアップイベントを生成し、アダプターがフルパワー状態に戻ります。

**メモ** モバイルブロードバンド (MB) ミニポートドライバーでは、NDIS wake reason ステータスのインジケーターのサポートは省略可能です。

ミニポートドライバーは、オブジェクト識別子 (OID) set 要求 ( [oid\_pm\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-parameters)) を使用して、電源管理 (pm) パラメーターで構成されます。 この OID 要求では、 [**NDIS\_pm\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)構造体を使用して pm パラメーターを指定します。

[**NDIS\_PM\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)構造体では、次の種類のウェイクアップイベントのパラメーターを指定します。

<a href="" id="received-packet-wake-up-events"></a>受信パケットウェイクアップイベント  
Wake on LAN (WOL) パターンに一致するパケットを受信すると、ネットワークアダプターはウェイクアップイベントを生成します。 WOL パターンは次のとおりです。

-   パケットペイロード内のマジックパケットや TCP/IP データパターンなど、メディアに依存しない WOL パターン。 たとえば、 [**NDIS\_PM\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)構造体では、TCP SYN フレームの WOL パターンを指定できます。

-   EAPOL 要求識別子パケットやモバイルブロードバンド (MB) ショートメッセージサービス (SMS) メッセージなど、メディア固有の WOL パターン。

-   Oid\_GEN の OID セット要求によって指定された受信フィルターに一致するワイルドカードパターンは、[現在の\_パケット\_フィルター\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-packet-filter)ます。

**メモ** この種類のスリープ解除の理由を示すために、ネットワークアダプターは受信したパケットを保存できる必要があります。 ドライバーは、受信したパケットをステータス表示内で返す必要があります。

WOL パターンは、 [**NDIS\_PM\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)構造体の**EnabledWoLPacketPatterns**メンバーによって指定されます。

<a href="" id="media-specific-wake-up-events"></a>メディア固有のウェイクアップイベント  
ネットワークアダプターは、802.11 アクセスポイント (AP) からの関連付け、モバイルブロードバンド (MB) ショートメッセージサービス (SMS) メッセージの受信など、メディア固有の理由により、ウェイクアップイベントを生成します。

この種類のウェイクアップイベントは、 [**NDIS\_PM\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)構造体の**MediaSpecificWakeUpEvents**メンバーによって指定されます。

<a href="" id="media-independent-wake-up-events"></a>メディアに依存しないウェイクアップイベント  
メディア接続や切断など、メディアに依存しない理由により、ネットワークアダプターはウェイクアップイベントを生成します。

この種類のウェイクアップイベントは、 [**NDIS\_PM\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)構造体の**WakeUpFlags**メンバーによって指定されます。

ネットワークアダプターによってウェイクアップ信号が生成された場合は、ミニポートドライバーは、 [ **\_PM\_ウェイク\_理由**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)を示す状態を示す NDIS\_ステータスを発行する必要があります。 この処理は、アダプターをフルパワー状態に移行するために、 [oid\_PNP\_\_設定](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)された OID の oid セット要求を処理している間に行われます。

**メモ** ミニポートドライバーは、ウェイクアップイベントに関連する状態を示す通知を発行する前に、 [ **\_PM\_wake\_REASON ステータスを示す NDIS\_status**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)を発行する必要があります。 たとえば、ウェイクアップイベントがメディアの接続状態の変更によって発生した場合、ミニポートドライバーは、ndis の\_ステータス\_PM を発行した後\_状態の状態を示す[ **\_リンクを\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)発行する必要があります。 **\_ウェイク\_理由**の状態を示します。

ミニポートドライバーが[**NDIS\_status\_PM\_WAKE\_REASON**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)状態を示す場合は、次の手順に従う必要があります。

1.  ミニポートドライバーは、次のものを格納するのに十分な大きさのバッファーを割り当てる必要があります。

    -   [**NDIS\_PM\_ウェイク\_REASON**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_reason)構造体。

    -   [**NDIS\_PM\_wake\_パケット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_packet)構造と共に、ネットワークアダプターがウェイクアップイベントを生成する原因となった受信パケット (*ウェイクアップパケット*) と共に使用します。

        **メモ** ミニポートドライバーは、メディア固有またはメディアに依存しないウェイクアップイベントを示す場合、このバッファー領域を割り当てる必要はありません。

2.  ミニポートドライバーは、バッファーの開始時に、 [**NDIS\_PM\_WAKE\_REASON**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_reason)構造体を初期化します。 このドライバーは、ウェイクアップイベントの種類を定義する**WakeReason**メンバーを、 [**NDIS\_PM\_wake\_REASON\_type**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_pm_wake_reason_type)列挙値に設定します。

    たとえば、ミニポートドライバーが受信パケットウェイクアップイベントを示す場合、 **WakeReason**メンバーを**NdisWakeReasonPacket**に設定する必要があります。 それ以外の場合、ドライバーは、メディア固有またはメディアに依存しないウェイクアップイベントに最も近い列挙値に**WakeReason**メンバーを設定します。

3.  Miniportdriver が NDIS\_STATUS を発行している場合は[ **\_PM\_wake\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)の状態を示す受信パケットウェイクアップイベントについて、次の手順に従う必要があります。

    1.  ミニポートドライバーは、バッファー内の[**ndis\_PM\_wake\_REASON**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_reason)構造体に続く[**ndis\_pm\_wake\_パケット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_packet)構造のオフセットに、 **infobufferoffset**メンバーを設定します。

        **メモ** ミニポートドライバーは、64ビットの境界で、 [**NDIS\_PM\_WAKE\_パケット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_packet)構造の開始位置を揃える必要があります。

    2.  このミニポートドライバーは、 **Infobuffersize**メンバーを[**NDIS\_PM\_wake\_パケット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_packet)構造のサイズに、ウェイクアップイベントの原因となったパケットのサイズを設定します。

    3.  ミニポートドライバーは、ndis [ **\_pm\_wake\_REASON**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_reason)構造体をバッファーに置いた後に、 [**ndis\_pm\_wake\_パケット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_packet)構造を初期化します。

        ミニポートドライバーは、次のように、 [**NDIS\_PM\_WAKE\_パケット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_packet)構造のメンバーを設定します。

        -   **PatternId**メンバーは、ウェイクアップパケットと一致する WOL パターンの識別子に設定されます。 この識別子は、 [**NDIS\_pm\_WOL\_pattern**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)構造の**PatternId**メンバーによって指定されます。これは、Oid 設定要求の[OID\_PM\_\_WOL\_PATTERN の追加によってドライバーに渡されます。](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-add-wol-pattern).

        -   **Pattern friendlyname**メンバーは、 **PatternId**メンバーによって指定されたウェイクパターンのユーザーが判読できる説明に設定されます。 この値は、 [**NDIS\_PM\_WOL\_PATTERN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)構造体の**FriendlyName**メンバーによって指定されます。

            **メモ** ミニポートドライバーは、このメンバーを初期化する必要はありません。 NDIS は、 [ **\_PM\_WAKE\_PACKET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_packet)構造体を後続のドライバーに渡す前に、 **pattern friendlyname**メンバーを正しい値に設定します。

        -   **OriginalPacketSize**メンバーは、ネットワークアダプターが受信したパケットの長さに設定されます。

        -   **SavedPacketSize**メンバーは、 [**NDIS\_status\_PM\_WAKE\_REASON**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)ステータス表示によって報告されるパケットの長さに設定する必要があります。

            **メモ** このメンバーの値は、 [**NDIS\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)の構造体の**MaxWoLPacketSaveBuffer**メンバーで設定されているミニポートドライバーの値より大きくすることはできません。 ドライバーは、スリープ解除パケットの表示機能を報告するときに、この構造体を返します。 詳細については、「 [Wake Reason Status のレポート機能](reporting-wake-reason-status-indication-capabilities.md)」を参照してください。

        -   **SavedPacketOffset**メンバーは、 [**NDIS\_PM\_wake\_パケット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_packet)構造に続く wake パケットのバイト単位のオフセットに設定する必要があります。

            **メモ** ミニポートドライバーは、バッファー内の64ビット境界で wake パケットの開始位置を揃える必要があります。

    4.  ミニポートは、 **SavedPacketOffset**メンバーによって指定されたオフセットで、ウェイクアップパケットをバッファーにコピーします。

4.  ミニポートドライバーが[**NDIS\_status\_PM\_wake\_REASON**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)状態を発行している場合、メディア固有またはメディアに依存しないウェイクアップイベントについて、**インフォ Bufferoffset**と**インフォ buffersize**を設定します。[**NDIS\_PM\_WAKE\_REASON**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wake_reason)構造体のメンバーが0になります。

5.  ミニポートドライバーは、 [**NDIS\_ステータス\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)表示構造体を初期化します。 ドライバーは、 **StatusCode**メンバーを NDIS\_STATUS\_PM\_WAKE\_REASON に設定します。 また、ドライバーは、 **statusbuffer**メンバーがバッファーを指すように設定し、 **statusbufferlength**をバッファーの長さ (バイト単位) に設定します。

6.  ミニポートドライバーは[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)を呼び出し、 *statusindication*パラメーターに、 [**NDIS\_STATUS\_を示す**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)構造体へのポインターを渡します。

**メモ** ミニポートドライバーによって、 [**NDIS\_status\_PM\_WAKE\_REASON**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)ステータスが返された後、受信したパケットウェイクアップイベントについては、 [**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)を呼び出すことによって、この受信パケットを示す必要があります。