---
title: プロトコル ドライバー バッファー管理
description: プロトコル ドライバー バッファー管理
ms.assetid: 1f91b58e-d432-46c8-994e-d95c3aadfe43
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 294cb388f13d180d0ea24f0ee7d353ed7c241b4c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574184"
---
# <a name="protocol-driver-buffer-management"></a>プロトコル ドライバー バッファー管理





プロトコル ドライバーを管理する必要があります[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)プール構造体と[ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)の構造体のプールは、操作を送信します。 これらのプールを作成するには、ドライバーは、次の関数を呼び出します。

[**NdisAllocateNetBufferListPool**](https://msdn.microsoft.com/library/windows/hardware/ff561611)

[**NdisAllocateNetBufferPool**](https://msdn.microsoft.com/library/windows/hardware/ff561613)

プロトコル ドライバーでは、次の関数を使用して、構造体をプールから割り当てます。

[**NdisAllocateNetBufferAndNetBufferList**](https://msdn.microsoft.com/library/windows/hardware/ff561608)

[**NdisAllocateNetBufferList**](https://msdn.microsoft.com/library/windows/hardware/ff561609)

[**NdisAllocateNetBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff561607)

呼び出す**NdisAllocateNetBufferAndNetBufferList**呼び出しよりも効率的です**NdisAllocateNetBufferList**続けて**NdisAllocateNetBuffer**します。 ただし、 **NdisAllocateNetBufferAndNetBufferList** 1 つのネットワークを作成するだけ\_ネット上のバッファーの構造体\_バッファー\_リスト構造体。 使用する**NdisAllocateNetBufferAndNetBufferList**、ドライバーを設定する必要があります、 *AllocateNetBuffer*パラメーターを**TRUE**呼び出し時に**NdisAllocateNetBufferListPool**します。

プロトコル ドライバーでは、OID 要求を使用して、基になるドライバーの補充とコンテキストの領域の要件をクエリします。 プロトコル ドライバーが補充し、コンテキスト内でバインディング要件を決定する必要があります、*開く*または*再起動*状態。 ドライバーでは、スタック全体のための十分な補充とコンテキストの領域を割り当てる必要があります。 かどうか、必要に応じてプロトコル ドライバーは、解放、プールおよびに再割り当て、*再起動*状態。

プロトコル ドライバーでは、空き、プールに、次の関数を使用します。

[**NdisFreeNetBufferListPool**](https://msdn.microsoft.com/library/windows/hardware/ff562590)

[**NdisFreeNetBufferPool**](https://msdn.microsoft.com/library/windows/hardware/ff562592)します。

プロトコル ドライバーでは、次の関数を使用して、プールから割り当てられている構造体を解放します。

[**NdisFreeNetBufferList**](https://msdn.microsoft.com/library/windows/hardware/ff562583)

[**NdisFreeNetBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff562582)

ドライバーは、NET を解放する必要があります\_で割り当てられたバッファーの構造体**NdisAllocateNetBuffer**関連付けられている NET を解放する前に\_バッファー\_リスト構造体。 NET\_で割り当てられたバッファーの構造体**NdisAllocateNetBufferAndNetBufferList** 、ドライバーは呼び出し時に解放されます**NdisFreeNetBufferList**関連付けられているネットワークに\_バッファー\_リスト構造体。

 

 





