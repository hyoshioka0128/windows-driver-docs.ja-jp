---
title: WOL パターンの現在の設定の取得
description: WOL パターンの現在の設定の取得
ms.assetid: 113ea75a-83d8-41aa-b61c-711ef90bccca
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 786d78e032a2333c9d02e148e3674813ac6aec29
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354505"
---
# <a name="obtaining-the-current-settings-of-wol-patterns"></a>WOL パターンの現在の設定の取得





後続のドライバーを使用できます、 [OID\_PM\_WOL\_パターン\_一覧](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-wol-pattern-list)基になるネットワーク アダプターに設定されている wake on LAN (WOL) パターンを列挙するためのクエリ要求の OID。 で、クエリから正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造に含まれる、一覧へのポインター [ **NDIS\_PM\_WOL\_パターン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)現在追加 WOL パターンを記述する構造体。 内容については、 **NDIS\_PM\_WOL\_パターン**構造体は、「[の追加と削除 Wake on LAN パターン](adding-and-deleting-wake-on-lan-patterns.md)します。

NDIS 処理 OID\_PM\_WOL\_パターン\_一覧 OID がミニポート ドライバーに代わって要求。 そのため、NDIS ミニポート ドライバーは、OID をサポートする必要はありません\_PM\_WOL\_パターン\_一覧 OID 要求。

 

 





