---
title: Wake On LAN 用の省電力
description: Wake On LAN 用の省電力
ms.assetid: 9ab8fa19-e75a-4266-accf-4e8b2964f82e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39acf24d3f0994a5639079a277e2f37255e91304
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356235"
---
# <a name="low-power-for-wake-on-lan"></a>Wake On LAN 用の省電力





Wake on LAN (WOL) 機能は、ネットワーク アダプターが、WOL イベントを検出すると、コンピューターの省電力状態を解除します。

ミニポート ドライバーでは、初期化中にネットワーク アダプターの WOL 機能を報告します。 WOL 機能をレポートの詳細については、次を参照してください。[電源管理機能の報告](reporting-power-management-capabilities.md)します。

メディアの下の電源の切断に注意してください (D3 の切断) リンクの状態が循環した外部; ときにコンピューターのスリープ解除を回避するには、コンピューターがスリープ状態に入ったときに機能が取り消されましたつまり、ときに、スイッチが有効または無効にします。 詳細については D3 切断時は、「[メディア切断の低電力](low-power-on-media-disconnect.md)します。

次の図は、ネットワーク アダプターを低電力状態に設定するに発生するイベントの順序を示します。

![nic を低電力状態に設定するイベントの順序を示す図](images/d3onsleep.png)

NDIS は、ネットワーク アダプターを低電力状態に、次のシーケンスが発生します。

1.  NDIS 使用[OID\_PM\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-parameters)ウェイク メディアが接続を wake on LAN を有効にすると、無効にします。 NDIS\_PM\_WAKE\_ON\_リンク\_変更\_ENABLED がオフになって、 **WakeUpFlags**メンバー。

2.  NDIS 使用[OID\_PNP\_設定\_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)新しい電源の状態 (D3) のミニポート ドライバーに通知します。

3.  ミニポート ドライバーが、不明なメディア接続を使用して状態を示す、 [ **NDIS\_状態\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)状態を示す値。 **MediaConnectStateUnknown**値を設定、 **MediaConnectState**のメンバー、 [ **NDIS\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_link_state)構造体。 詳細については、次を参照してください。、 [ **NDIS\_状態\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)ドキュメント。

4.  NDIS PCI Express (PCIe) バスに送信する[ **IRP\_MN\_待機\_WAKE** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake) IRP WOL イベントを待機します。

5.  NDIS PCIe バスに送信、 [ **IRP\_MN\_設定\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power) IRP をバス D3 状態に設定されます。

次の図は、ネットワーク アダプターに WOL イベントの後に全機能を復元する発生するイベントのシーケンスを示しています。

![wol イベントの後に、nic に完全な電源を復旧するイベントのシーケンスを示す図](images/d0onwol.png)

ネットワーク アダプターが、コンピューターをスリープ解除するときは、次のシーケンスが発生します。

1.  ネットワーク アダプターでは、システムをスリープ ウェイク アサートすることで\#PCIe バスまたは PME\# PCI バスにします。

2.  バスが完了すると、保留中[ **IRP\_MN\_待機\_WAKE** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake) IRP します。 IRP では、保留中のシーケンスの電源の最後の手順を完了します。

3.  NDIS で完全な電源 (D0) バスを設定する、 [ **IRP\_MN\_設定\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power) IRP します。

4.  NDIS の OID のセットの要求でネットワーク アダプターが (D0) 能力を最大限にミニポート ドライバーに通知[OID\_PNP\_設定\_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)します。

5.  ネットワーク アダプターに通知するメディアの NDIS 接続イベントを[ **NDIS\_状態\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)状態を示す値。 **MediaConnectStateConnected**値を設定、 **MediaConnectState**のメンバー、 [ **NDIS\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_link_state)構造体。

ミニポート ドライバーがサポートしている場合は、NDIS 6.30、以降[ **NDIS\_状態\_PM\_WAKE\_理由**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)状態のインジケーターにする必要があります発行これ場合は、ネットワーク アダプターがシステムをスリープ状態の通知。 OID は、それが処理中にこの状態の通知を設定するドライバーの問題の要求の[OID\_PNP\_設定\_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power) (D0) の電力状態に遷移します。

詳細については、次を参照してください。 [NDIS Wake 理由状態インジケーター](ndis-wake-reason-status-indications.md)します。

 

 





