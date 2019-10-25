---
title: IPsec Offload Version 2 の概要
description: IPsec Offload Version 2 の概要
ms.assetid: d8fd0bf8-f7b6-44ad-a3dc-f10bb20ce651
keywords:
- IPsecOV2 WDK TCP/IP transport、IPsecOV2 について
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9565942f7a7bf983626702d4ac8982ad3c1d75e9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844173"
---
# <a name="introduction-to-ipsec-offload-version-2"></a>IPsec Offload Version 2 の概要

\[IPsec タスクオフロード機能は非推奨とされているため、使用しないでください。\]




IPsec オフロードバージョン 2 (IPsecOV2) は、IPsec オフロードバージョン 1 (IPsecOV1) で提供されるサービスを拡張します。 IPsecOV1 オフロードと IPsec の詳細については、「 [Ipsec オフロードバージョン 1](ipsec-offload-version-1.md)」を参照してください。

NDIS 6.1 以降のミニポートドライバーは、ミニポートアダプターの IPsecOV2 オフロード機能を NDIS に報告します。 IPsec 機能を報告するには:

-   初期化中に、ミニポートドライバーは、タスクオフロードの既定の構成と、 [**NDIS\_ミニポート\_アダプター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_offload_attributes)のミニポートアダプターのハードウェア機能を報告し、\_属性の構造\_オフロードします。

-   構成した機能が変更された場合は、現在の構成が、ミニポートドライバーによって、 [**NDIS\_ステータス\_タスク\_オフロード\_現在の\_構成**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-current-config)状態が表示されます。 構成は、 [oid\_TCP\_オフロード\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters) oid によって、ミニポートアダプターの現在のタスクオフロード構成が設定されている場合に変更される可能性があります。 また、 [mux 中間ドライバー](ndis-mux-intermediate-drivers.md)のハードウェア構成が変更された場合、mux 中間ドライバーは、ハードウェア構成の変更を、 [**NDIS\_STATUS\_タスク\_オフロード\_ハードウェアに報告する必要があり\_機能**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-hardware-capabilities)の状態を示します。

NDIS は、ミニポートアダプターのオフロード機能の既定の構成を、 [**ndis\_BIND\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)構造体のプロトコルドライバーに報告します。 プロトコルドライバーでは、現在の構成でサポートされているサービスから IPsecOV2 タスクオフロードサービスを選択できます。 [**NDIS\_status\_タスク\_オフロード\_現在の\_構成**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-current-config)の状態の表示では、すべてのプロトコルドライバーが新機能の情報で更新されます。

初期化中にハードウェア機能を報告する場合、ミニポートドライバーはレジストリから標準化されたキーワードを読み取る必要があります。 IPsecOV2 オフロード機能の詳細については、「 [NIC の IPsec オフロードバージョン2機能の報告](reporting-a-nic-s-ipsec-offload-version-2-capabilities.md)」を参照してください。

**  ndis**は、ndis 6.1 以降のドライバー用の直接 OID 要求インターフェイスを提供します。 [直接 oid 要求パス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)は、クエリまたは頻繁に設定される oid 要求をサポートしています。

 

IPsecOV2 は、 [ipsec\_オフロード\_v2\_\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-add-sa)、 [OID\_TCP\_タスク\_ipsec\_オフロード\_V2 @no__t_ を追加する\_の\_TCP タスク\_の oid を提供14_ UPDATE\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-update-sa)、 [OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-delete-sa)直接 OID 要求を削除して、プロトコルドライバーの追加、更新を有効にします。を削除し、セキュリティアソシエーション (SAs) を削除します。 SAs の詳細については、「 [IPsec オフロードバージョン2でのセキュリティアソシエーションの管理](managing-security-associations-in-ipsec-offload-version-2.md)」を参照してください。

NIC は、送信パスと受信パスに対して IPsec オフロードタスクを実行できます。 NDIS ドライバーでは、 [**ndis\_ipsec\_オフロード\_V2\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_net_buffer_list_info)、 [**NDIS\_IPSEC\_OFFLOAD\_V2\_HEADER\_NET\_BUFFER\_LIST\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_header_net_buffer_list_info)、および[**NDIS\_ipsec\_オフロード\_V2\_トンネル\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_tunnel_net_buffer_list_info)構造体を使用して ipsec アウトオブバンド (OOB) にアクセスする参照.

送信パスでは、これ以降のドライバーは、IPsecOV2 のオフロードタスクを実行する必要があることを指定するために、 [**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造の OOB 情報の送信 SA と IPsec ヘッダー情報にハンドルを設定します。

受信パスでは、SA がオフロードされた後、NIC は、ミニポートドライバーが NDIS に報告した機能に一致するすべての受信パケットに対して IPsec 処理を実行する必要があります。 ミニポートドライバーは、 [**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造の OOB 情報に適切なフラグを設定して、NIC が実行する特定のオフロードタスクとそれらの操作の結果を指定します。

IPsecOV2 での送受信処理の詳細については、「 [Ipsec オフロードバージョン2を使用してネットワークデータを送信](sending-network-data-with-ipsec-offload-version-2.md)する」および「 [Ipsec オフロードバージョン2でネットワークデータを受信](receiving-network-data-with-ipsec-offload-version-2.md)する」を参照してください。

 

 





