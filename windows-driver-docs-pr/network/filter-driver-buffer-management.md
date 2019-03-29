---
title: フィルター ドライバー バッファー管理
description: フィルター ドライバー バッファー管理
ms.assetid: 92b38710-056d-4853-b266-ca86cee298b6
keywords:
- フィルター ドライバー WDK ネットワー キング、バッファー
- NDIS フィルター ドライバー WDK、バッファー
- バッファー管理 WDK NDIS フィルターです。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7cae78746cce3fb63c3832f3da99db273de5e7d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579039"
---
# <a name="filter-driver-buffer-management"></a>フィルター ドライバー バッファー管理





フィルター ドライバーは、他のドライバーから取得したネットワーク データをコピーしたり、送信を開始または受信操作をバッファーを作成します。

フィルター ドライバーは、バッファーを作成していない、ドライバーでは、バッファー プールは管理しません。 このようなドライバーは、他のドライバーから受信するバッファーを渡すだけです。

送信をサポートするか、操作を受信するバッファーを作成するフィルター ドライバーを管理する必要があります[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)プール構造体と[ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)プールを構成します。

これらのプールを作成するには、ドライバーは、次の関数を呼び出します。

[**NdisAllocateNetBufferListPool**](https://msdn.microsoft.com/library/windows/hardware/ff561611)

[**NdisAllocateNetBufferPool**](https://msdn.microsoft.com/library/windows/hardware/ff561613)

フィルター ドライバーは、次の関数を使用して、構造体をプールから割り当てできます。

[**NdisAllocateNetBufferAndNetBufferList**](https://msdn.microsoft.com/library/windows/hardware/ff561608)

[**NdisAllocateNetBufferList**](https://msdn.microsoft.com/library/windows/hardware/ff561609)

[**NdisAllocateNetBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff561607)

呼び出す**NdisAllocateNetBufferAndNetBufferList**呼び出しよりも効率的です**NdisAllocateNetBufferList**続けて**NdisAllocateNetBuffer**します。 ただし、 **NdisAllocateNetBufferAndNetBufferList** 1 つのネットワークを作成するだけ\_ネット上のバッファーの構造体\_バッファー\_リスト構造体。 使用する**NdisAllocateNetBufferAndNetBufferList**、ドライバーを設定する必要があります、 *AllocateNetBuffer*パラメーターを**TRUE**呼び出し時に**NdisAllocateNetBufferListPool**します。

発信フィルター ドライバーは送信要求は、基になるドライバーのコンテキストとバックフィル容量の要件を決定する必要があります。 フィルター ドライバーの使用は、基になるドライバーのバックフィル要件を決定する属性を再起動します。 フィルター ドライバーはバックフィルとコンテキストの要件を決定する必要があります、*再起動*状態。 ドライバーは、スタック全体のバックフィルとコンテキストのための十分な領域を割り当てる必要があります。 かどうか必要に応じて、フィルター ドライバーは、解放、プールおよびそれらを再割り当て、*再起動*状態。

フィルター ドライバーは、空き、プールに、次の関数を使用します。

[**NdisFreeNetBufferListPool**](https://msdn.microsoft.com/library/windows/hardware/ff562590)

[**NdisFreeNetBufferPool**](https://msdn.microsoft.com/library/windows/hardware/ff562592)

フィルター ドライバーでは、次の関数を使用して、プールから割り当てられている構造体を解放します。

[**NdisFreeNetBufferList**](https://msdn.microsoft.com/library/windows/hardware/ff562583)

[**NdisFreeNetBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff562582)

ドライバーは、NET を解放する必要があります\_で割り当てられたバッファーの構造体**NdisAllocateNetBuffer**関連付けられている NET を解放する前に\_バッファー\_リスト構造体。 NET\_で割り当てられたバッファーの構造体**NdisAllocateNetBufferAndNetBufferList** 、ドライバーは呼び出し時に解放されます**NdisFreeNetBufferList**関連付けられているネットワークに\_バッファー\_リスト構造体。

 

 





