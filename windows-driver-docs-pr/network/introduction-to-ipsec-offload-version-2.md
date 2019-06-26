---
title: IPsec Offload Version 2 の概要
description: IPsec Offload Version 2 の概要
ms.assetid: d8fd0bf8-f7b6-44ad-a3dc-f10bb20ce651
keywords:
- IPsecOV2 WDK TCP/IP トランスポートは、IPsecOV2 について
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc9d12ecffec7edf84276b5256c0f6dab15dcf98
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378676"
---
# <a name="introduction-to-ipsec-offload-version-2"></a>IPsec Offload Version 2 の概要

\[IPsec タスク オフロード機能は非推奨し、は使用できません。\]




IPsec オフロード バージョン 2 (IPsecOV2) は、IPsec オフロード バージョン 1 (IPsecOV1) で提供されているサービスを拡張します。 IPsecOV1 オフロードと IPsec の詳細については、次を参照してください。 [IPsec オフロード バージョン 1](ipsec-offload-version-1.md)します。

NDIS 6.1 と以降のミニポート ドライバー レポート、IPsecOV2 する NDIS ミニポート アダプターの機能をオフロードします。 IPsec の機能を報告します。

-   初期化中に、ミニポート ドライバーをレポート タスク オフロードの既定の構成およびミニポート アダプターのハードウェア機能、 [ **NDIS\_ミニポート\_アダプター\_オフロード\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_offload_attributes)構造体。

-   ミニポート ドライバーが現在の構成とをレポートする構成済みの機能を変更する場合、 [ **NDIS\_状態\_タスク\_オフロード\_現在\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-current-config)状態を示す値。 場合、構成を変更することができます、 [OID\_TCP\_オフロード\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters) OID ミニポート アダプターの現在のタスク オフロードの構成を設定します。 また場合、ハードウェア構成、 [MUX 中間ドライバー](ndis-mux-intermediate-drivers.md)変更、MUX 中間ドライバーのハードウェア構成の変更を報告する必要があります、 [ **NDIS\_の状態\_タスク\_オフロード\_ハードウェア\_機能**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-hardware-capabilities)状態を示す値。

NDIS ミニポート アダプターのオフロード機能にプロトコル ドライバーに関連する既定の構成を報告する、 [ **NDIS\_バインド\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)構造体。 プロトコル ドライバーに重なって IPsecOV2 タスク オフロード、現在の構成でサポートされているサービスからサービスを選択できます。 [ **NDIS\_状態\_タスク\_オフロード\_現在\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-current-config)状態表示により、後続のすべてプロトコル ドライバーは、新しい機能の情報で更新されます。

初期化中にハードウェアの機能をレポートするときに、ミニポート ドライバーは、レジストリから標準化されたキーワードを読み取る必要があります。 IPsecOV2 オフロード機能の詳細については、次を参照してください。[レポート NIC の IPsec オフロード バージョン 2 機能](reporting-a-nic-s-ipsec-offload-version-2-capabilities.md)します。

**注**  NDIS NDIS 6.1 と以降のドライバーの直接の OID 要求インターフェイスを提供します。 [OID の直接の要求パス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)クエリを実行したり、頻繁に設定されている OID 要求をサポートします。

 

IPsecOV2 の提供、 [OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_追加\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-add-sa)、 [OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_UPDATE\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-update-sa)、および[OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_削除\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-delete-sa)追加、更新、およびセキュリティ アソシエーション (Sa) を削除するプロトコルのドライバーを有効にする OID 要求を送信します。 SAs の詳細については、次を参照してください。 [IPsec オフロード バージョン 2 のセキュリティ アソシエーションを管理する](managing-security-associations-in-ipsec-offload-version-2.md)します。

NIC は、送信で IPsec オフロード タスクを実行し、パスを受信できます。 NDIS ドライバーを使用して、 [ **NDIS\_IPSEC\_オフロード\_V2\_NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_ipsec_offload_v2_net_buffer_list_info)、[ **NDIS\_IPSEC\_オフロード\_V2\_ヘッダー\_NET\_バッファー\_一覧\_情報** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_ipsec_offload_v2_header_net_buffer_list_info)、および[ **NDIS\_IPSEC\_オフロード\_V2\_トンネル\_NET\_バッファー\_ボックスの一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_ipsec_offload_v2_tunnel_net_buffer_list_info) IPsec アウト オブ バンド (OOB) の情報にアクセスする構造体。

上にあるドライバーが OOB 情報の送信 SA と IPsec ヘッダー情報に、ハンドルを設定、送信パス上、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体を指定するにはNIC には、IPsecOV2 オフロード タスクを実行する必要があります。

受信パスでは、SA をオフロードすると後、NIC する必要があります実行 IPsec に NDIS ミニポート ドライバーが報告された機能に一致するすべての受信パケットの処理します。 ミニポート ドライバーは、OOB 情報で適切なフラグを設定、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)特定を指定する構造体は、NIC が実行されるタスクをオフロードし、これらの操作の結果。

送信し、受信 IPsecOV2 の処理についての詳細についてを参照してください。 [IPsec オフロード バージョン 2 でのネットワーク データの送信](sending-network-data-with-ipsec-offload-version-2.md)と[IPsec オフロード バージョン 2 でのネットワーク データの受信](receiving-network-data-with-ipsec-offload-version-2.md)します。

 

 





