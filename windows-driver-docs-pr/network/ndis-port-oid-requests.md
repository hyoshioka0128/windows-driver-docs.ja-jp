---
title: NDIS ポート OID 要求
description: NDIS ポート OID 要求
ms.assetid: 361f9adf-2bf6-4aa8-b66b-fe9304b14550
keywords:
- WDK の NDIS OID 要求をポートします。
- NDIS ポート WDK、OID 要求
- OID 要求 WDK NDIS ポート
- WDK NDIS ポートを要求する OID を関連付ける
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e5ffeb2846784540f5d5ff2fd70be73e6b0d68a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354959"
---
# <a name="ndis-port-oid-requests"></a>NDIS ポート OID 要求





NDIS ドライバーでは、NDIS ポート OID 要求を関連付けることができます。 このような OID 要求で、 **PortNumber**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体は、ターゲット ポート番号に設定されます。 OID 要求が既定のポートの場合、ポート番号は 0 を使用します。 上にあるドライバーは、特定のポート番号を指定する任意の OID 要求を行う前に、ポートがアクティブであることを確認する必要があります。

NDIS を呼び出すと、 [ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)プロトコル ドライバー、NDIS の関数で現在アクティブなすべてのポートの一覧を提供する、 **ActivePorts** のメンバー[**NDIS\_バインド\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)構造体、 *BindParameters*パラメーターを指します。 NDIS は、ポートがアクティブ化し、非アクティブ化されたときに、PnP イベントとプロトコル ドライバーにも通知します。 PnP ポートのアクティブ化と非アクティブ化の通知の詳細については、次を参照してください。 [NDIS ポート PnP 通知の処理](handling-ndis-ports-pnp-event-notifications.md)します。

次の Oid、NDIS ポート インターフェイスに固有のとおりです。

<a href="" id="oid-gen-enumerate-ports"></a>[OID\_GEN\_ENUMERATE\_ポート](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-enumerate-ports)  
ミニポート アダプターに関連付けられているアクティブなポートを列挙します。

<a href="" id="oid-gen-port-state"></a>[OID\_GEN\_ポート\_状態](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-port-state)  
現在のリンクと認証ポートの状態を取得します。

<a href="" id="--------oid-gen-port-authentication-parameters"></a>[OID\_GEN\_ポート\_認証\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-port-authentication-parameters)  
NDIS ポートの現在の認証状態を設定します。

このセクションの内容:

-   [ポートを列挙します。](enumerating-ports.md)
-   [ポートの状態のクエリを実行します。](querying-the-port-state.md)
-   [ポート設定の認証パラメーター](setting-port-authentication-parameters.md)

 

 





