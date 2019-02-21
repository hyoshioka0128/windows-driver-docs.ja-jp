---
title: リモートの NDIS デバイスの制御
description: リモートの NDIS デバイスの制御
ms.assetid: 52096845-57ee-4da5-95c7-ceae00e8159d
keywords:
- リモートの NDIS WDK のネットワーク、デバイスの制御
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be646203a1e9ad77327101d5959c3ef6d1295dbd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553951"
---
# <a name="remote-ndis-device-control"></a>リモートの NDIS デバイスの制御





リモート ホストで使用されて\_NDIS\_クエリ\_MSG とリモート\_NDIS\_設定\_NDIS リモート デバイスの操作を制御するメッセージ。 NDIS オブジェクト ID (OID) は、デバイスの運用パラメーターまたは統計カウンターを識別するために、このような各メッセージで使用されます。 リスト[リモート NDIS Oid](remote-ndis-oids.md)は 2 つのグループに分割されます:*全般 OID*と*802.3 に固有の OID*します。 さらに、各グループには、OID クエリの統計情報のサブセクションが含まれています。 [全般] の Oid は、任意のネットワーク デバイスの必要があります。

 

 





