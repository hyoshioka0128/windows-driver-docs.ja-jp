---
title: ポート状態のクエリ
description: ポート状態のクエリ
ms.assetid: 3659d99b-1bbd-453c-8a56-b968d1748c1f
keywords:
- ポートの状態 WDK NDIS
- NDIS ポートの状態の照会
- ポート WDK NDIS、OID 要求
- NDIS ポート WDK、OID 要求
- OID が WDK NDIS ポートを要求する
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ccb894eda118b71b33ca678bfadafe555e2df4e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844865"
---
# <a name="querying-the-port-state"></a>ポート状態のクエリ





それまでのドライバーは[oid\_GEN\_port\_STATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-port-state) oid クエリ要求を発行して、 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造のポート**番号メンバーに**指定されているポートの現在の状態を取得できます。 NDIS はこの OID を処理し、ミニポートドライバーはこの OID クエリを受信しません。 NDIS は、 [**ndis\_ポート\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_characteristics)の構造でポートの状態情報を受信します。

OID\_GEN\_PORT\_STATE OID は、NDIS 6.0 以降のバージョンでサポートされています。

それ以降のドライバーでは、可能な場合は\_ポート\_状態の OID\_GEN を使用しないでください。代わりに、 [**NDIS\_ステータス\_ポート\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-port-state)の状態の表示に依存する必要があります。 ポート関連のステータス表示の詳細については、「 [NDIS ポートの状態](handling-ndis-ports-status-indications.md)の表示を処理する」を参照してください。

OID\_GEN\_PORT\_状態クエリが成功した場合、NDIS は[**ndis\_ポート\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_state)構造でポートの状態情報を返します。

 

 





