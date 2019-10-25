---
title: NDIS ネットワーク インターフェイス OID
description: このセクションでは、すべての NDIS ドライバーのネットワークインターフェイス Oid について説明します。
keywords:
- NDIS ネットワーク インターフェイス OID
- WDK NDIS ネットワークインターフェイス Oid
- WDK ネットワークインターフェイス Oid
ms.assetid: A66B5AC6-9EAF-4234-8614-0EBF179B3DDE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c64435cb711e73954592ae619b74cdb588b81439
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844361"
---
# <a name="ndis-network-interface-oids"></a>NDIS ネットワーク インターフェイス OID

NDIS ネットワークインターフェイスオブジェクト識別子 (Oid) は、MIB ([RFC 2863](overview-of-ndis-network-interfaces.md)) をサポートするネットワークインターフェイスに関する情報を提供します。

NDIS インターフェイスプロバイダーは、これらの Oid をサポートする必要があります。 登録されていないインターフェイスプロバイダーではないドライバーは、このセクションの Oid をサポートしていません。

NDIS は、 [Providerqueryobject](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-if_query_object)関数を呼び出して、インターフェイスプロバイダーからの情報のクエリ要求を行います。 この関数の*ObjectId*パラメーターには、オブジェクト識別子が含まれています。 インターフェイスプロバイダーは、インターフェイスプロバイダーとして登録するために[NdisIfRegisterProvider](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifregisterprovider)関数を呼び出したときに*providerqueryobject*を登録しました。

*Providerqueryobject*関数の*ProviderIfContext*パラメーターにあるハンドルは、ネットワークインターフェイスを識別します。 このハンドルは、インターフェイスプロバイダーがインターフェイスを登録するために[NdisIfRegisterInterface](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifregisterinterface)関数を呼び出したときに NDIS に提供されました。 *Providerqueryobject*関数の*poutputbuffer*パラメーターには、OID 要求の結果が含まれています。

NDIS ネットワークインターフェイス Oid の詳細については、「 [ndis 6.0 ネットワークインターフェイス](ndis-network-interfaces2.md)」を参照してください。

このセクションでは、次の NDIS ネットワークインターフェイス Oid について説明します。

- [OID_GEN_ALIAS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-alias) 
- [OID_GEN_ADMIN_STATUS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-admin-status) 
- [OID_GEN_OPERATIONAL_STATUS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-operational-status) 
- [OID_GEN_PROMISCUOUS_MODE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-promiscuous-mode) 
- [OID_GEN_XMIT_LINK_SPEED](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-xmit-link-speed) 
- [OID_GEN_RCV_LINK_SPEED](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-link-speed) 
- [OID_GEN_UNKNOWN_PROTOS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-unknown-protos) 
- [OID_GEN_DISCONTINUITY_TIME](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-discontinuity-time) 
- [OID_GEN_LAST_CHANGE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-last-change) 
- [OID_GEN_INTERFACE_INFO](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-interface-info) 
- [OID_GEN_MEDIA_CONNECT_STATUS_EX](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-media-connect-status-ex) 
- [OID_GEN_LINK_SPEED_EX](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-link-speed-ex) 
- [OID_GEN_MEDIA_DUPLEX_STATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-media-duplex-state) 
- [OID_TUNNEL_INTERFACE_RELEASE_OID](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tunnel-interface-release-oid) 
- [OID_TUNNEL_INTERFACE_SET_OID](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tunnel-interface-set-oid) 


