---
title: イーサネットの統計情報の Oid
description: このトピックでは、イーサネットの統計情報の Oid をについて説明します
ms.assetid: b38ec79d-d8f3-46fa-9e6f-d42fa18f467c
keywords:
- イーサネットの統計 Oid、ネットワー キング イーサネット NDIS Oid、Oid WDK のイーサネット、イーサネット Oid
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15ca916da71bc065f6110428ed0606807ff817a2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550316"
---
# <a name="ethernet-statistics-oids"></a>イーサネットの統計情報の Oid

次の表は、ネットワーク インターフェイス コント ローラー (Nic) のイーサネットの統計情報を取得するために使用する Oid をまとめたものです。

| 長さ | クエリ | 設定 | 名前 |
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

