---
title: ポートの列挙
description: ポートの列挙
ms.assetid: b38c5556-5124-45ea-af2f-4a4cd9313cc7
keywords:
- WDK NDIS をポート NDIS を列挙します。
- WDK の NDIS OID 要求をポートします。
- NDIS ポート WDK、OID 要求
- OID 要求 WDK NDIS ポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77dbf3d94129d784993236f661b26e3dbeb42cd8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354573"
---
# <a name="enumerating-ports"></a>ポートの列挙





NDIS プロトコルおよびフィルター ドライバーを使用できる、 [OID\_GEN\_ENUMERATE\_ポート](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-enumerate-ports)OID のクエリ要求に関連付けられているアクティブな NDIS ポートの特性を決定する、基になるミニポート アダプター。 NDIS が、この OID を処理し、ミニポート ドライバーには、この OID クエリは受け取りません。

NDIS でクエリの結果は、クエリが成功すると、 [ **NDIS\_ポート\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_port_array)構造体。 **NumberOfPorts**の NDIS メンバー\_ポート\_ミニポート アダプターに関連付けられているアクティブなポートの数が配列に含まれています。 **ポート**の NDIS メンバー\_ポート\_配列へのポインターのリストに含まれる[ **NDIS\_ポート\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_port_characteristics)構造体。 各 NDIS\_ポート\_の特性構造が 1 つのポートの特性を定義します。

 

 





