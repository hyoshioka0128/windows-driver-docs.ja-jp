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
ms.openlocfilehash: b6338ada64df707970e8770ada8567d875680b88
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535923"
---
# <a name="closing-an-address-family"></a>アドレス ファミリを閉じる





接続指向のクライアントが呼び出す[ **NdisClCloseAddressFamily** ](https://msdn.microsoft.com/library/windows/hardware/ff561626)自体、コール マネージャー、および基になる特定の NIC 間の関連付けを削除するには

いる CoNDIS スタンドアロン コール マネージャーには、バインドの終了時に、マネージャー (MCM) を基になるミニポート アダプター、またはミニポート呼び出しミニポート アダプターの停止が、関連付けられているアドレス ファミリ (AF) を閉じる場合は、コール マネージャーや、MCM から NDIS に通知する必要があります。 NDIS はそのクライアントが、AF を閉じる必要がありますを開く AF を持つ各いる CoNDIS クライアントを通知します。

ここでは、次のトピックについて説明します。

[いる CoNDIS コール マネージャーまたは MCM を閉じる](closing-a-condis-call-manager-or-mcm.md)

[閉じている CoNDIS クライアントで、アドレス ファミリ](closing-an-address-family-in-a-condis-client.md)

 

 





