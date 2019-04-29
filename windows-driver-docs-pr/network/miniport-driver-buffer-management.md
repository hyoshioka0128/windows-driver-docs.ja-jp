---
title: ミニポート ドライバー バッファー管理
description: ミニポート ドライバー バッファー管理
ms.assetid: 3b8844e0-9b38-4030-9aec-b713643de523
keywords:
- バッファーの WDK NDIS ミニポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db3f578bcb571e4baab8f456cb36f4355523a938
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390294"
---
# <a name="miniport-driver-buffer-management"></a>ミニポート ドライバー バッファー管理





通常、ミニポート ドライバーを呼び出す[ **NdisAllocateNetBufferListPool** ](https://msdn.microsoft.com/library/windows/hardware/ff561611)から[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389) のプールを作成するには[**NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。 ミニポート ドライバーでは、これらの構造を使用して、受信したデータを示します。

通常、割り当て、NET ミニポート ドライバー\_バッファー\_リスト構造体を割り当て、1 つのキュー [ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376) そのネットワーク上の構造\_バッファー\_リスト構造体。 NET を事前に割り当てられる方が効率的です\_NET のプールを割り当てるときにバッファーが構造体\_バッファー\_NET の割り当てをリストは構造\_バッファー\_リストの構造体と NET\_バッファーが個別に構造体します。

ミニポート ドライバーを呼び出すことができます**NdisAllocateNetBufferListPool**設定と、 *AllocateNetBuffer*パラメーターを**TRUE**ことを示す[ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)構造が事前に割り当てられます。 この場合は、NET\_バッファーの構造が各 NET で事前に割り当てられた\_バッファー\_ドライバーはプールから割り当てリスト構造。 このようなドライバーを呼び出す必要があります[ **NdisAllocateNetBufferAndNetBufferList** ](https://msdn.microsoft.com/library/windows/hardware/ff561608)構造体をこのプールから割り当てることです。

通常、ミニポート ドライバーを呼び出す**NdisAllocateNetBufferAndNetBufferList**から*MiniportInitializeEx*をそれが必要とする多くのバッファーを割り当てる後続受信操作。 この場合、ドライバーは、空きバッファーの内部リストを管理します。

[ *MiniportReturnNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff559437)関数は、返された NET を準備できます\_バッファー\_後ろに続くで再利用するためのリストの構造を示す値を受信します。 *MiniportReturnNetBufferLists*ネットを返すことができます\_バッファー\_プールにリストの構造体 (たとえば、呼び出すでした[ **NdisFreeNetBufferList** ](https://msdn.microsoft.com/library/windows/hardware/ff562583))、プールに返すことがなく、構造を再利用する方が効率的であることができます。

ミニポート ドライバーは、すべての NET を解放する必要があります\_バッファー\_リストの構造体と NDIS アダプターの停止時に関連付けられているデータ。 ドライバーを呼び出すことができます**NdisFreeNetBufferList**構造体を解放して、 [ **NdisFreeNetBufferListPool** ](https://msdn.microsoft.com/library/windows/hardware/ff562590)ネットの解放関数\_バッファー\_プールの一覧。

 

 





