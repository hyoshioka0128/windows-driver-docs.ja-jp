---
title: 電源管理パラメーターの取得と更新
description: 電源管理パラメーターの取得と更新
ms.assetid: 46c4d2ab-e6d9-4d23-bf40-0037b80b01af
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5ea9ffbcb9c2cfbb4cbb98d034f63557f4e08d6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837747"
---
# <a name="obtaining-and-updating-power-management-parameters"></a>電源管理パラメーターの取得と更新





プロトコルドライバーは、 [oid\_PM\_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-parameters) oid を使用して、現在有効になっているネットワークアダプターのハードウェア機能を照会できます。 クエリから正常に戻った後、 [**ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、 [**ndis\_PM\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)構造体へのポインターが含まれています。

プロトコルドライバーでは、ネットワークアダプターの現在のハードウェア機能を有効または無効にするための設定要求として、OID\_PM\_パラメーターを使用することもできます。 プロトコルドライバーは、ndis\_OID\_要求構造の**Informationbuffer**メンバー内にある NDIS\_PM\_PARAMETERS 構造体へのポインターを提供します。

**注**  プロトコルドライブは、他のプロトコルドライバーによって有効にされた機能を無効にすることはできません。 プロトコルドライバーによって機能が有効になっていない場合、その機能は使用されません。

 

**  NDIS**では、ユーザー設定に基づいてマジックパケットと低電力の切断機能が有効になっており、これらの機能をプロトコルドライバーで無効にすることはできません。

 

NDIS\_PM\_パラメーターには、次の情報が含まれています。

<a href="" id="enabledwolpacketpatterns"></a>**EnabledWoLPacketPatterns**  
[**NDIS\_PM\_capabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)構造体の**SupportedWoLPacketPatterns**メンバーでミニポートドライバーによって報告された機能に対応するフラグを格納します。 たとえば、ネットワークアダプターは、ビットマップ、WOL マジックパケット、または EAP over LAN (EAPOL) 要求識別子メッセージを受信したときにウェイクアップイベントを生成するように有効になっています。 現在のオペレーティングシステムで使用可能なパターンの完全な一覧については、「 [**NDIS\_PM\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)のリファレンス」ページを参照してください。

<a href="" id="enabledprotocoloffloads"></a>**EnabledProtocolOffloads**  
[**NDIS\_PM\_capabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)構造体の**SupportedProtocolOffloads**メンバーでミニポートドライバーによって報告された機能に対応するフラグを格納します。 NDIS は、これらのフラグを使用して、ネットワークアダプターの低電力プロトコルオフロード機能を有効または無効にします。 たとえば、IPv4 ARP、IPv6 近隣要請 (NS)、または IEEE 802.11 の堅牢なセキュリティで保護されたネットワーク (RSN) の4方向および双方向のハンドシェイクのネットワークアダプターオフロードが有効になっています。 現在のオペレーティングシステムでサポートされているプロトコルオフロードの完全な一覧については、「 [**NDIS\_PM\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)のリファレンス」ページを参照してください。

<a href="" id="wakeupflags"></a>**WakeUpFlags**  
ネットワークアダプターでウェイクアップ機能を有効または無効にするために NDIS が使用するフラグが含まれています。

NDIS 6.20 の場合、NDIS\_PM\_WAKE\_ON\_LINK\_CHANGE\_ENABLED フラグによって、リンク変更 (メディア接続) でのスリープ解除機能が有効になります。 このフラグの詳細については、「[低電力オンメディア切断](low-power-on-media-disconnect.md)」を参照してください。

Ndis 6.30 以降では、NDIS\_PM\_選択的\_SUSPEND\_ENABLED フラグにより、基になる USB ネットワークアダプターでの NDIS セレクティブサスペンドのサポートが有効になります。 詳細については、「 [NDIS の選択的中断](ndis-selective-suspend.md)」を参照してください。

ドライバーが[oid\_PM\_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-parameters) oid を設定すると、NDIS はミニポートドライバーに転送せずに要求を完了します。 NDIS は、要求された設定を格納し、その他の要求の設定と組み合わせます。

Ndis は、ネットワークアダプターを低電力状態に移行する前に、ndis が格納したすべての要求の組み合わせた設定を含むミニポートドライバーにセット要求を送信します。 低電力状態の設定の詳細については、「 [Wake ON LAN の低電力](low-power-for-wake-on-lan.md)」を参照してください。

現在有効になっている機能は、ハードウェアがサポートする機能のサブセットにすることができます。 ハードウェアがサポートする機能の詳細については、「[電源管理機能のレポート](reporting-power-management-capabilities.md)」を参照してください。

 

 





