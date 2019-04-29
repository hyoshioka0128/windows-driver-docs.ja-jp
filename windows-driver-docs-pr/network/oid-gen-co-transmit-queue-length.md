---
title: OID_GEN_CO_TRANSMIT_QUEUE_LENGTH
description: このトピックでは、OID_GEN_CO_TRANSMIT_QUEUE_LENGTH オブジェクト識別子 (OID) について説明します。
ms.assetid: bd99e26d-abd4-4b71-8106-e474f61630ff
keywords:
- OID_GEN_CO_TRANSMIT_QUEUE_LENGTH
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3a9020c9c1032acc979014be6564533c9b89ab3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386236"
---
# <a name="oidgencotransmitqueuelength"></a>OID_GEN_CO_TRANSMIT_QUEUE_LENGTH

OID_GEN_CO_TRANSMIT_QUEUE_LENGTH OID は、Pdu 現在キュー内の数、伝送の NIC であるかどうか、またはドライバーの内部キューを指定します。 返される数は常に Pdu の合計数現在キューに置かれた、要求は、NDIS ライブラリでキューに置かれた未送信の送信が含まれています。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

