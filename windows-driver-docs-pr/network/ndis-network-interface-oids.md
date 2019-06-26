---
title: NDIS ネットワーク インターフェイス OID
description: このセクションには、すべての NDIS ドライバー用のネットワーク インターフェイスの Oid がについて説明します
keywords:
- NDIS ネットワーク インターフェイス OID
- ネットワーク インターフェイスの WDK NDIS Oid
- WDK のネットワーク インターフェイスの Oid
ms.assetid: A66B5AC6-9EAF-4234-8614-0EBF179B3DDE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d43d086e381f0eb4ecbaae1d4825a33ad316b1b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354981"
---
# <a name="ndis-network-interface-oids"></a>NDIS ネットワーク インターフェイス OID

NDIS ネットワーク インターフェイスのオブジェクト識別子 (Oid) は、MIB をサポートするネットワーク インターフェイスに関する情報を提供 ([RFC 2863](overview-of-ndis-network-interfaces.md))。

NDIS インターフェイス プロバイダーでは、これらの Oid をサポートする必要があります。 プロバイダーの登録済みのインターフェイスのないドライバーをする必要があります、このセクションでは、Oid をサポートしていません。

NDIS 呼び出し、 [ProviderQueryObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-if_query_object)インターフェイス プロバイダーからの情報のクエリ要求を作成する関数。 *ObjectId*この関数のパラメーターには、オブジェクト識別子が含まれています。 インターフェイスのプロバイダーが登録されている*ProviderQueryObject*呼び出されたときに、 [NdisIfRegisterProvider](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifregisterprovider)インターフェイス プロバイダーとして登録します。

ハンドル、 *ProviderIfContext*のパラメーター、 *ProviderQueryObject*関数は、ネットワーク インターフェイスを識別します。 このハンドルが NDIS インターフェイス プロバイダーに呼び出されたときに提供された、 [NdisIfRegisterInterface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifregisterinterface)インターフェイスを登録する関数。 *POutputBuffer*のパラメーター、 *ProviderQueryObject*関数には OID 要求の結果が含まれています。

ネットワーク インターフェイスの Oid の NDIS の詳細についてを参照してください[NDIS 6.0 のネットワーク インターフェイス](ndis-network-interfaces2.md)します。

このセクションには、次の NDIS ネットワーク インターフェイスの Oid がについて説明します。

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


