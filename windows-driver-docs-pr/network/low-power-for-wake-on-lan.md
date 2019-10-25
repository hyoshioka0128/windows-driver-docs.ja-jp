---
title: Wake On LAN 用の省電力
description: Wake On LAN 用の省電力
ms.assetid: 9ab8fa19-e75a-4266-accf-4e8b2964f82e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0610151f88b860fc002e441a1a97b847dcf3c3fd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844137"
---
# <a name="low-power-for-wake-on-lan"></a>Wake On LAN 用の省電力





Wake on LAN (WOL) 機能は、ネットワークアダプターが WOL イベントを検出したときに、コンピューターを低電力状態からスリープ解除します。

ミニポートドライバーは、初期化中にネットワークアダプター WOL 機能を報告します。 レポート WOL 機能の詳細については、「[電源管理機能のレポート](reporting-power-management-capabilities.md)」を参照してください。

リンクの状態が外部で切り替えられたときにコンピューターのスリープ状態が解除されるのを防ぐために、コンピューターがスリープ状態になると、[メディア切断 (切断時に D3)] 機能の電源が少なくなることに注意してください。つまり、スイッチがオフになっていて、オンになっている場合です。 切断時の D3 の詳細については、「[低電力オンメディア切断](low-power-on-media-disconnect.md)」を参照してください。

次の図は、ネットワークアダプターを低電力状態に設定する場合に発生する一連のイベントを示しています。

![nic を低電力状態に設定するイベントのシーケンスを示す図](images/d3onsleep.png)

NDIS がネットワークアダプターを低電力状態にすると、次のような処理が行われます。

1.  NDIS では、 [\_PM\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-parameters)を使用して WAKE on LAN を有効にし、wake on media connect を無効にします。 NDIS\_PM\_WAKE\_ON\_リンク\_変更\_有効になっているのは、 **WakeUpFlags**メンバーです。

2.  NDIS は、 [OID\_PNP](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)を使用して\_電力を設定し、新しい電源状態 (D3) のミニポートドライバーに通知\_します。

3.  ミニポートドライバーは、 [**NDIS\_の状態\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)の状態の表示を使用して、不明なメディアの接続状態を示している可能性があります。 **MediaConnectStateUnknown**値は、 [**NDIS\_LINK\_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state)構造体の**MediaConnectState**メンバーで設定されます。 詳細については、「 [**NDIS\_の状態」\_リンク\_の状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)に関するドキュメントを参照してください。

4.  NDIS は、PCI Express (PCIe) バスを送信します。これ[ **\_は\_待機\_WAKE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake) IRP を待機して、WOL イベントを待機します。

5.  NDIS は、バスを D3 状態に設定するために、 [ **\_電源 irp を\_設定**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)して、PCIe バス a irp\_を送信します。

次の図は、WOL イベントの後でネットワークアダプターに電力を完全に復元するために発生するイベントのシーケンスを示しています。

![wol イベント後に nic へのフルパワーを復元するイベントのシーケンスを示す図](images/d0onwol.png)

ネットワークアダプターがコンピューターをスリープ解除すると、次のシーケンスが発生します。

1.  ネットワークアダプターは、PCI バス上の PCIe バスまたは PME\# で WAKE\# をアサートすることによって、システムをスリープ解除します。

2.  バスは、保留中の[**irp\_完了\_待機\_ウェイク**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)irp を完了します。 IRP は、電源ダウンシーケンスの最後のステップから完了を待ちます。

3.  NDIS は、バスをフルパワー (D0) に設定します。 [**irp\_\_設定され\_電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)irp を使用します。

4.  NDIS は、ネットワークアダプターがいっぱいになっていることをミニポートドライバーに通知します。これは、 [\_PNP\_設定](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)された oid の oid セット要求を使用して\_ます。

5.  ネットワークアダプターは、 [**ndis\_状態\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)の状態の表示を使用して、メディア接続イベントを ndis に通知します。 **MediaConnectStateConnected**値は、 [**NDIS\_LINK\_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state)構造体の**MediaConnectState**メンバーで設定されます。

NDIS 6.30 以降では、ミニポートドライバーが[**ndis\_status\_PM\_WAKE\_REASON**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)状態を示している場合、ネットワークアダプターがシステムをスリープ解除すると、この状態通知を発行する必要があります。 このドライバーは、フルパワー (D0) 状態への移行のために[電源\_設定](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)された oid\_\_の oid セット要求を処理しているときに、この状態通知を発行します。

詳細については、「 [NDIS Wake Reason Status 兆候](ndis-wake-reason-status-indications.md)」を参照してください。

 

 





