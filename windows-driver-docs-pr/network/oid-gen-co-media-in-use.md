---
title: OID_GEN_CO_MEDIA_IN_USE
description: このトピックでは、OID_GEN_CO_MEDIA_IN_USE オブジェクト識別子 (OID) について説明します。
ms.assetid: 59a2c981-87a5-4df9-af26-3c5a5eadc17a
keywords:
- OID_GEN_CO_MEDIA_IN_USE
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: afbeba2a2f20c972aafccf298158956d27291e47
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916900"
---
# <a name="oid_gen_co_media_in_use"></a>OID_GEN_CO_MEDIA_IN_USE

NIC で現在サポートされているメディアの種類の完全な一覧。一部として定義されていません (NULL フィルターとも呼ばれます)。または、次のすべてが対象となります。

**NdisMedium802_3**  
イーサネット (802.3)。

**NdisMedium802_5**  
トークンリング (802.5)。

**NdisMediumFddi**  
FDDI.

**NdisMediumWan**  
WAN.

**NdisMediumLocalTalk**  
LocalTalk.

**NdisMediumDix**  
DIX.

**NdisMediumArcnetRaw**  
ARCNET (raw)。

**NdisMediumArcnet878_2**  
ARCNET (878.2)。

**NdisMediumWirelessWan**  
さまざまな種類の NdisWirelessXxx メディア。

**NdisMediumAtm**  
ATM.

基になるミニポートドライバーがこのクエリに対して**NULL**を返した場合、または実験的なメディアの種類が使用されている場合は、ドライバーで Receive with [NdisMCoIndicateReceivePacket](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff553455(v=vs.85))を指定する必要があります。


## <a name="requirements"></a>要件

**バージョン**: Windows Vista 以降の**ヘッダー**: Ntddndis (Ndis .h を含む)

