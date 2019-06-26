---
title: アドレス ファミリを閉じる
description: アドレス ファミリを閉じる
ms.assetid: 0533bc31-dd4c-42c4-8170-8201e32e1026
keywords:
- アドレス ファミリの WDK ネットワーク
- AFs WDK ネットワーク
- アドレス ファミリを閉じる
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 334fab6cfd6241537140f4ab4b90769bb5060de5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369220"
---
# <a name="closing-an-address-family"></a>アドレス ファミリを閉じる





接続指向のクライアントが呼び出す[ **NdisClCloseAddressFamily** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclcloseaddressfamily)自体、コール マネージャー、および基になる特定の NIC 間の関連付けを削除するには

いる CoNDIS スタンドアロン コール マネージャーには、バインドの終了時に、マネージャー (MCM) を基になるミニポート アダプター、またはミニポート呼び出しミニポート アダプターの停止が、関連付けられているアドレス ファミリ (AF) を閉じる場合は、コール マネージャーや、MCM から NDIS に通知する必要があります。 NDIS はそのクライアントが、AF を閉じる必要がありますを開く AF を持つ各いる CoNDIS クライアントを通知します。

ここでは、次のトピックについて説明します。

[いる CoNDIS コール マネージャーまたは MCM を閉じる](closing-a-condis-call-manager-or-mcm.md)

[閉じている CoNDIS クライアントで、アドレス ファミリ](closing-an-address-family-in-a-condis-client.md)

 

 





