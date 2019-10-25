---
title: アドレス ファミリを閉じる操作の概要
description: アドレス ファミリを閉じる操作の概要
ms.assetid: 0533bc31-dd4c-42c4-8170-8201e32e1026
keywords:
- アドレスファミリ WDK ネットワーク
- AFs WDK ネットワーク
- アドレスファミリを終了する
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f285ecad68427ccd3051de342587e124098d243
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835147"
---
# <a name="closing-an-address-family-overview"></a>アドレス ファミリを閉じる操作の概要

接続指向クライアントは、 [**NdisClCloseAddressFamily**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclcloseaddressfamily)を呼び出して、それ自体、呼び出しマネージャー、および特定の基になる NIC との間の関連付けを削除します。

CoNDIS スタンドアロン呼び出しマネージャーが、基になるミニポートアダプターへのバインドを閉じるとき、またはミニポート呼び出しマネージャー (MCM) がミニポートアダプターを停止している場合、関連付けられたアドレスファミリ (AF) を閉じる必要がある場合は、呼び出しマネージャーまたは MCM が NDIS に通知する必要があります。 次に、クライアントが AF を閉じる必要がある AF が開いている各 CoNDIS に通知します。

ここでは、次のトピックについて説明します。

[Conmcall マネージャーまたは MCM を閉じる](closing-a-condis-call-manager-or-mcm.md)

[CoNDIS でのアドレスファミリの終了](closing-an-address-family-in-a-condis-client.md)

 

 





