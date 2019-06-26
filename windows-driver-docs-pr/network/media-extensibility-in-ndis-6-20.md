---
title: NDIS 6.20 のメディア拡張性
description: NDIS 6.20 のメディア拡張性
ms.assetid: abc240da-be6e-4a7a-a9d1-186633c5bfd3
keywords:
- NDIS 6.20 WDK、メディアの機能拡張
- メディアの機能拡張 WDK NDIS 6.20 が動作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7364adcd5a0eccf5175322d0941b74b0a0bdd8a1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373987"
---
# <a name="media-extensibility-in-ndis-620"></a>NDIS 6.20 のメディア拡張性





NDIS 6.20 が動作には、追加のメディア拡張機能が導入されています。 これは、ドライバー スタックのネットワーク層では、独立した複数のメディアがあります。

これらの機能では、NDIS 6.20 が動作し、後では、IEEE 802.3 を実装していないドライバーを実装するために必要なコードの複雑さを軽減します。 さらに、これらの非 802.3 実装は、ARP と DHCP を実装するためにはありません。

NDIS 6.20 以降提供*生 IP*フレームの生 IP (NdisMediumIP) の新しいメディアの種類をサポートします。 たとえば、NDIS WWAN サポートは、生 IP を使用します。

NDIS 6.20 が動作には、バンド (OOB) データを使用して特定のメディアのサポートの強化が導入されています。 特定のメディア情報には、Microsoft を代入するタグがあります。 NDIS 6.20 以降では、複数のメディア固有の情報タグをサポートします。

メディア拡張機能の詳細については、メディア固有の情報の詳細については、次を参照してください[OID\_GEN\_物理\_MEDIUM\_EX](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-physical-medium-ex)と[。**NDIS\_NBL\_メディア\_特定\_情報\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_nbl_media_specific_information_ex)します。

 

 





