---
title: ポートの列挙
description: ポートの列挙
ms.assetid: b38c5556-5124-45ea-af2f-4a4cd9313cc7
keywords:
- NDIS ポート WDK NDIS を列挙しています
- ポート WDK NDIS、OID 要求
- NDIS ポート WDK、OID 要求
- OID が WDK NDIS ポートを要求する
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95cb831fe209a4b3c6e2979afc57daa7cdc355db
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834769"
---
# <a name="enumerating-ports"></a>ポートの列挙





NDIS プロトコルドライバーとフィルタードライバーは、 [oid\_GEN\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-enumerate-ports)使用して\_ポート oid クエリ要求を列挙し、基になるミニポートアダプターに関連付けられているアクティブな NDIS ポートの特性を判断できます。 NDIS はこの OID を処理し、ミニポートドライバーはこの OID クエリを受信しません。

クエリが成功した場合、NDIS は、 [**ndis\_ポート\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_array)構造にクエリの結果を提供します。 NDIS\_PORT\_ARRAY の**Numberofports**メンバーには、ミニポートアダプターに関連付けられているアクティブなポートの数が含まれています。 NDIS\_PORT\_ARRAY の**Ports**メンバーには、 [**ndis\_ポート\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_characteristics)構造へのポインターの一覧が含まれています。 各 NDIS\_ポート\_特性構造では、1つのポートの特性を定義します。

 

 





