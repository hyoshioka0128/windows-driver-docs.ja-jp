---
title: ポート状態のクエリ
description: ポート状態のクエリ
ms.assetid: 3659d99b-1bbd-453c-8a56-b968d1748c1f
keywords:
- ポートの状態が WDK NDIS
- NDIS ポートの状態のクエリを実行します。
- WDK の NDIS OID 要求をポートします。
- NDIS ポート WDK、OID 要求
- OID 要求 WDK NDIS ポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6559d86cad14f7a569e96ae747dabd2ae9a12ccb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377025"
---
# <a name="querying-the-port-state"></a>ポート状態のクエリ





ドライバーのスライドを発行できます、 [OID\_GEN\_ポート\_状態](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-port-state)OID のクエリ要求で指定されているポートの現在の状態を取得する、 **PortNumber**メンバー[ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体。 NDIS が、この OID を処理し、ミニポート ドライバーには、この OID クエリは受け取りません。 NDIS 受信ポートの状態情報で、 [ **NDIS\_ポート\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_port_characteristics)構造体。

OID\_GEN\_ポート\_状態 OID が NDIS 6.0 以降でサポートされています。

OID を使用しないようにドライバーを重なって\_GEN\_ポート\_可能な場合の状態にあり、代わりに依存する必要があります、 [ **NDIS\_状態\_ポート\_状態** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-port-state)状態を示す値。 ポートに関連する状態インジケーターの詳細については、次を参照してください。 [NDIS ポートの状態インジケーターの処理](handling-ndis-ports-status-indications.md)します。

場合、OID\_GEN\_ポート\_状態クエリが成功すると、NDIS には、ポートの状態情報が返されます、 [ **NDIS\_ポート\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_port_state)構造体。

 

 





