---
title: リソースのメモリの種類を指定します。
description: リソースのメモリの種類を指定します。
ms.assetid: b4691de0-d3c9-4a6f-a9f4-aafb22ea3e97
keywords:
- ビデオ メモリの種類の WDK の表示
- メモリの種類の WDK の表示
- リソースのメモリの種類の WDK 表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ba445fc94bab92226137cc6da200d6eec4bbee0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560860"
---
# <a name="specifying-memory-type-for-a-resource"></a>リソースのメモリの種類を指定します。


ユーザー モードのディスプレイ ドライバーが受け取ったときに使用されるメモリの種類に関する情報を受け取る、[リソースを作成する要求](requesting-and-using-surface-memory.md)します。 システムまたはビデオのいずれかのメモリを割り当て、D3DDDIPOOL としてメモリの種類が指定されて\_SYSTEMMEM または D3DDDIPOOL\_グラフィックスアクセラレータ列挙子のそれぞれの**プール**のメンバー、 [ **D3DDDIARG\_CREATERESOURCE** ](https://msdn.microsoft.com/library/windows/hardware/ff542963)構造体。 さらに、マイクロソフトの Direct3D ランタイムがで次の列挙子のいずれかを指定して使用するビデオ メモリの種類について、ドライバーにヒントを提供、**プール**メンバー。

-   D3DDDIPOOL\_LOCALVIDMEM

    ランタイムは、ドライバーの使用のローカル ビデオ メモリをお勧めします。

-   D3DDDIPOOL\_NONLOCALVIDMEM

    ランタイムは、ドライバーがローカルでないビデオ メモリ (AGP メモリなど) を使用することをお勧めします。

ランタイムは、ユーザー モードへのヒントの表示パフォーマンスを向上させるためにドライバーを提供します。 たとえば、ランタイムを指定 D3DDDIPOOL\_NONLOCALVIDMEM 場合は、CPU が高速非ローカルのビデオ メモリを使用して実行すると、画面に書き込みます。

ユーザー モードのディスプレイ ドライバーを使って表示ミニポート ドライバーにヒントを通過する、 **pPrivateDriverData**のメンバー、 [ **D3DDDI\_ALLOCATIONINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff544364)と[ **DXGK\_ALLOCATIONINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff560960)ベンダー固有の方法で構造体。 ディスプレイのミニポート ドライバーでビデオ メモリ マネージャーに、適切なメモリのセグメントのセグメントの識別子を返すことで使用することを示します、 **HintedSegmentId** 、DXGK のメンバー\_ALLOCATIONINFO 構造体ドライバーの呼び出しから[ **DxgkDdiCreateAllocation** ](https://msdn.microsoft.com/library/windows/hardware/ff559606)関数。

、リソースの作成に使用されるビデオ メモリの種類に関係なく、ユーザー モードのディスプレイ ドライバーは、実行時に、セマンティックの相違点を公開する必要がありますしません。 ビデオ メモリの種類ごとに、ドライバーと同じ情報を表示する必要があり、値が同じ戻り値を返す必要があります。

 

 





