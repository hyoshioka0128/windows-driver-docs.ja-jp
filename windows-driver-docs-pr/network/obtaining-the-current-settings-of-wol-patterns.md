---
title: WOL パターンの現在の設定の取得
description: WOL パターンの現在の設定の取得
ms.assetid: 113ea75a-83d8-41aa-b61c-711ef90bccca
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b83554a74910baa8935810cdc5cb757687026074
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837739"
---
# <a name="obtaining-the-current-settings-of-wol-patterns"></a>WOL パターンの現在の設定の取得





これまでのドライバーでは、 [oid\_PM\_WOL\_PATTERN\_LIST](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-wol-pattern-list) oid クエリ要求を使用して、基になるネットワークアダプターに設定されている WAKE on LAN (WOL) パターンを列挙できます。 クエリから正常に戻った後、 [**ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、 [**NDIS\_PM\_\_WOL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)のリストへのポインターが含まれています。現在追加されている WOL パターン。 **NDIS\_PM\_WOL\_パターン**構造の内容については、「 [Wake on LAN パターンの追加と削除](adding-and-deleting-wake-on-lan-patterns.md)」を参照してください。

NDIS は、ミニポートドライバーに代わって oid 要求を一覧表示し\_oid\_PM\_WOL\_パターンを処理します。 そのため、NDIS ミニポートドライバーは、oid\_PM\_WOL\_PATTERN\_LIST OID 要求をサポートするために必要ありません。

 

 





