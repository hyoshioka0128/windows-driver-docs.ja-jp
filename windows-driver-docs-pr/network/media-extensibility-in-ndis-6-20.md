---
title: NDIS 6.20 のメディア拡張性
description: NDIS 6.20 のメディア拡張性
ms.assetid: abc240da-be6e-4a7a-a9d1-186633c5bfd3
keywords:
- NDIS 6.20 WDK、メディア拡張
- メディア拡張機能 WDK NDIS 6.20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e2fe7f34974a03acb9213717be402e32ecd8594
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844265"
---
# <a name="media-extensibility-in-ndis-620"></a>NDIS 6.20 のメディア拡張性





NDIS 6.20 では、追加のメディア拡張機能が導入されています。 つまり、ドライバースタックのネットワーク層は、よりメディアに依存しません。

NDIS 6.20 以降のこれらの機能により、IEEE 802.3 を実装していないドライバーの実装に必要なコードの複雑さが軽減されます。 また、これらの IEEE 802.3 以外の実装では、ARP と DHCP を実装する必要はありません。

NDIS 6.20 以降では、raw ip (NdisMediumIP) の新しいメディアの種類を使用して、*生の ip*フレームのサポートを提供します。 たとえば、NDIS WWAN サポートは生の IP を使用します。

NDIS 6.20 では、メディア固有の帯域外 (OOB) データのサポートが強化されています。 メディア固有の情報には、Microsoft によって割り当てられるタグがあります。 NDIS 6.20 以降では、複数のメディア固有の情報タグがサポートされています。

メディア固有の情報の詳細については、メディア拡張機能の詳細については、「 [OID\_GEN\_物理\_MEDIUM\_EX](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-physical-medium-ex)および[**NDIS\_NBL\_media\_特定の\_」を参照してください。情報\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_nbl_media_specific_information_ex)

 

 





