---
title: グラフィックスメモリの計算
description: グラフィックスメモリの計算
ms.assetid: 030a332b-d1f0-4a86-b11f-cfd2fbe42ac2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfb559848f62cf286ff95eb8e0989ffe7f0e8f0c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839063"
---
# <a name="calculating-graphics-memory"></a>グラフィックスメモリの計算


ビデオメモリマネージャーは、グラフィックスメモリの正確なアカウントを報告する前に、グラフィックスメモリの合計サイズを計算する必要があります。 次の項目の一覧では、ビデオメモリマネージャーがグラフィックスメモリの数値を計算する方法について説明します。

<span id="Total_system_memory"></span><span id="total_system_memory"></span><span id="TOTAL_SYSTEM_MEMORY"></span>システムメモリの合計  
オペレーティングシステムからアクセスできるシステムメモリの合計容量。 BIOS によって割り当てられたメモリは、この合計システムメモリの値に表示されません。 たとえば、1 GB の DIMM (1024 MB) を搭載し、1 MB のメモリを予約する BIOS も搭載されているコンピューターは、1023 MB のシステムメモリを搭載しています。

<span id="Total_system_memory_that_is_available_for_graphics_use"></span><span id="total_system_memory_that_is_available_for_graphics_use"></span><span id="TOTAL_SYSTEM_MEMORY_THAT_IS_AVAILABLE_FOR_GRAPHICS_USE"></span>グラフィックスの使用に使用できる合計システムメモリ  
GPU に専用または共有されているシステムメモリの合計サイズ。 この数値は次のように計算されます。

```cpp
TotalSystemMemoryAvailableForGraphics = MAX((TotalSystemMemory / 2), 64MB)
```

<span id="Commit_limit_on_aperture_segment"></span><span id="commit_limit_on_aperture_segment"></span><span id="COMMIT_LIMIT_ON_APERTURE_SEGMENT"></span>絞りセグメントのコミット制限  
ビデオメモリマネージャーが使用できるシステムメモリの量によって、ピン留めするためのミニポートドライバーを表示できます (つまり、ミニポートドライバーを表示するシステムメモリの量は、任意の時点で GPU が使用されます)。 GPU に割り当てられているシステムメモリの合計容量がコミット制限を超えている可能性があります。ただし、ビデオメモリマネージャーでは、コミット制限の量が常に1つのアパーチャセグメントに存在することが保証されます。

既定では、特定のアパーチャセグメントのコミット制限は、そのセグメントのサイズです。 ドライバーでセグメントが記述されている場合、表示ミニポートドライバーでは、 [**DXGK\_SEGMENTDESCRIPTOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor)構造体の**commitlimit**メンバーに異なるコミット制限を指定できます。 このように指定されたコミット制限は、ドライバーが記述する特定のセグメントにのみ適用されます。

セグメントごとのコミット制限に加えて、すべてのアパーチャセグメントにグローバルコミット制限があります。 このグローバルコミット制限は、共有システムメモリとも呼ばれます。 この値は、ビデオメモリマネージャーによって計算されます。 ただし、表示ミニポートドライバーでは、この値を[**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)構造体の**ApertureSegmentCommitLimit**メンバーの小さい値に減らすことができますが、この方法はお勧めしません。

ビデオメモリマネージャーでは、ディスプレイミニポートドライバーがセグメント単位のコミット制限に違反したり、グローバルコミット制限に違反したりすることは許可されていません。 特定のセグメントに 1 GB のコミット制限があり、グローバルコミット制限が 256 MB の場合、ビデオメモリマネージャーでは、ディスプレイミニポートドライバーが、256 MB を超えるシステムメモリをそのセグメントにマップすることを許可していません。

<span id="Dedicated_video_memory"></span><span id="dedicated_video_memory"></span><span id="DEDICATED_VIDEO_MEMORY"></span>専用のビデオメモリ  
ディスプレイミニポートドライバーが各セグメントの[**DXGK\_SEGMENTFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentflags)構造体で**PopulatedFromSystemMemory**メンバーを指定しなかったすべてのメモリセグメントのサイズの合計。

<span id="Dedicated_system_memory"></span><span id="dedicated_system_memory"></span><span id="DEDICATED_SYSTEM_MEMORY"></span>専用システムメモリ  
ディスプレイミニポートドライバーが各セグメントの[**DXGK\_SEGMENTFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentflags)構造体の**PopulatedFromSystemMemory**メンバーを指定するすべてのメモリセグメントのサイズの合計。 この数を、グラフィックスの使用に使用できる合計システムメモリ (Totalsystemmemoryavailable Forgraphics) より大きくすることはできません。

<span id="Shared_system_memory"></span><span id="shared_system_memory"></span><span id="SHARED_SYSTEM_MEMORY"></span>共有システムメモリ  
GPU に共有されるシステムメモリの最大量。 この数値は次のように計算されます。

```cpp
MaxSharedSystemMemory = TotalSystemMemoryAvailableForGraphics - DedicatedSystemMemory
```

GPU に共有されるシステムメモリの量。 この数値は次のように計算されます。

```cpp
SharedSystemMemory = MIN(MIN(SumOfCommitLimitOnAllApertureSegment, DXGK_DRIVERCAPS.ApertureSegmentCommitLimit), MaxSharedSystemMemory)
```

<span id="Total_video_memory"></span><span id="total_video_memory"></span><span id="TOTAL_VIDEO_MEMORY"></span>合計ビデオメモリ  
ビデオメモリの合計サイズ。 この数値は次のように計算されます。

```cpp
TotalVideoMemory = DedicatedVideoMemory + DedicatedSystemMemory + SharedSystemMemory
```

 

 





