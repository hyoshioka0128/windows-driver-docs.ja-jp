---
title: イーサネット統計情報 OID
description: このトピックでは、イーサネットの統計情報の Oid をについて説明します
ms.assetid: b38ec79d-d8f3-46fa-9e6f-d42fa18f467c
keywords:
- イーサネットの統計 Oid、ネットワー キング イーサネット NDIS Oid、Oid WDK のイーサネット、イーサネット Oid
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15ca916da71bc065f6110428ed0606807ff817a2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368316"
---
# <a name="ethernet-statistics-oids"></a>イーサネット統計情報 OID

次の表は、ネットワーク インターフェイス コント ローラー (Nic) のイーサネットの統計情報を取得するために使用する Oid をまとめたものです。

| 長さ | クエリ | Set | 名前 |
| --- | --- | --- | --- |
| 4 | O |   | [OID_802_3_RCV_OVERRUN](oid-802-3-rcv-overrun.md) |
| 4 | O |   | [OID_802_3_XMIT_DEFERRED](oid-802-3-xmit-deferred.md) |
| 4 | O |   | [OID_802_3_XMIT_HEARTBEAT_FAILURE](oid-802-3-xmit-heartbeat-failure.md) |
| 4 | O |   | [OID_802_3_XMIT_LATE_COLLISIONS](oid-802-3-xmit-late-collisions.md) |
| 4 | O |   | [OID_802_3_XMIT_MAX_COLLISIONS](oid-802-3-xmit-max-collisions.md) |
| 4 | O |   | [OID_802_3_XMIT_TIMES_CRS_LOST](oid-802-3-xmit-times-crs-lost.md) |
| 4 | O |   | [OID_802_3_XMIT_UNDERRUN](oid-802-3-xmit-underrun.md) |

> [!NOTE]
> 次の Oid は、NDIS 6.0 では古い以降です。
> - OID_802_3_RCV_ERROR_ALIGNMENT
> - OID_802_3_XMIT_MORE_COLLISIONS
> - OID_802_3_XMIT_ONE_COLLISION

