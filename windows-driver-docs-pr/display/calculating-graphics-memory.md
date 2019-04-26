---
title: グラフィックス メモリの計算
description: グラフィックス メモリの計算
ms.assetid: 030a332b-d1f0-4a86-b11f-cfd2fbe42ac2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5933d95cb8549bf4cc8e10e940c6d5b2142f3ee1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341586"
---
# <a name="calculating-graphics-memory"></a>グラフィックス メモリの計算


ビデオ メモリ マネージャーは、グラフィックス メモリの正確なアカウントを報告する前に、グラフィックス メモリの総量を計算する必要があります。 次の項目の一覧では、ビデオ メモリ マネージャーがグラフィックス メモリの数値を計算する方法について説明します。

<span id="Total_system_memory"></span><span id="total_system_memory"></span><span id="TOTAL_SYSTEM_MEMORY"></span>システム メモリ合計  
オペレーティング システムにアクセスできるシステム メモリの総量。 BIOS が割り当てたメモリは、このシステム メモリの合計数には表示されません。 たとえば、1 GB の DIMM (つまり、1024 MB) とを使用しているコンピューターもが 1023 MB のシステム メモリが 1 MB のメモリを確保する BIOS が表示されます。

<span id="Total_system_memory_that_is_available_for_graphics_use"></span><span id="total_system_memory_that_is_available_for_graphics_use"></span><span id="TOTAL_SYSTEM_MEMORY_THAT_IS_AVAILABLE_FOR_GRAPHICS_USE"></span>グラフィックスを使用するために使用可能な合計システム メモリ  
専用または GPU で共有されているシステム メモリの総量。 この数は、次のように計算されます。

```cpp
TotalSystemMemoryAvailableForGraphics = MAX((TotalSystemMemory / 2), 64MB)
```

<span id="Commit_limit_on_aperture_segment"></span><span id="commit_limit_on_aperture_segment"></span><span id="COMMIT_LIMIT_ON_APERTURE_SEGMENT"></span>コミット aperture セグメント上の制限  
ビデオ メモリ マネージャーでは、システム メモリの量ピン留めするミニポート ドライバーを表示する (つまり、ミニポート ドライバーを表示するシステム メモリの量できます、aperture セグメントを介したメモリ マップ)、特定の時点での GPU 使用します。 GPU に割り当てられたシステム メモリの総量は大幅に; コミット制限を超える場合があります。ただし、ビデオ メモリ マネージャーにより、コミットまでしか限度額が実際には、開口部セグメントに常駐している任意の時点で。

既定では、特定の開口部セグメント上、commit limit は、そのセグメントのサイズです。 ディスプレイのミニポート ドライバーで別のコミット制限値を指定できます、 **CommitLimit**のメンバー、 [ **DXGK\_SEGMENTDESCRIPTOR** ](https://msdn.microsoft.com/library/windows/hardware/ff562035)構造体ときに、ドライバーでは、セグメントについて説明します。 などで指定されているコミット制限方法は、ドライバーを記述する特定のセグメントにのみ適用されます。

セグメントあたりのコミット制限に加えて、グローバル コミットに制限はすべて aperture セグメントです。 このグローバル コミット制限は、"共有システム メモリ"とも呼ばれます。 この値は、ビデオ メモリ マネージャーによって計算されます。 ただし、ディスプレイのミニポート ドライバーに小さい値にこの値を小さくことができますが、 **ApertureSegmentCommitLimit**のメンバー、 [ **DXGK\_DRIVERCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff561062)構造体には、この実習をようお勧めできません。

ビデオ メモリ マネージャーでは、セグメントあたりのコミット制限も、グローバル コミット制限に違反するディスプレイのミニポート ドライバーは許可されません。 特定のセグメントが 1 GB のコミット制限が、グローバル コミット制限値は 256 MB、ビデオ メモリ マネージャーにはそのセグメントを 256 MB 以上のシステム メモリにマップするディスプレイのミニポート ドライバーはできません。

<span id="Dedicated_video_memory"></span><span id="dedicated_video_memory"></span><span id="DEDICATED_VIDEO_MEMORY"></span>専用ビデオ メモリ  
ディスプレイのミニポート ドライバー情報が指定しなかったのセグメントのすべてのメモリのサイズの合計、 **PopulatedFromSystemMemory**内のメンバー、 [ **DXGK\_SEGMENTFLAGS** ](https://msdn.microsoft.com/library/windows/hardware/ff562039)各セグメントの構造体。

<span id="Dedicated_system_memory"></span><span id="dedicated_system_memory"></span><span id="DEDICATED_SYSTEM_MEMORY"></span>専用のシステム メモリ  
ディスプレイのミニポート ドライバーが指定のセグメントのすべてのメモリのサイズの合計、 **PopulatedFromSystemMemory**内のメンバー、 [ **DXGK\_SEGMENTFLAGS** ](https://msdn.microsoft.com/library/windows/hardware/ff562039)各セグメントの構造体。 この数は、グラフィックの使用 (TotalSystemMemoryAvailableForGraphics) で利用可能な合計システム メモリよりも大きいにすることはできません。

<span id="Shared_system_memory"></span><span id="shared_system_memory"></span><span id="SHARED_SYSTEM_MEMORY"></span>共有のシステム メモリ  
GPU に共有されているシステム メモリの最大量。 この数は、次のように計算されます。

```cpp
MaxSharedSystemMemory = TotalSystemMemoryAvailableForGraphics - DedicatedSystemMemory
```

GPU に共有されているシステム メモリの量。 この数は、次のように計算されます。

```cpp
SharedSystemMemory = MIN(MIN(SumOfCommitLimitOnAllApertureSegment, DXGK_DRIVERCAPS.ApertureSegmentCommitLimit), MaxSharedSystemMemory)
```

<span id="Total_video_memory"></span><span id="total_video_memory"></span><span id="TOTAL_VIDEO_MEMORY"></span>ビデオ メモリの合計  
ビデオ メモリの総量。 この数は、次のように計算されます。

```cpp
TotalVideoMemory = DedicatedVideoMemory + DedicatedSystemMemory + SharedSystemMemory
```

 

 





