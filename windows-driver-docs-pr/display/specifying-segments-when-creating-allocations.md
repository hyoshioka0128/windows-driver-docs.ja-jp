---
title: 割り当てを作成するときにセグメントを指定します。
description: 割り当てを作成するときにセグメントを指定します。
ms.assetid: 31bfbfd9-89e5-42fe-90bc-8ff54bac4f8b
keywords:
- メモリのセグメントの WDK 表示、割り当ての作成
- WDK の割り当てを表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2186ca0e2f57633fd8ad791e445ed9c9c69f3f1e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530286"
---
# <a name="specifying-segments-when-creating-allocations"></a>割り当てを作成するときにセグメントを指定します。


## <span id="ddk_specifying_segments_for_creating_and_rendering_allocations_gg"></span><span id="DDK_SPECIFYING_SEGMENTS_FOR_CREATING_AND_RENDERING_ALLOCATIONS_GG"></span>


ディスプレイのミニポート ドライバーを指定し、ビデオ メモリ マネージャーの使用が推奨ビデオ メモリ マネージャーがドライバーを呼び出すときにそのメモリ セグメントに関する情報を返します[ **DxgkDdiCreateAllocation** ](https://msdn.microsoft.com/library/windows/hardware/ff559606)関数。 呼び出しで*DxgkDdiCreateAllocation*ドライバーがビデオ リソースの割り当てを作成します。 ドライバーがサポートされるセグメントとセグメント各自の好みの識別子を返します、 [ **DXGK\_ALLOCATIONINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff560960)の割り当てを記述する構造体。

返されるセグメントの情報からは、ビデオ メモリ マネージャーは、指定された操作のページで、適切なメモリ セグメントを決定します。

 

 





