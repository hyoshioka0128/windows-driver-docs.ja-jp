---
title: メモリ セグメントの使用の初期化
description: メモリ セグメントの使用の初期化
ms.assetid: 8e4cf1dc-c428-4564-9a16-925e17e6d488
keywords:
- メモリ セグメント WDK の表示の初期化
- GPU のアドレス空間 WDK の表示
- ページング バッファー WDK の表示
- セグメントの WDK の表示
- アドレス空間 WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9dd291523544587468e311fd9f139afe00931bdd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571891"
---
# <a name="initializing-use-of-memory-segments"></a>メモリ セグメントの使用の初期化


## <span id="ddk_initializing_use_of_memory_segments_gg"></span><span id="DDK_INITIALIZING_USE_OF_MEMORY_SEGMENTS_GG"></span>


Windows Vista およびそれ以降 (WDDM)、ディスプレイ ドライバー モデルのコンテキストでのメモリのセグメントの記述、グラフィックス処理ユニット (GPU) のアドレス空間を使用するビデオ メモリ マネージャー。 メモリのセグメントは、汎用化し、ビデオ メモリ リソースを仮想化します。 ハードウェアをサポートするメモリの種類に応じてメモリ セグメントが構成されている (たとえば、フレーム バッファー メモリまたはシステム メモリの開口部)。

