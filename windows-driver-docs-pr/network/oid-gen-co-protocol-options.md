---
title: OID_GEN_CO_PROTOCOL_OPTIONS
description: このトピックでは、OID_GEN_CO_PROTOCOL_OPTIONS オブジェクト識別子 (OID) について説明します。
ms.assetid: 5c1212e4-1fd2-435a-ae8c-9f75522cbca6
keywords:
- OID_GEN_CO_PROTOCOL_OPTIONS
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0d0698b891872e151876486579c5be7b470bd7a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355721"
---
# <a name="oidgencoprotocoloptions"></a>OID_GEN_CO_PROTOCOL_OPTIONS

プロトコル ドライバーの省略可能なプロパティを定義するビットマスク。 プロトコルは、これらのオプションで利用できますが、そのプロパティの NDIS を通知します。 プロトコル ドライバーがバインディングでそのフラグを設定しない場合、NDIS すべてクリアが前提としています。

次のフラグは現在定義されています。

NDIS_PROT_OPTION_ESTIMATED_LENGTH  
このプロトコルには正確な値ではなく、パケット サイズの最悪の場合の推定値でパケットを示すことができますを示します。

NDIS_PROT_OPTION_NO_LOOPBACK  
プロトコルでは、バインディングでループバックのサポートは必要ありません。

NDIS_PROT_OPTION_NO_RSVD_ON_RCVPKT  
プロトコルが使用しない、 **ProtocolReserved**のセクションに示されるパケットを受信します。 これにより、受信パケットを 1 つ以上のプロトコルを示す NDIS できます。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

