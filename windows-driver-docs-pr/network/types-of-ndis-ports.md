---
title: NDIS ポートの種類
description: NDIS ポートの種類
ms.assetid: a77ceb1b-d4b9-4a42-aa5b-685295722fa3
keywords:
- WDK NDIS、種類のポート
- NDIS ポート WDK、種類
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50afb12241b115c8a95bdc4778e8d6a06dd5d977
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551206"
---
# <a name="types-of-ndis-ports"></a>NDIS ポートの種類





NDIS ポートには、次の種類のいずれかを指定できます。

<a href="" id="ndisporttypeundefined"></a>**NdisPortTypeUndefined**  
既定ポートの種類。 次の種類のいずれかに適合しないポートの一般的なアプリケーションには、この型を使用します。

<a href="" id="ndisporttypebridge"></a>**NdisPortTypeBridge**  
システムの使用に予約されています。

<a href="" id="ndisporttyperasconnection"></a>**NdisPortTypeRasConnection**  
リモート アクセス サービス (RAS) 接続します。

<a href="" id="ndisporttype8021xsupplicant"></a>**NdisPortType8021xSupplicant**  
このホスト コンピューター上のアクセス ポイントに関連付けられているリモートのワイヤレス局です。

<a href="" id="ndisporttypendisimplatform"></a>**NdisPortTypeNdisImPlatform**  
システムの使用に予約されています。

**注**  だけで NDIS 6.30 以降にこの値がサポートされています。

 

NDIS ポートの特性は、別の 1 つのポートのアプリケーションによって異なります。 たとえば、ブリッジ インターフェイスは、中間のドライバーのミニポート ドライバー上端作成、 **NdisPortTypeBridge**ポートの中間のドライバーのプロトコルのエッジが必要とする物理ミニポート アダプターに連結すると、ブリッジでは、3 つをレイヤーします。

## <a name="related-topics"></a>関連トピック


[NDIS ポート](ndis-ports.md)

[NDIS ポートの概要](overview-of-ndis-ports.md)

 

 






