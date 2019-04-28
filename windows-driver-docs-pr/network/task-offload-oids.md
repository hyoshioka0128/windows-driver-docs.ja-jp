---
title: タスク オフロード OID
description: このトピックでは、タスクのオフロード Oid をについて説明します
ms.assetid: 0d7eab31-d5c9-4264-9598-c72e19e1d86b
keywords:
- タスクのオフロード Oid、タスク オフロード NDIS Oid、タスク オフロード Oid WDK、タスクは、ネットワークの Oid をオフロード
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53088e50e0d771d1bf79add695b07547e5c5a5fa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368218"
---
# <a name="task-offload-oids"></a>タスク オフロード OID

次の表では、TCP/IP タスク オフロードの操作をサポートする Oid をまとめたものです。 このような操作に関する詳細については、次を参照してください[TCP/IP タスク オフロード](task-offload.md).-ndis-status-dot11-wfd-group-operating-channel.md。

次の表では、M は、OID は必須では、O は、これは省略可能なことを示しますを示します。

| 長さ | クエリ | Set | 名前 |
| --- | --- | --- | --- |
| arr |   | M | [OID_TCP_TASK_IPSEC_ADD_SA](oid-tcp-task-ipsec-add-sa.md) |
| arr |   | M | [OID_TCP_TASK_IPSEC_ADD_UDPESP_SA](oid-tcp-task-ipsec-add-udpesp-sa.md) |
| 4 |   | M | [OID_TCP_TASK_IPSEC_DELETE_SA](oid-tcp-task-ipsec-delete-sa.md) |
| 4 |   | M | [OID_TCP_TASK_IPSEC_DELETE_UDPESP_SA](oid-tcp-task-ipsec-delete-udpesp-sa.md) |
| arr | M | M | [OID_TCP_TASK_OFFLOAD](oid-tcp-task-offload.md) |

