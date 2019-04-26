---
title: OID_GEN_CO_MEDIA_SUPPORTED
description: このトピックでは、OID_GEN_CO_MEDIA_SUPPORTED オブジェクト識別子 (OID) について説明します。
ms.assetid: 688d5054-f92d-4054-bf6e-dcf43fcfeb06
keywords:
- OID_GEN_CO_MEDIA_SUPPORTED
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b473639e3788c38c876d7d116da1db5f29b6a97
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348204"
---
# <a name="oidgencomediasupported"></a>OID_GEN_CO_MEDIA_SUPPORTED

メディアの完全な一覧は、次のシステム定義の値の適切なサブセットとして、NIC がサポートを型します。

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
DEC/Intel/Xerox (DIX) イーサネットします。

**NdisMediumArcnetRaw**  
ARCNET (raw)。

**NdisMediumArcnet878_2**  
ARCNET (878.2)。

**NdisMediumWirelessWan**  
NdisWirelessXxx メディアのさまざまな種類。

**NdisMediumAtm**  
ATM します。

**NdisMediumIrda**  
Windows 2000 以降のプラットフォームで将来使用するために予約されています。

## <a name="remarks"></a>注釈

ATM ネットワーク用のドライバーを LAN エミュレーション宣言としてそのメディア**NdisMedium802_3** 、なく**NdisMediumAtm**します。 このようなドライバーは、上位レベルの NDIS ドライバーにイーサネットをエミュレート、ATM フォーラムのレーンに準拠し、UNI 信号方式のサポートを提供します。

ワイヤレス WAN NIC ドライバーはそのメディアの種類としてレポートする必要があります**NdisMediumWirelessWan**します。 ただし、このようなミニポート ドライバーも指定する必要あります**NdisWWDIXEthernetFrames**いずれにもヘッダーの形式には、この形式を選択したプロトコルがバインドされているし、ミニポート ドライバーは、NIC のネイティブのヘッダーの形式も提供できます。 既存の LAN ベースのプロトコルをサポートするには、ドライバー開発者はワイヤレス NIC のネイティブのヘッダーの形式と既存のプロトコルで認識される形式にメディア固有の情報に「変換」する NDIS 中間ドライバーを提供できます。

基になるミニポート ドライバーに返された場合**NULL**このクエリのかどうか、実験的なメディアを使用して、ドライバーを示す必要がありますまたは受信[NdisMCoIndicateReceivePacket](https://msdn.microsoft.com/library/windows/hardware/ff553455)します。


## <a name="requirements"></a>必要条件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

