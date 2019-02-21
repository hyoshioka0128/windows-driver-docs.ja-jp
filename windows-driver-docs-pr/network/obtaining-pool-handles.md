---
title: 処理プールの取得
description: 処理プールの取得
ms.assetid: 752b0d64-2ca3-4dc0-a6cd-642e96af1f8f
keywords:
- プールの WDK ネットワークを処理します。
- プロトコル ドライバー WDK ネットワー キング、ハンドルのプール
- NDIS プロトコル ドライバー WDK には、プールを処理します。
- ミニポート ドライバー WDK ネットワー キング、ハンドルのプール
- NDIS ミニポート ドライバー WDK、ハンドルをプールします。
- 中間ドライバー WDK ネットワーク、po
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09ec469bd5831a1901880dc2db55483d0362284a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552702"
---
# <a name="obtaining-pool-handles"></a>処理プールの取得





次の NDIS プール割り当て関数には、リソースの割り当てを識別するハンドルが必要です。

-   [**NdisAllocateNetBufferPool**](https://msdn.microsoft.com/library/windows/hardware/ff561613)

-   [**NdisAllocateNetBufferListPool**](https://msdn.microsoft.com/library/windows/hardware/ff561611)

NDIS 6.0 のドライバーは、次のようなハンドルを取得します。

<a href="" id="protocol-drivers"></a>プロトコル ドライバー  
プロトコルのドライバーの呼び出し、 [ **NdisRegisterProtocolDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff564520)ハンドルを取得する関数。

<a href="" id="miniport-drivers"></a>ミニポート ドライバー  
NDIS 呼び出し、 [ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)ミニポート ドライバーにハンドルを渡す関数。

<a href="" id="intermediate-drivers"></a>中間ドライバー  
中級レベルのドライバーの呼び出し、 [ **NdisRegisterProtocolDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff564520)プールで使用される送信操作と NDIS のハンドルを取得する関数を呼び出す*MiniportInitializeEx*にプールで使用される受信操作のため、中間のドライバーにハンドルを渡します。

<a href="" id="filter-drivers"></a>フィルター ドライバー  
NDIS 呼び出し、 [ *FilterAttach* ](https://msdn.microsoft.com/library/windows/hardware/ff549905)フィルター ドライバーにハンドルを渡す関数。

<a href="" id="other-drivers"></a>その他のドライバー  
ドライバーを呼び出すことができる場合、ドライバーは、上記の方法のいずれかで、ハンドルを取得することはできません、 [ **NdisAllocateGenericObject** ](https://msdn.microsoft.com/library/windows/hardware/ff561603)ハンドルを取得する関数。

 

 





