---
title: NDIS ポート OID 要求
description: NDIS ポート OID 要求
ms.assetid: 361f9adf-2bf6-4aa8-b66b-fe9304b14550
keywords:
- ポート WDK NDIS、OID 要求
- NDIS ポート WDK、OID 要求
- OID が WDK NDIS ポートを要求する
- OID 要求に WDK NDIS ポートを関連付ける
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07d5c760c69fc9512fd1740f4bb1f76e850a8e26
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826956"
---
# <a name="ndis-port-oid-requests"></a>NDIS ポート OID 要求





NDIS ドライバーは、OID 要求を NDIS ポートに関連付けることができます。 このような OID 要求では、 [**NDIS\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造のポート**ポート**メンバーは、ターゲットポート番号に設定されます。 OID 要求が既定のポートに対するものである場合、ポート番号は0です。 このドライバーは、特定のポート番号を指定する OID 要求を行う前に、ポートがアクティブであることを確認する必要があります。

NDIS がプロトコルドライバーの[*Protocolbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)関数を呼び出すと、ndis は、 [**NDIS\_\_BIND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)の**activeports**メンバー内の現在アクティブなすべてのポートの一覧を提供します *。BindParameters*パラメーターはを指します。 また、ポートがアクティブ化され、非アクティブ化されると、プロトコルドライバーに PnP イベントが通知されます。 PnP ポートのアクティブ化と非アクティブ化の通知の詳細については、「 [NDIS ポートの Pnp 通知の処理](handling-ndis-ports-pnp-event-notifications.md)」を参照してください。

次の Oid は、NDIS ポートインターフェイスに固有のものです。

<a href="" id="oid-gen-enumerate-ports"></a>[OID\_GEN\_\_ポートの列挙](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-enumerate-ports)  
ミニポートアダプターに関連付けられているアクティブなポートを列挙します。

<a href="" id="oid-gen-port-state"></a>[OID\_GEN\_ポート\_の状態](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-port-state)  
現在のリンクおよび認証ポートの状態を取得します。

<a href="" id="--------oid-gen-port-authentication-parameters"></a>[OID\_GEN\_ポート\_認証\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-port-authentication-parameters)  
NDIS ポートの現在の認証状態を設定します。

このセクションの内容:

-   [ポートの列挙](enumerating-ports.md)
-   [ポートの状態を照会する](querying-the-port-state.md)
-   [ポート認証パラメーターの設定](setting-port-authentication-parameters.md)

 

 





