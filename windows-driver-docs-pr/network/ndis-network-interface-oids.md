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
ms.openlocfilehash: 6d2a026cb2a86460b506fd55c0ca4036d6cb4641
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378344"
---
# <a name="ndis-network-interface-oids"></a>NDIS ネットワーク インターフェイス OID

NDIS ネットワーク インターフェイスのオブジェクト識別子 (Oid) は、MIB をサポートするネットワーク インターフェイスに関する情報を提供 ([RFC 2863](overview-of-ndis-network-interfaces.md))。

NDIS インターフェイス プロバイダーでは、これらの Oid をサポートする必要があります。 プロバイダーの登録済みのインターフェイスのないドライバーをする必要があります、このセクションでは、Oid をサポートしていません。

NDIS 呼び出し、 [ProviderQueryObject](https://msdn.microsoft.com/library/windows/hardware/ff570399)インターフェイス プロバイダーからの情報のクエリ要求を作成する関数。 *ObjectId*この関数のパラメーターには、オブジェクト識別子が含まれています。 インターフェイスのプロバイダーが登録されている*ProviderQueryObject*呼び出されたときに、 [NdisIfRegisterProvider](https://msdn.microsoft.com/library/windows/hardware/ff562716)インターフェイス プロバイダーとして登録します。

ハンドル、 *ProviderIfContext*のパラメーター、 *ProviderQueryObject*関数は、ネットワーク インターフェイスを識別します。 このハンドルが NDIS インターフェイス プロバイダーに呼び出されたときに提供された、 [NdisIfRegisterInterface](https://msdn.microsoft.com/library/windows/hardware/ff562715)インターフェイスを登録する関数。 *POutputBuffer*のパラメーター、 *ProviderQueryObject*関数には OID 要求の結果が含まれています。

ネットワーク インターフェイスの Oid の NDIS の詳細についてを参照してください[NDIS 6.0 のネットワーク インターフェイス](ndis-network-interfaces2.md)します。

このセクションには、次の NDIS ネットワーク インターフェイスの Oid がについて説明します。

- [OID_GEN_ALIAS](https://msdn.microsoft.com/library/windows/hardware/ff569438) 
- [OID_GEN_ADMIN_STATUS](https://msdn.microsoft.com/library/windows/hardware/ff569437) 
- [OID_GEN_OPERATIONAL_STATUS](https://msdn.microsoft.com/library/windows/hardware/ff569619) 
- [OID_GEN_PROMISCUOUS_MODE](https://msdn.microsoft.com/library/windows/hardware/ff569625) 
- [OID_GEN_XMIT_LINK_SPEED](https://msdn.microsoft.com/library/windows/hardware/ff569655) 
- [OID_GEN_RCV_LINK_SPEED](https://msdn.microsoft.com/library/windows/hardware/ff569630) 
- [OID_GEN_UNKNOWN_PROTOS](https://msdn.microsoft.com/library/windows/hardware/ff569648) 
- [OID_GEN_DISCONTINUITY_TIME](https://msdn.microsoft.com/library/windows/hardware/ff569581) 
- [OID_GEN_LAST_CHANGE](https://msdn.microsoft.com/library/windows/hardware/ff569591) 
- [OID_GEN_INTERFACE_INFO](https://msdn.microsoft.com/library/windows/hardware/ff569589) 
- [OID_GEN_MEDIA_CONNECT_STATUS_EX](https://msdn.microsoft.com/library/windows/hardware/ff569605) 
- [OID_GEN_LINK_SPEED_EX](https://msdn.microsoft.com/library/windows/hardware/ff569594) 
- [OID_GEN_MEDIA_DUPLEX_STATE](https://msdn.microsoft.com/library/windows/hardware/ff569606) 
- [OID_TUNNEL_INTERFACE_RELEASE_OID](https://msdn.microsoft.com/library/windows/hardware/dn155803) 
- [OID_TUNNEL_INTERFACE_SET_OID](https://msdn.microsoft.com/library/windows/hardware/dn155804) 


