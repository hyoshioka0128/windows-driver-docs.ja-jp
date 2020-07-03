---
title: OID_GEN_CO_MEDIA_SUPPORTED
description: このトピックでは、OID_GEN_CO_MEDIA_SUPPORTED オブジェクト識別子 (OID) について説明します。
ms.assetid: 688d5054-f92d-4054-bf6e-dcf43fcfeb06
keywords:
- OID_GEN_CO_MEDIA_SUPPORTED
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96f92e6110d3b2a3a4d0b51041cb24c1ded7c883
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917916"
---
# <a name="oid_gen_co_media_supported"></a>OID_GEN_CO_MEDIA_SUPPORTED

次のシステム定義の値の適切なサブセットとして、NIC がサポートするメディアの種類の完全な一覧。

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
DEC/Intel/Xerox (DIX) イーサネット。

**NdisMediumArcnetRaw**  
ARCNET (raw)。

**NdisMediumArcnet878_2**  
ARCNET (878.2)。

**NdisMediumWirelessWan**  
さまざまな種類の NdisWirelessXxx メディア。

**NdisMediumAtm**  
ATM.

**NdisMediumIrda**  
Windows 2000 以降のプラットフォームで今後使用するために予約されています。

## <a name="remarks"></a>注釈

ATM ネットワーク用の LAN エミュレーションドライバーは、メディアを**NdisMediumAtm**ではなく、 **NdisMedium802_3**として宣言します。 このようなドライバーは、イーサネットを高レベルの NDIS ドライバーにエミュレートし、ATM フォーラムの LANE に準拠し、UNI シグナリングのサポートを提供します。

ワイヤレス WAN NIC ドライバーは、メディアの種類を**NdisMediumWirelessWan**として報告する必要があります。 ただし、このようなミニポートドライバーは、この形式を選択する任意のバインドされたプロトコルに**NdisWWDIXEthernetFrames** header 形式を提供する必要があります。また、ミニポートドライバーも、NIC のネイティブヘッダー形式を提供できます。 既存の LAN ベースのプロトコルをサポートするために、ドライバーライターは、ワイヤレス NIC のネイティブヘッダー形式と中程度の情報を既存のプロトコルによって認識される形式に "変換" する NDIS 中間ドライバーを提供できます。

基になるミニポートドライバーがこのクエリに対して**NULL**を返した場合、または実験的なメディアの種類が使用されている場合は、ドライバーで Receive with [NdisMCoIndicateReceivePacket](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff553455(v=vs.85))を指定する必要があります。


## <a name="requirements"></a>要件

**バージョン**: Windows Vista 以降の**ヘッダー**: Ntddndis (Ndis .h を含む)