Microsoft DirectX グラフィックスのカーネル サブシステム (Dxgkrnl.sys) が表示ミニポート ドライバーを呼び出してメモリ セグメントの使用方法を初期化する[ *DxgkDdiQueryAdapterInfo* ](https://msdn.microsoft.com/library/windows/hardware/ff559746)関数。 メモリのセグメントに関する情報を返すディスプレイ ミニポート ドライバーに出力するため、 *DxgkDdiQueryAdapterInfo*呼び出し、グラフィックス サブシステムでは、いずれかを指定します、 **DXGKQAITYPE\_QUERYSEGMENT**または**DXGKQAITYPE\_QUERYSEGMENT3**値、**型**のメンバー、 [ **DXGKARG\_QUERYADAPTERINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff557621)構造体。

グラフィックス サブシステム呼び出しディスプレイ ミニポート ドライバーの[ *DxgkDdiQueryAdapterInfo* ](https://msdn.microsoft.com/library/windows/hardware/ff559746)関数セグメント情報を 2 回クリックします。 最初の呼び出し*DxgkDdiQueryAdapterInfo*を取得しますが、ドライバーと 2 番目の呼び出しでセグメントの数がサポートされる各セグメントに関する詳細情報を取得します。 呼び出しで*DxgkDdiQueryAdapterInfo*、ドライバーのポイント、 **pOutputData**のメンバー [ **DXGKARG\_QUERYADAPTERINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff557621)に設定されている[ **DXGK\_QUERYSEGMENTOUT** ](https://msdn.microsoft.com/library/windows/hardware/ff562018) (ドライバー バージョンで Windows Display Driver Model (WDDM) 1.2 より前) の構造体、またはに設定[ **DXGK\_QUERYSEGMENTOUT3** ](https://msdn.microsoft.com/library/windows/hardware/hh464082) (WDDM 1.2 およびそれ以降のドライバー) 用の構造体。

最初の呼び出しで、 **pSegmentDescriptor**のメンバー [ **DXGK\_QUERYSEGMENTOUT** ](https://msdn.microsoft.com/library/windows/hardware/ff562018) (用、および WDDM 1.2 より前のドライバー バージョン) または[ **DXGK\_QUERYSEGMENTOUT3** ](https://msdn.microsoft.com/library/windows/hardware/hh464082) (WDDM 1.2 およびそれ以降のドライバー) 用に設定されて**NULL**します。 ドライバーがのみ入力する必要があります、 **NbSegment**のメンバー **DXGK\_QUERYSEGMENTOUT**または**DXGK\_QUERYSEGMENTOUT3**の数サポートされるセグメントの種類。 この番号では、値の数も示されます[ **DXGK\_SEGMENTDESCRIPTOR** ](https://msdn.microsoft.com/library/windows/hardware/ff562035) (用、および WDDM 1.2 より前のドライバー バージョン) または[ **DXGK\_SEGMENTDESCRIPTOR3** ](https://msdn.microsoft.com/library/windows/hardware/hh464086) (WDDM 1.2 とそれ以降のドライバー) の 2 番目の呼び出しからドライバーを必要とする構造体[ *DxgkDdiQueryAdapterInfo* ](https://msdn.microsoft.com/library/windows/hardware/ff559746).

2 番目の呼び出しでは、ドライバーはのすべてのメンバーを入力する必要があります[ **DXGK\_QUERYSEGMENTOUT** ](https://msdn.microsoft.com/library/windows/hardware/ff562018)または[ **DXGK\_QUERYSEGMENTOUT3**](https://msdn.microsoft.com/library/windows/hardware/hh464082). 2 番目の呼び出しでは、ドライバーが設定配列のサイズ**NbSegment**の[ **DXGK\_SEGMENTDESCRIPTOR** ](https://msdn.microsoft.com/library/windows/hardware/ff562035)または[ **DXGK\_SEGMENTDESCRIPTOR3** ](https://msdn.microsoft.com/library/windows/hardware/hh464086)内の構造体、 **pSegmentDescriptor**のメンバー **DXGK\_QUERYSEGMENTOUT**または**DXGK\_QUERYSEGMENTOUT3**ドライバーがサポートするセグメントに関する情報を使用します。

両方の呼び出しで[ *DxgkDdiQueryAdapterInfo*](https://msdn.microsoft.com/library/windows/hardware/ff559746)、 **pInputData**のメンバー [ **DXGKARG\_QUERYADAPTERINFO**](https://msdn.microsoft.com/library/windows/hardware/ff557621)を指す、 [ **DXGK\_QUERYSEGMENTIN** ](https://msdn.microsoft.com/library/windows/hardware/ff562015) AGP の開口部のプロパティと場所に関する情報を含む構造体。 AGP 開口部が使用できない場合、またはいずれかが存在するが、適切な GART ドライバーがインストールされていない場合は、AGP aperture に関する情報は、0 に設定されます。 かどうか AGP aperture が存在しない、ディスプレイのミニポート ドライバーいないはずの**pSegmentDescriptor**の配列[ **DXGK\_QUERYSEGMENTOUT** ](https://msdn.microsoft.com/library/windows/hardware/ff562018)または[ **DXGK\_QUERYSEGMENTOUT3**](https://msdn.microsoft.com/library/windows/hardware/hh464082)AGP 型の開口部セグメントをサポートしていること。 AGP 型 aperture セグメントは、このような状況に示されているが、アダプターは初期化に失敗します。

初期化中に、メモリが十分にある、ので、ページング バッファーのメモリは、特定のセグメントから割り当てことができます。 ビデオ メモリ マネージャーで指定されたセグメントからページング バッファーのメモリを割り当て、 **PagingBufferSegmentId**のメンバー [ **DXGK\_QUERYSEGMENTOUT** ](https://msdn.microsoft.com/library/windows/hardware/ff562018)または[ **DXGK\_QUERYSEGMENTOUT3**](https://msdn.microsoft.com/library/windows/hardware/hh464082)します。 ドライバーは、2 番目の呼び出しでページング バッファー セグメントの識別子を示します[ *DxgkDdiQueryAdapterInfo*](https://msdn.microsoft.com/library/windows/hardware/ff559746)します。 ドライバーでページング バッファーを割り当てる必要があるバイト単位でサイズを指定する必要がありますも、 **PagingBufferSize**のメンバー **DXGK\_QUERYSEGMENTOUT**または**DXGK\_QUERYSEGMENTOUT3**します。

セグメントのメモリとページング バッファーの使用の詳細については、次を参照してください。[メモリ セグメントの処理](handling-memory-segments.md)と[ビデオ メモリ リソースをページング](paging-video-memory-resources.md)します。

 

 





