---
title: OID_GEN_CO_TRANSMIT_QUEUE_LENGTH
description: このトピックでは、OID_GEN_CO_TRANSMIT_QUEUE_LENGTH オブジェクト識別子 (OID) について説明します。
ms.assetid: bd99e26d-abd4-4b71-8106-e474f61630ff
keywords:
- OID_GEN_CO_TRANSMIT_QUEUE_LENGTH
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 976b978bb8d69ba95a01e45a1525593a0cf436e4
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917025"
---
# <a name="oid_gen_co_transmit_queue_length"></a>OID_GEN_CO_TRANSMIT_QUEUE_LENGTH

OID_GEN_CO_TRANSMIT_QUEUE_LENGTH OID は、NIC またはドライバー内部キューにあるかどうかにかかわらず、現在転送のためにキューに入れられている Pdu の数を指定します。 返される数は常に、現在キューに置かれている Pdu の総数です。この数には、NDIS ライブラリでキューに登録された未送信の送信要求が含まれます。

## <a name="requirements"></a>要件

**バージョン**: Windows Vista 以降の**ヘッダー**: Ntddndis (Ndis .h を含む)

