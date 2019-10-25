---
title: メモリ セグメントの使用の初期化
description: メモリ セグメントの使用の初期化
ms.assetid: 8e4cf1dc-c428-4564-9a16-925e17e6d488
keywords:
- メモリセグメント WDK 表示、初期化
- GPU アドレス空間 WDK ディスプレイ
- ページングバッファーの WDK 表示
- セグメント WDK 表示
- アドレス空間 WDK ディスプレイ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 586c210fd48a3dec00e52ff74822b5eb8a2ff91d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840367"
---
# <a name="initializing-use-of-memory-segments"></a>メモリ セグメントの使用の初期化


## <span id="ddk_initializing_use_of_memory_segments_gg"></span><span id="DDK_INITIALIZING_USE_OF_MEMORY_SEGMENTS_GG"></span>


メモリセグメントは、Windows Vista 以降 (WDDM) の表示ドライバーモデルのコンテキストで、ビデオメモリマネージャーに対するグラフィックス処理ユニット (GPU) アドレス空間を記述します。 メモリセグメントは、ビデオメモリリソースを一般化し、仮想化します。 メモリセグメントは、ハードウェアがサポートするメモリの種類 (たとえば、フレームバッファーメモリやシステムメモリアパーチャ) に従って構成されます。

メモリセグメントの使用方法を初期化するために、Microsoft DirectX graphics カーネルサブシステム (Dxgkrnl) は、ディスプレイミニポートドライバーの[*DxgkDdiQueryAdapterInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)関数を呼び出します。 ディスプレイミニポートドライバーに*DxgkDdiQueryAdapterInfo*呼び出しからメモリセグメントに関する情報を返すように指示するには、グラフィックサブシステムで**DXGKQAITYPE\_Querysegment**または DXGKQAITYPE のいずれかを指定し **\_** [**Dxgkarg\_QUERYADAPTERINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_queryadapterinfo)構造体の**型**メンバーの QUERYSEGMENT3 値。

グラフィックスサブシステムは、セグメント情報に対してディスプレイミニポートドライバーの[*DxgkDdiQueryAdapterInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)関数を2回呼び出します。 *DxgkDdiQueryAdapterInfo*の最初の呼び出しでは、ドライバーでサポートされているセグメントの数を取得し、2回目の呼び出しで各セグメントに関する詳細情報を取得します。 *DxgkDdiQueryAdapterInfo*の呼び出しでは、ドライバーは、 [**Dxgkarg\_queryadapterinfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_queryadapterinfo)の**Poutputdata**メンバーに[ **\_DXGK QUERYSEGMENTOUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout)構造体を設定します (Windows より前のドライバーバージョンの場合)。ドライバーモデル (WDDM) 1.2) を表示するか、 [**DXGK\_QUERYSEGMENTOUT3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout3)構造体 (wddm 1.2 以降のドライバー用) を設定します。

最初の呼び出しでは、 [**DXGK\_QUERYSEGMENTOUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout)の**PSEGMENTDESCRIPTOR**メンバー (wddm 1.2 より前のドライバーバージョンの場合) または[**DXGK\_QUERYSEGMENTOUT3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout3) (wddm 1.2 以降のドライバーの場合) が**NULL**に設定されます。 ドライバーは、サポートするセグメントの種類の数と共に、 **DXGK\_QUERYSEGMENTOUT**または**DXGK\_QUERYSEGMENTOUT3**の**nbsegment**メンバーだけを入力する必要があります。 この番号は、いない[**DXGK\_SEGMENTDESCRIPTOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor)の数 (wddm 1.2 より前のドライバーバージョンの場合) または[**DXGK\_SEGMENTDESCRIPTOR3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor3) (wddm 1.2 以降のドライバーの場合) を示します。[*DxgkDdiQueryAdapterInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)への2回目の呼び出し。

2番目の呼び出しでは、ドライバーは[**DXGK\_QUERYSEGMENTOUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout)または[**DXGK\_QUERYSEGMENTOUT3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout3)のすべてのメンバーに入力する必要があります。 2番目の呼び出しでは、PSegmentDescriptor の**DXGK**メンバー内の[**DXGK\_SEGMENTDESCRIPTOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor)または[**DXGK\_SEGMENTDESCRIPTOR3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor3)構造体の**nbsegment**のサイズが、ドライバーによって配列に設定される必要があり **\_QUERYSEGMENTOUT**または**DXGK\_** 、ドライバーがサポートするセグメントに関する情報を QUERYSEGMENTOUT3 します。

[*DxgkDdiQueryAdapterInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)の両方の呼び出しで、 [**Dxgkarg\_Queryadapterinfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_queryadapterinfo)の**Pinputdata**メンバーは[**DXGK\_QUERYSEGMENTIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentin)構造体を指します。これには、の場所とプロパティに関する情報が含まれています。AGP アパーチャ。 使用可能な AGP アパーチャがない場合、または、適切な GART ドライバーがインストールされていない場合は、AGP アパーチャに関する情報が0に設定されます。 AGP アパーチャが存在しない場合、ディスプレイミニポートドライバーは、 [**DXGK\_QUERYSEGMENTOUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout)または[**DXGK\_QUERYSEGMENTOUT3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout3)の**pSegmentDescriptor**配列で、agp 型のアパーチャセグメントをサポートしていることを示す必要はありません。 このような状況で、AGP 型のアパーチャセグメントが示されている場合、アダプターは初期化に失敗します。

初期化中に、メモリが十分にあるため、ページングバッファー用のメモリは特定のセグメントから割り当てることができます。 ビデオメモリマネージャーは、 [**DXGK\_QUERYSEGMENTOUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout)または[**DXGK\_QUERYSEGMENTOUT3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout3)の**PagingBufferSegmentId**メンバーに指定されたセグメントからページングバッファーにメモリを割り当てます。 ドライバーは、 [*DxgkDdiQueryAdapterInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)への2回目の呼び出しのページングバッファーセグメントの識別子を示します。 また、ドライバーでは、 **DXGK\_QUERYSEGMENTOUT**または**DXGK\_QUERYSEGMENTOUT3**の**pagingbuffersize**メンバーのページングバッファーに割り当てるサイズ (バイト単位) も指定する必要があります。

メモリセグメントおよびページングバッファーの操作の詳細については、「[メモリセグメントの処理](handling-memory-segments.md)」および「[ビデオメモリリソースのページング](paging-video-memory-resources.md)」を参照してください。

 

 





