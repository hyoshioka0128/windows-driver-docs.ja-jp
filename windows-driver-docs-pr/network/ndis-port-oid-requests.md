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
ms.openlocfilehash: 2094b4e9744286d3256fcfa41a2617a79ac93b31
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378289"
---
# <a name="ndis-port-oid-requests"></a>NDIS ポート OID 要求





NDIS ドライバーでは、NDIS ポート OID 要求を関連付けることができます。 このような OID 要求で、 **PortNumber**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体は、ターゲット ポート番号に設定されます。 OID 要求が既定のポートの場合、ポート番号は 0 を使用します。 上にあるドライバーは、特定のポート番号を指定する任意の OID 要求を行う前に、ポートがアクティブであることを確認する必要があります。

NDIS を呼び出すと、 [ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)プロトコル ドライバー、NDIS の関数で現在アクティブなすべてのポートの一覧を提供する、 **ActivePorts** のメンバー[**NDIS\_バインド\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff564832)構造体、 *BindParameters*パラメーターを指します。 NDIS は、ポートがアクティブ化し、非アクティブ化されたときに、PnP イベントとプロトコル ドライバーにも通知します。 PnP ポートのアクティブ化と非アクティブ化の通知の詳細については、次を参照してください。 [NDIS ポート PnP 通知の処理](handling-ndis-ports-pnp-event-notifications.md)します。

次の Oid、NDIS ポート インターフェイスに固有のとおりです。

<a href="" id="oid-gen-enumerate-ports"></a>[OID\_GEN\_ENUMERATE\_ポート](https://msdn.microsoft.com/library/windows/hardware/ff569583)  
ミニポート アダプターに関連付けられているアクティブなポートを列挙します。

<a href="" id="oid-gen-port-state"></a>[OID\_GEN\_ポート\_状態](https://msdn.microsoft.com/library/windows/hardware/ff569624)  
現在のリンクと認証ポートの状態を取得します。

<a href="" id="--------oid-gen-port-authentication-parameters"></a>[OID\_GEN\_ポート\_認証\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569623)  
NDIS ポートの現在の認証状態を設定します。

このセクションの内容:

-   [ポートを列挙します。](enumerating-ports.md)
-   [ポートの状態のクエリを実行します。](querying-the-port-state.md)
-   [ポート設定の認証パラメーター](setting-port-authentication-parameters.md)

 

 





