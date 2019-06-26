---
title: メディア切断時の省電力
description: メディア切断時の省電力
ms.assetid: 592f3835-47ec-443a-9ab5-e700fed2f7f4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45d5da9822ef33c61dbde1f52b6eb7303be767d3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356204"
---
# <a name="low-power-on-media-disconnect"></a>メディア切断時の省電力





メディア切断の省電力 (D3 の切断) 機能は、メディアが切断されたときに、低電力状態 (D3) にネットワーク アダプターを配置することで電力を節約します。 メディアが再接続されたときにネットワーク アダプターが再びバックアップ (D0) の電力状態にします。

NDIS は、D3 には、これらの条件下で機能を切断します。

-   ネットワーク アダプターのハードウェアは、メディア ウェイク イベントを生成できる必要がありますに接続します。

-   ミニポート ドライバーのネットワーク アダプターのウェイク イベント機能を報告する必要があります、 **MinLinkChangeWakeUp**のメンバー、 [ **NDIS\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_capabilities)構造体。

-   値**MinLinkChangeWakeUp**の値に対応する必要があります、 **DeviceWake**のメンバー、 [**デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_capabilities)によって報告される構造体、 [ **IRP\_MN\_クエリ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities) IRP します。

-   ミニポート ドライバーは、NDIS 6.20 ドライバーまたは以降のバージョンとして登録する必要があります。

-   ネットワーク アダプターはイーサネット PCI アダプターである必要があります。

-   ウェイク イベント機能を有効にする必要があります、  **\*DeviceSleepOnDisconnect** INF ファイルの標準のキーワード。

-   コンピューター チップセットでは、ウェイク イベントを正しく反映されるまで、コンピューターの電源が完全にできる必要があります。 NDIS、DEVPKEY をクエリすることによって検証\_PciDevice\_S0WakeupSupported PCI プロパティ。

D3 に切断注記を使用できるは、動作状態 (S0) でコンピューターの電源が完全にだけです。 コンピューターが、リンクの状態が循環した外部; ときにコンピューターのスリープ解除を防ぐためにスリープ状態に入ったときに、この機能は取り消されますつまり、ときに、スイッチが有効または無効にします。 コンピューターがスリープ状態に入ったときに、低電力状態を参照してください、設定の詳細については[Wake on LAN の低電力](low-power-for-wake-on-lan.md)します。

ミニポート ドライバー レポート D3 には、初期化中に機能を切断します。 詳細については D3 のレポートの機能を切断時を参照してください[電源管理機能の報告](reporting-power-management-capabilities.md)します。

**\*DeviceSleepOnDisconnect** INF ファイルの標準のキーワードは、切断のデバイスが有効になっているまたはで D3 のサポートを無効になっているかどうかを指定します。 この INF キーワードの詳細については、次を参照してください。[電源管理のための標準化された INF キーワード](standardized-inf-keywords-for-power-management.md)します。

初期化中には、D3 の切断をサポートしていますがメディアのオペレーティング システムに通知する機能をサポートできる最下位の電源レベルを報告する必要がありますミニポート ドライバーは、イベントを接続します。 ミニポート ドライバーでの電源のレベルを報告する、 **MinLinkChangeWakeUp**のメンバー、 [ **NDIS\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_capabilities)構造体。 たとえば、ミニポート ドライバーをレポートできます**NdisDeviceStateD3**します。

次の図は、メディア切断イベント後に、ネットワーク アダプターを低電力状態に設定するイベントのシーケンスを示しています。

![メディア切断イベント後に、省電力状態に nic を設定するイベントの順序を示す図](images/d3ondisconnect.png)

アダプターは、メディアの切断を検出すると、次のシーケンスが発生します。

1.  ネットワーク アダプターのハードウェアでは、メディアが切断イベントと、ミニポート ドライバーに情報を渡すを検出します。

2.  ミニポート ドライバーに通知するメディアの NDIS 切断イベントを使用して、 [ **NDIS\_状態\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)状態を示す値。 **StatusBuffer**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)構造に含まれる、 [ **NDIS\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_link_state)構造体。 MediaConnectStateDisconnected 値で設定されます、 **MediaConnectState**のメンバー、 **NDIS\_リンク\_状態**構造体。

3.  NDIS 使用[OID\_PM\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-parameters)ウェイク メディアが接続を Wake on LAN を無効にして有効にする (NDIS\_PM\_WAKE\_ON\_リンク\_変更\_ENABLED 設定されている、 **WakeUpFlags**メンバー)。

4.  NDIS を使用して、 [OID\_PNP\_設定\_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power) OID 新しい電源の状態 (D3) のミニポート ドライバーに通知します。

5.  NDIS PCIe バスに送信、 [ **IRP\_MN\_待機\_WAKE** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake) IRP を再接続イベントを待機します。

6.  NDIS PCIe バスを D3 の状態に設定する、 [ **IRP\_MN\_設定\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power) IRP します。

次の図は、メディア接続イベント後に、ネットワーク アダプターに全機能を復元するイベントのシーケンスを示しています。

![メディア接続イベント後に、nic に全機能を復元するイベントの順序を示す図](images/d0onconnect.png)

メディアが再接続されたときに、次のシーケンスが発生します。

1.  ネットワーク アダプターでは、システムをスリープ ウェイク アサートすることで\#PCIe バスまたは PME\# PCI バスにします。

2.  バスが完了すると、保留中[ **IRP\_MN\_待機\_WAKE** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake) IRP します。 IRP では、保留中の切断のシーケンスの最後の手順を完了します。

3.  NDIS で完全な電源 (D0) バスを設定する、 [ **IRP\_MN\_設定\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power) IRP します。

4.  NDIS は、ネットワーク アダプター、OID と完全な電力 (D0) 状態に設定されての要求をミニポート ドライバーに通知[OID\_PNP\_設定\_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)します。

5.  ネットワーク アダプターに通知するメディアの NDIS 接続イベントを[ **NDIS\_状態\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)状態を示す値。 **MediaConnectStateConnected**値を設定、 **MediaConnectState**のメンバー、 [ **NDIS\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_link_state)構造体。

ミニポート ドライバーがサポートしている場合は、NDIS 6.30、以降[ **NDIS\_状態\_PM\_WAKE\_理由**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)状態のインジケーターにする必要があります発行これ場合は、ネットワーク アダプターがシステムをスリープ状態の通知。 OID は、それが処理中にこの状態の通知を設定するドライバーの問題の要求の[OID\_PNP\_設定\_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power) (D0) の電力状態に遷移します。

詳細については、次を参照してください。 [NDIS Wake 理由状態インジケーター](ndis-wake-reason-status-indications.md)します。

**注**  ミニポート ドライバーが発行された場合、 [ **NDIS\_状態\_PM\_WAKE\_理由**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)状態の表示発行前に行うする必要があります、 [ **NDIS\_状態\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)状態を示す値。

 

 

 





