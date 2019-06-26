---
title: OID_GEN_CO_MEDIA_IN_USE
description: このトピックでは、OID_GEN_CO_MEDIA_IN_USE オブジェクト識別子 (OID) について説明します。
ms.assetid: 59a2c981-87a5-4df9-af26-3c5a5eadc17a
keywords:
- OID_GEN_CO_MEDIA_IN_USE
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2eb974aeb0ff8cb421077c3122d60069e5f19509
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361181"
---
# <a name="oidgencomediainuse"></a>OID_GEN_CO_MEDIA_IN_USE

NIC がサポートされているメディアの種類の完全な一覧は、いくつか、(NULL のフィルターとも呼ばれます)、none または、次のすべてのとして定義。

**NdisMedium802_3**  
イーサネット (802.3)。

**NdisMedium802_5**  
トークン リング (802.5)。

**NdisMediumFddi**  
FDDI します。

**NdisMediumWan**  
WAN します。

**NdisMediumLocalTalk**  
LocalTalk します。

**NdisMediumDix**  
DIX します。

**NdisMediumArcnetRaw**  
ARCNET (raw)。

**NdisMediumArcnet878_2**  
ARCNET (878.2)。

**NdisMediumWirelessWan**  
NdisWirelessXxx メディアのさまざまな種類。

**NdisMediumAtm**  
ATM します。

基になるミニポート ドライバーに返された場合**NULL**このクエリのかどうか、実験的なメディアを使用して、ドライバーを示す必要がありますまたは受信[NdisMCoIndicateReceivePacket](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff553455(v=vs.85))します。


## <a name="requirements"></a>必要条件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

