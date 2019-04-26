---
title: シリアル化された NDIS ミニポート ドライバー
description: シリアル化された NDIS ミニポート ドライバー
ms.assetid: 6b9b94ad-5d5d-465a-90bc-47095f6e2b9c
keywords:
- ミニポート ドライバー WDK ネットワークの種類
- NDIS ミニポート ドライバー WDK、種類
- シリアル化された NDIS ミニポート ドライバー WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb28d4660b446527ffafd3b1ecbdca5ecf7e1edb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346758"
---
# <a name="serialized-ndis-miniport-drivers"></a>シリアル化された NDIS ミニポート ドライバー





シリアル化された NDIS ミニポート ドライバーでは、Windows Vista およびそれ以降のバージョンの廃止です。 NDIS 6.0 のドライバーでは、シリアル化されたミニポート ドライバーはサポートされていません。 Windows Vista のサポートは、NDIS 5.1 と以前のドライバーに対してのみ、ミニポート ドライバーをシリアル化されます。 逆シリアル化されたミニポート ドライバーとは異なり、シリアル化されたミニポート ドライバーが、独自の操作をシリアル化する NDIS に依存*MiniportXxx*関数とデータのネットワーク パケットを送信するためのキューを管理します。

新しいミニポート ドライバーを記述するかどうか、する必要がありますを記述する、[逆シリアル化されたドライバー](deserialized-ndis-miniport-drivers.md)します。 可能であれば、する必要がありますもポート古いドライバー NDIS 6.0 以降。 NDIS 6.0 のドライバーの移植の詳細については、次を参照してください。 [NDIS 6.0 への移植の NDIS 5.x ドライバー](https://docs.microsoft.com/previous-versions/windows/hardware/network/porting-ndis-5-x-drivers-to-ndis-6-0)します。

 

 





