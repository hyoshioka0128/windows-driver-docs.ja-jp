---
title: OID_GEN_CO_PROTOCOL_OPTIONS
description: このトピックでは、OID_GEN_CO_PROTOCOL_OPTIONS オブジェクト識別子 (OID) について説明します。
ms.assetid: 5c1212e4-1fd2-435a-ae8c-9f75522cbca6
keywords:
- OID_GEN_CO_PROTOCOL_OPTIONS
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2b3bca6ee5dc9e76646bc1759f472c77d92b2f9
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917494"
---
# <a name="oid_gen_co_protocol_options"></a>OID_GEN_CO_PROTOCOL_OPTIONS

プロトコルドライバーのオプションプロパティを定義するビットマスク。 プロトコルは、そのプロパティを NDIS に通知します。これにより、オプションでこれらを利用できます。 プロトコルドライバーによってバインドにフラグが設定されていない場合、NDIS はすべてが明確であると想定します。

現在、次のフラグが定義されています。

NDIS_PROT_OPTION_ESTIMATED_LENGTH  
パケットが、このプロトコルに対する正確な値ではなく、最悪のパケットサイズの推定で示されることを示します。

NDIS_PROT_OPTION_NO_LOOPBACK  
プロトコルでは、バインディングでのループバックのサポートは必要ありません。

NDIS_PROT_OPTION_NO_RSVD_ON_RCVPKT  
プロトコルは、指定された受信パケットの**Protocolreserved**セクションを使用しません。 これにより、NDIS は複数のプロトコルに対して受信パケットを示すことができます。

## <a name="requirements"></a>要件

**バージョン**: Windows Vista 以降の**ヘッダー**: Ntddndis (Ndis .h を含む)

