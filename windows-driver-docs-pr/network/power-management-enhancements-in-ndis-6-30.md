---
title: NDIS 6.30 の電源管理の機能強化
ms.assetid: A3B64252-DD6C-4715-8D4B-8D8176BC585B
description: コンピューターの電力消費を削減するための NDIS 6.30 電源管理機能の強化について説明します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f70c6577592bf2325bc5435f4226f10322e6a0e5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843502"
---
# <a name="power-management-enhancements-in-ndis-630"></a>NDIS 6.30 の電源管理の機能強化


NDIS 6.20 には、コンピューターの電力消費を削減するための電源管理の新機能と機能強化が含まれています。 Ndis 6.30 では、「[電源管理 (ndis 6.30)](power-management--ndis-6-30-.md)」で説明されているように、次の機能を使用して ndis 6.20 電源管理サポートが拡張されます。

### <a name="ndis-packet-coalescing"></a>NDIS パケット結合

NDIS 6.30 以降では、ネットワークアダプターは NDIS パケット合体をサポートできます。 この機能により、ランダムなブロードキャストまたはマルチキャストパケットの受信によって、ホストシステムでの処理のオーバーヘッドと電力消費が軽減されます。

詳細については、「 [NDIS パケット合体](ndis-packet-coalescing.md)」を参照してください。

### <a name="ndis-selective-suspend"></a>NDIS セレクティブ サスペンド

Ndis 6.30 以降では、ndis の選択的中断インターフェイスを使用して、アダプターを低電力状態に移行することによって、NDIS でアイドル状態のネットワークアダプターを中断できます。 これにより、システムは CPU とネットワークアダプターの電力オーバーヘッドを軽減できます。

詳細については、「 [NDIS の選択的中断](ndis-selective-suspend.md)」を参照してください。

### <a name="ndis-wake-reason-status-indications"></a>NDIS ウェイク理由状態表示

NDIS 6.30 以降では、ミニポートドライバーによって、ndis wake reason ステータス表示 ([**ndis\_status\_PM\_wake\_reason**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)) が発行され、システムウェイクアップイベントの理由について ndis およびそれ以降のドライバーに通知されます。 ネットワークアダプターによってウェイクアップイベントが生成された場合、ミニポートドライバーは、システムがフルパワー状態になったときに、この NDIS ステータスを直ちに発行します。

**注:** モバイルブロードバンド (MB) ミニポートドライバーでは、NDIS wake reason ステータスの  のサポートは省略可能です。

 

詳細については、「 [NDIS Wake Reason Status 兆候](ndis-wake-reason-status-indications.md)」を参照してください。

### <a name="ndis-no-pause-on-suspend"></a>中断されていない NDIS

Ndis 6.30 以降では、ミニポートドライバーは、Ndis\_ミニポート\_アダプターで属性フラグ (**ndis\_ミニポート\_属性\_\_一時停止**\_) を指定でき[ **\_登録\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)構造体。 ドライバーは、 [**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)関数の呼び出しで、この構造体へのポインターを渡します。

ミニポートで Ndis\_ミニポート\_属性が設定されている場合、 **\_SUSPEND 属性フラグの\_\_一時停止\_** 、ndis では、オブジェクト識別子の前にミニポートドライバーの[*miniportpause*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pause)関数が呼び出されません (OID) [\_PNP\_設定](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)されている\_電源がドライバーに発行されていることを要求します。 ミニポートドライバーは OID 要求を処理するときに、低電力状態に移行するためにミニポートアダプターを準備するときに、以前は一時停止していたと想定してはいけません。

詳細については、「 [**NDIS\_ミニポート\_アダプター\_登録\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)」を参照してください。

 

 





