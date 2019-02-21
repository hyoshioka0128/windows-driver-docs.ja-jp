---
title: NDIS 6.20 でメディアの機能拡張
description: NDIS 6.20 でメディアの機能拡張
ms.assetid: abc240da-be6e-4a7a-a9d1-186633c5bfd3
keywords:
- NDIS 6.20 WDK、メディアの機能拡張
- メディアの機能拡張 WDK NDIS 6.20 が動作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea8345740d9d5b8359369394f1fb69f5b7ddeab9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553721"
---
# <a name="media-extensibility-in-ndis-620"></a>NDIS 6.20 でメディアの機能拡張





NDIS 6.20 が動作には、追加のメディア拡張機能が導入されています。 これは、ドライバー スタックのネットワーク層では、独立した複数のメディアがあります。

これらの機能では、NDIS 6.20 が動作し、後では、IEEE 802.3 を実装していないドライバーを実装するために必要なコードの複雑さを軽減します。 さらに、これらの非 802.3 実装は、ARP と DHCP を実装するためにはありません。

NDIS 6.20 以降提供*生 IP*フレームの生 IP (NdisMediumIP) の新しいメディアの種類をサポートします。 たとえば、NDIS WWAN サポートは、生 IP を使用します。

NDIS 6.20 が動作には、バンド (OOB) データを使用して特定のメディアのサポートの強化が導入されています。 特定のメディア情報には、Microsoft を代入するタグがあります。 NDIS 6.20 以降では、複数のメディア固有の情報タグをサポートします。

メディア拡張機能の詳細については、メディア固有の情報の詳細については、次を参照してください[OID\_GEN\_物理\_MEDIUM\_EX](https://msdn.microsoft.com/library/windows/hardware/ff569622)と[。**NDIS\_NBL\_メディア\_特定\_情報\_EX**](https://msdn.microsoft.com/library/windows/hardware/ff566518)します。

 

 





