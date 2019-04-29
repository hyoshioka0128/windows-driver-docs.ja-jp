---
title: メモリ割り当てのサイズおよびピッチの設定
description: メモリ割り当てのサイズおよびピッチの設定
ms.assetid: babd331f-7aec-4aee-aef9-7c10b98f9181
keywords:
- メモリ割り当て WDK の表示
- WDK の表示メモリの割り当てください。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb189d800a37b48433c19afd339334ec72d12d98
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383857"
---
# <a name="setting-the-size-and-pitch-of-the-memory-allocation"></a>メモリ割り当てのサイズおよびピッチの設定


## <span id="ddk_introduction_to_command_and_dma_buffers_gg"></span><span id="DDK_INTRODUCTION_TO_COMMAND_AND_DMA_BUFFERS_GG"></span>


GDI ハードウェア アクセラレーションをサポートしているディスプレイ ミニポート ドライバーは、次の割り当て呼び出しを処理するときにシステムまたはビデオ メモリの割り当てのピッチとサイズを設定する必要があります。

<span id="DxgkDdiCreateAllocation"></span><span id="dxgkddicreateallocation"></span><span id="DXGKDDICREATEALLOCATION"></span>[**DxgkDdiCreateAllocation**](https://msdn.microsoft.com/library/windows/hardware/ff559606)  
ドライバーがへの呼び出しを処理するときに*DxgkDdiCreateAllocation*、システムまたはビデオ メモリの割り当てのバイト単位のサイズを設定があります。 によって、割り当てのサイズが設定されます、 [ **pCreateAllocation** ](https://msdn.microsoft.com/library/windows/hardware/ff557559) *- &gt;* [ **pAllocationInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff560960) <em>- &gt;</em>**サイズ**メンバー。 割り当てが CPU に表示されている場合は、サイズは (バイト単位)、埋め込みを含む、画面の幅は、ピッチの値を含める必要があります。

割り当てが、CPU に表示される場合、 [ **pGetStandardAllocationDriverData** ](https://msdn.microsoft.com/library/windows/hardware/ff557598) *-* &gt; [ **pCreateGdiSurfaceData**](https://msdn.microsoft.com/library/windows/hardware/ff546021)<em>-&gt;</em>**型**D3DKMDT にメンバーが設定されている\_GDISURFACE\_ステージング\_CPUVISIBLE または D3DKMDT\_GDISURFACE\_EXISTINGSYSMEM します。 ような画面のプロパティの説明を参照してください。 [ **D3DKMDT\_GDISURFACETYPE**](https://msdn.microsoft.com/library/windows/hardware/ff546039)します。

<span id="DxgkDdiGetStandardAllocationDriverData"></span><span id="dxgkddigetstandardallocationdriverdata"></span><span id="DXGKDDIGETSTANDARDALLOCATIONDRIVERDATA"></span>[**DxgkDdiGetStandardAllocationDriverData**](https://msdn.microsoft.com/library/windows/hardware/ff559673)  
ドライバーがへの呼び出しを処理するときに*DxgkDdiGetStandardAllocationDriverData*の CPU に表示されている割り当て、その必要があります。

1.  設定、 [ **pGetStandardAllocationDriverData**](https://msdn.microsoft.com/library/windows/hardware/ff557598)*-*&gt;[**StandardAllocationType**](https://msdn.microsoft.com/library/windows/hardware/ff546589) D3DKMDT メンバー\_STANDARDALLOCATION\_GDISURFACE します。

2.  リダイレクトの GDI ハードウェア アクセラレータとを介して Windows デスクトップ マネージャー (DWM) で使用できる画面の説明の設定、 [ **D3DKMDT\_GDISURFACEDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff546021)構造体指す、 [ **pGetStandardAllocationDriverData**](https://msdn.microsoft.com/library/windows/hardware/ff557598)*-*&gt;**pCreateGdiSurfaceData**メンバー。 たとえば、を通じて割り当てのピッチを設定、**ピッチ**D3DKMDT のメンバー\_GDISURFACEDATA します。

 

 





