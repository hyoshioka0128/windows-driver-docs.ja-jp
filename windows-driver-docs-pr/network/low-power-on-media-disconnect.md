---
title: メディア切断時の省電力
description: メディア切断時の省電力
ms.assetid: 592f3835-47ec-443a-9ab5-e700fed2f7f4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: afabbff8ec4d34f2e5218c659c0fb2223e52532b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844135"
---
# <a name="low-power-on-media-disconnect"></a>メディア切断時の省電力





メディアの切断 (切断時に D3) 機能は、メディアが切断されたときにネットワークアダプターを低電力状態 (D3) に配置することで電力を節約します。 メディアが再接続されると、ネットワークアダプターがフルパワー状態 (D0) に戻されます。

NDIS は、次の条件下で D3 on disconnect 機能を使用します。

-   ネットワークアダプターのハードウェアは、メディア接続でウェイクイベントを生成できる必要があります。

-   ミニポートドライバーは、 [**NDIS\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)の構造の**Minlinkchangewakeup**メンバーのネットワークアダプターの wake イベント機能を報告する必要があります。

-   **Minlinkchangewakeup**の値は、[**デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)の構造の**devicewake**メンバーの値に対応している必要があります。この値は、 [**irp\_、\_クエリ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)の irp によって報告されます。

-   ミニポートドライバーは、NDIS 6.20 ドライバーまたはそれ以降のバージョンとして登録する必要があります。

-   ネットワークアダプターは、イーサネット PCI アダプターである必要があります。

-   Wake イベント機能は、 **\*DeviceSleepOnDisconnect** standard INF file キーワードで有効にする必要があります。

-   コンピューターの電源が入っている間は、コンピューターのチップセットで wake イベントを正しく伝達できる必要があります。 NDIS は、DEVPKEY\_PciDevice\_S0WakeupSupported PCI プロパティを照会することによってこれを検証します。

切断時の D3 は、コンピューターの動作状態 (S0) が完全に機能している場合にのみ使用できます。 この機能は、コンピューターがスリープ状態になったときにキャンセルされ、リンクの状態が外部で切り替えられたときにコンピューターがスリープ解除されるのを防ぎます。つまり、スイッチがオフになっていて、オンになっている場合です。 コンピューターがスリープ状態に入るときの低電力状態の設定の詳細については、「 [Wake ON LAN の低電力](low-power-for-wake-on-lan.md)」を参照してください。

ミニポートドライバーは、初期化中に切断機能について D3 を報告します。 切断機能のレポート D3 の詳細については、「[電源管理機能のレポート](reporting-power-management-capabilities.md)」を参照してください。

**\*DeviceSleepOnDisconnect** standard INF file キーワードは、デバイスが切断時に D3 のサポートを有効または無効にしたかどうかを指定します。 この INF キーワードの詳細については、「 [Power Management の標準化](standardized-inf-keywords-for-power-management.md)された inf キーワード」を参照してください。

初期化中に、切断時に D3 をサポートするミニポートドライバーは、メディア接続イベントのオペレーティングシステムに通知する機能をサポートできる最も低い電源レベルを報告する必要があります。 ミニポートドライバーは、 [**NDIS\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)構造の**Minlinkchangewakeup**メンバーの電源レベルを報告します。 たとえば、ミニポートドライバーは**NdisDeviceStateD3**を報告できます。

次の図は、メディアの切断イベント後にネットワークアダプターを低電力状態に設定するイベントのシーケンスを示しています。

![メディアの切断イベント後に nic を低電力状態に設定するイベントのシーケンスを示す図](images/d3ondisconnect.png)

アダプターがメディアの切断を検出すると、次の順序が発生します。

1.  ネットワークアダプターのハードウェアは、メディアの切断イベントを検出し、その情報をミニポートドライバーに渡します。

2.  ミニポートドライバーは、 [**ndis\_の状態\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)の状態の表示を使用して、メディアの切断イベントを ndis に通知します。 [**Ndis\_ステータス\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)表示構造体の**statusbuffer**メンバーには、 [**ndis\_LINK\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state)構造体が含まれています。 MediaConnectStateDisconnected 値は、 **NDIS\_LINK\_STATE**構造体の**MediaConnectState**メンバーで設定されます。

3.  NDIS は、 [\_PM\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-parameters)を使用して WAKE on LAN を無効にし、wake on media connect を有効にします (NDIS\_PM\_WAKE\_ON\_LINK\_CHANGE\_ENABLED は**WakeUpFlags**メンバーに設定されています)。

4.  NDIS は、 [oid\_PNP\_設定\_power](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power) oid を使用して、新しい電源状態 (D3) をミニポートドライバーに通知します。

5.  NDIS は、再接続イベントを待機するために、[**ウェイクアップ\_ウェイク irp を\_待機**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)するように、PCIe バスを送信し\_します。

6.  NDIS は、 [**irp\_\_設定**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)された\_電源 irp を使用して、PCIe バスを D3 状態に設定します。

次の図は、メディア接続イベント後にネットワークアダプターに電力を完全に復元するイベントのシーケンスを示しています。

![メディア接続イベント後に nic にフルパワーを復元するイベントのシーケンスを示す図](images/d0onconnect.png)

メディアが再接続されると、次のシーケンスが発生します。

1.  ネットワークアダプターは、PCI バス上の PCIe バスまたは PME\# で WAKE\# をアサートすることによって、システムをスリープ解除します。

2.  バスは、保留中の[**irp\_完了\_待機\_ウェイク**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)irp を完了します。 IRP は、切断シーケンスの最後のステップからの完了を保留しています。

3.  NDIS は、バスをフルパワー (D0) に設定します。 [**irp\_\_設定され\_電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)irp を使用します。

4.  NDIS は、ネットワークアダプターが完全な電力 (D0) 状態であることを通知します。これは、 [\_PNP\_設定](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)された oid の oid セット要求と\_電源が設定されていることを示します。

5.  ネットワークアダプターは、 [**ndis\_状態\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)の状態の表示を使用して、メディア接続イベントを ndis に通知します。 **MediaConnectStateConnected**値は、 [**NDIS\_LINK\_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state)構造体の**MediaConnectState**メンバーで設定されます。

NDIS 6.30 以降では、ミニポートドライバーが[**ndis\_status\_PM\_WAKE\_REASON**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)状態を示している場合、ネットワークアダプターがシステムをスリープ解除すると、この状態通知を発行する必要があります。 このドライバーは、フルパワー (D0) 状態への移行のために[電源\_設定](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)された oid\_\_の oid セット要求を処理しているときに、この状態通知を発行します。

詳細については、「 [NDIS Wake Reason Status 兆候](ndis-wake-reason-status-indications.md)」を参照してください。

**注:** ミニポートドライバーが[ **\_ステータス\_PM\_WAKE\_REASON**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)  を発行する場合は、 [**ndis\_状態\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)を発行する前に、この操作を行う必要があります。状態を示します。

 

 

 





