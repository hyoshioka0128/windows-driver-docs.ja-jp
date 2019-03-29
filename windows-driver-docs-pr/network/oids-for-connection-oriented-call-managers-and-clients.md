---
title: 接続指向コール マネージャーおよびクライアントの OID
description: このトピックでは、接続指向のコール マネージャーとクライアントの Oid をについて説明します。
ms.assetid: a2ffbfd4-a63e-41d1-ab57-0c23661148ca
keywords:
- 接続指向コール マネージャーおよびクライアントの OID
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b0dad3bd79b415aaf73248d1a8d5717557972a1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581819"
---
# <a name="oids-for-connection-oriented-call-managers-and-clients"></a>接続指向コール マネージャーおよびクライアントの OID

次の表は、クライアントの接続指向マネージャーの呼び出しを送信できるまたは MCM ドライバーとその呼び出しマネージャーまたは MCM ドライバーは接続指向のクライアントに送信できます Oid をまとめたものです。 

次の表では、M は、OID は必須では、O は、これは省略可能なことを示しますを示します。

| 長さ | Query | Set | 名前 |
| --- | --- | --- | --- |
| 不定 |   | O | [OID_CO_ADD_ADDRESS](oid-co-add-address.md) |
| 不定 |   | O | [OID_CO_ADD_PVC](oid-co-add-pvc.md) |
| 0 |   | O | [OID_CO_ADDRESS_CHANGE](oid-co-address-change.md) |
| 0 |   | M | [OID_CO_AF_CLOSE](oid-co-af-close.md) |
| 不定 |   | O | [OID_CO_DELETE_ADDRESS](oid-co-delete-address.md) |
| 不定 |   | O | [OID_CO_DELETE_PVC](oid-co-delete-pvc.md) |
| 不定 | O |   | [OID_CO_GET_ADDRESSES](oid-co-get-addresses.md) |
|   |   |   | [OID_CO_GET_CALL_INFORMATION](oid-co-get-call-information.md) |
| 0 |   | O | [OID_CO_SIGNALING_DISABLED](oid-co-signaling-disabled.md) |
| 0 |   | O | [OID_CO_SIGNALING_ENABLED](oid-co-signaling-enabled.md) |

