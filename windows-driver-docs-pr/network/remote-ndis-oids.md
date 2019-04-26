---
title: リモート NDIS OID
description: リモート NDIS OID
ms.assetid: c97592e8-f395-475e-8e6c-6366d1605075
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2cd4b9d252b537c96160a390220b8245d8ba92bc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350841"
---
# <a name="remote-ndis-oids"></a>リモート NDIS OID





このセクションでは、リモートの NDIS イーサネット デバイスの必須およびオプションの NDIS Oid が一覧表示します。 一覧は考慮 NDIS リモート デバイスと、リモートの NDIS ミニポート ドライバーの一意のプロパティ リストが、通常の NDIS コネクションレス ミニポート ドライバーをサポートするリストと同じではないためです。 いくつかの Oid は、どちらも*設定*と*クエリ*Oid は、両方と必須の OID が定義されているかどうかは、両方のリモートの NDIS デバイスによってサポートされる必要があります[リモート\_NDIS\_設定\_MSG](remote-ndis-set-msg.md)と[リモート\_NDIS\_クエリ\_MSG](remote-ndis-query-msg.md)します。 Oid の詳細については、Microsoft Windows ドライバー開発キット (DDK) を参照してください。

次のリモートの NDIS Oid の一覧に分割されます 2 つのグループ - 一般的な OID と 802.3 特定の OID。 さらに、各グループには、OID クエリの統計情報のサブセクションが含まれています。 [全般] の Oid は、任意のネットワーク デバイスの必要があります。

-   [一般的な Oid](general-oids2.md)
-   [一般的な統計の Oid](general-statistic-oids.md)
-   [802.3 Oid](802-3-oids.md)
-   [802.3 統計 Oid](802-3-statistic-oids.md)
-   [省略可能な電源管理の Oid](optional-power-management-oids.md)
-   [省略可能なネットワークのスリープ解除 Oid](optional-network-wake-up-oids.md)

 

 





