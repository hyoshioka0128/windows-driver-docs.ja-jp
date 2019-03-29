---
title: OID_GEN_CO_TRANSMIT_QUEUE_LENGTH
description: このトピックでは、OID_GEN_CO_TRANSMIT_QUEUE_LENGTH オブジェクト識別子 (OID) について説明します。
ms.assetid: bd99e26d-abd4-4b71-8106-e474f61630ff
keywords:
- OID_GEN_CO_TRANSMIT_QUEUE_LENGTH
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3a9020c9c1032acc979014be6564533c9b89ab3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570074"
---
# <a name="oidgencotransmitqueuelength"></a>OID_GEN_CO_TRANSMIT_QUEUE_LENGTH

OID_GEN_CO_TRANSMIT_QUEUE_LENGTH OID は、Pdu 現在キュー内の数、伝送の NIC であるかどうか、またはドライバーの内部キューを指定します。 返される数は常に Pdu の合計数現在キューに置かれた、要求は、NDIS ライブラリでキューに置かれた未送信の送信が含まれています。

## <a name="requirements"></a>必要条件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

