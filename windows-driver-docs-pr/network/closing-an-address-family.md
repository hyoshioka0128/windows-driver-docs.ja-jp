---
title: アドレスファミリの終了の概要
description: アドレスファミリの終了の概要
ms.assetid: 0533bc31-dd4c-42c4-8170-8201e32e1026
keywords:
- アドレスファミリ WDK ネットワーク
- AFs WDK ネットワーク
- アドレスファミリを終了する
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e330313a40c2d5bab914227f0a6ee6a9ecc642b0
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565686"
---
# <a name="closing-an-address-family-overview"></a>アドレスファミリの終了の概要

接続指向クライアントは、 [**NdisClCloseAddressFamily**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclcloseaddressfamily)を呼び出して、それ自体、呼び出しマネージャー、および特定の基になる NIC との間の関連付けを削除します。

CoNDIS スタンドアロン呼び出しマネージャーが、基になるミニポートアダプターへのバインドを閉じるとき、またはミニポート呼び出しマネージャー (MCM) がミニポートアダプターを停止している場合、関連付けられたアドレスファミリ (AF) を閉じる必要がある場合は、呼び出しマネージャーまたは MCM が NDIS に通知する必要があります。 次に、クライアントが AF を閉じる必要がある AF が開いている各 CoNDIS に通知します。

ここでは、次のトピックについて説明します。

[Conmcall マネージャーまたは MCM を閉じる](closing-a-condis-call-manager-or-mcm.md)

[CoNDIS でのアドレスファミリの終了](closing-an-address-family-in-a-condis-client.md)

 

 





