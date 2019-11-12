---
title: NDIS ウェイク理由状態表示の概要
description: NDIS ウェイク理由状態表示の概要
ms.assetid: 94B54281-7A7E-4DBA-85AE-313EEF09E733
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a158811f25caaba74fa0a62bfcee61f5fa1bc064
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843731"
---
# <a name="overview-of-ndis-wake-reason-status-indications"></a>NDIS ウェイク理由状態表示の概要


NDIS 6.30 以降では、ミニポートドライバーによって、ndis wake reason ステータス表示 ([**ndis\_status\_PM\_wake\_reason**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)) が発行され、システムウェイクアップイベントの理由について ndis およびそれ以降のドライバーに通知されます。 ネットワークアダプターによってウェイクアップイベントが生成された場合、ミニポートドライバーは、ネットワークアダプターがフルパワー状態に復帰したときに、 **ndis\_status\_PM\_wake\_REASON**の ndis 状態を示します。

**注:** モバイルブロードバンド (MB) ミニポートドライバーでは、NDIS wake reason ステータスの  のサポートは省略可能です。

 

ミニポートドライバーは、オブジェクト識別子 (OID) set 要求 ( [oid\_pm\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-parameters)) を使用して、電源管理 (pm) パラメーターで構成されます。 この OID 要求では、 [**NDIS\_pm\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)構造体を使用して pm パラメーターを指定します。

[**NDIS\_PM\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)構造体では、次の種類のウェイクアップイベントのパラメーターを指定します。

<a href="" id="received-packet-wake-up-events"></a>受信パケットウェイクアップイベント  
Wake on LAN (WOL) パターンに一致するパケットを受信すると、ネットワークアダプターはウェイクアップイベントを生成します。 WOL パターンは次のとおりです。

-   パケットペイロード内のマジックパケットや TCP/IP データパターンなど、メディアに依存しない WOL パターン。 たとえば、 [**NDIS\_PM\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)構造体では、TCP SYN フレームの WOL パターンを指定できます。

-   EAPOL 要求識別子パケットやモバイルブロードバンド (MB) ショートメッセージサービス (SMS) メッセージなど、メディア固有の WOL パターン。

-   Oid\_GEN の OID セット要求によって指定された受信フィルターに一致するワイルドカードパターンは、[現在の\_パケット\_フィルター\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-packet-filter)ます。

**注**  この種類のウェイクステータスについては、ネットワークアダプターが受信したパケットを保存できる必要があります。 ドライバーは、受信したパケットをステータス表示内で返す必要があります。

 

WOL パターンは、 [**NDIS\_PM\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)構造体の**EnabledWoLPacketPatterns**メンバーによって指定されます。

<a href="" id="media-specific-wake-up-events"></a>メディア固有のウェイクアップイベント  
ネットワークアダプターは、802.11 アクセスポイント (AP) からの関連付け、モバイルブロードバンド (MB) ショートメッセージサービス (SMS) メッセージの受信など、メディア固有の理由により、ウェイクアップイベントを生成します。

この種類のウェイクアップイベントは、 [**NDIS\_PM\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)構造体の**MediaSpecificWakeUpEvents**メンバーによって指定されます。

<a href="" id="media-independent-wake-up-events"></a>メディアに依存しないウェイクアップイベント  
メディア接続や切断など、メディアに依存しない理由により、ネットワークアダプターはウェイクアップイベントを生成します。

この種類のウェイクアップイベントは、 [**NDIS\_PM\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)構造体の**WakeUpFlags**メンバーによって指定されます。

ミニポートドライバーは、次のガイドラインに従って、NDIS wake reason ステータスを示す必要があります。

-   ミニポートドライバーが、ウェイクアップパケットの兆候を発行する機能をサポートしている場合、NDIS がドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出すときに、この機能を報告する必要があります。 詳細については、「 [Wake Reason Status のレポート機能](reporting-wake-reason-status-indication-capabilities.md)」を参照してください。

    ミニポートドライバーは、WOL パケットの受信に関連付けられていないイベントに対して、NDIS wake reason ステータスを発行する機能を報告する必要はありませ**ん  。**

     

-   ミニポートドライバーは、WOL パケットに対して wake パケットの表示を発行するときに、ウェイクアップイベントの原因となったパケットを含める必要があります。 詳細については、「 [NDIS Wake Reason Status 兆候の発行](issuing-ndis-wake-reason-indications.md)」を参照してください。

-   ネットワークアダプターによってウェイクアップ信号が生成された場合は、ミニポートドライバーは、 [ **\_PM\_ウェイク\_理由**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)を示す状態を示す NDIS\_ステータスを発行する必要があります。 この処理は、フルパワー状態への移行のために、 [oid\_PNP\_\_設定](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)された OID の oid セット要求を処理している間に行われます。

-   ミニポートドライバーは、ウェイクアップイベントに関連する状態を示す通知を発行する前に、 [ **\_PM\_wake\_REASON ステータスを示す NDIS\_status**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)を発行する必要があります。 たとえば、ウェイクアップイベントがメディアの接続状態の変更によって発生した場合、ミニポートドライバーは、ndis の\_ステータス\_PM を発行した後\_状態の状態を示す[ **\_リンクを\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)発行する必要があります。 **\_ウェイク\_理由**の状態を示します。

-   ミニポートドライバーは、 [**NDIS\_status\_pm\_WAKE\_REASON**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)ステータスを示す必要があります。これは、以前は oid Set 要求[oid\_パラメーターによって有効にされていた電源管理イベントのみを示しています。](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-parameters).\_

-   ミニポートドライバーは、基になるネットワークアダプターによって生成されたウェイクアップイベントに対してのみ、 [ **\_PM\_wake\_REASON**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)ステータスを示すために、NDIS\_status を発行する必要があります。

 

 





