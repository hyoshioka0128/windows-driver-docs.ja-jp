---
title: リソースのメモリの種類の指定
description: リソースのメモリの種類の指定
ms.assetid: b4691de0-d3c9-4a6f-a9f4-aafb22ea3e97
keywords:
- ビデオ メモリの種類の WDK の表示
- メモリの種類の WDK の表示
- リソースのメモリの種類の WDK 表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7383a7f037e6cddfbf0fb8b55a623a7105699de3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376066"
---
# <a name="specifying-memory-type-for-a-resource"></a>リソースのメモリの種類の指定


ユーザー モードのディスプレイ ドライバーが受け取ったときに使用されるメモリの種類に関する情報を受け取る、[リソースを作成する要求](requesting-and-using-surface-memory.md)します。 システムまたはビデオのいずれかのメモリを割り当て、D3DDDIPOOL としてメモリの種類が指定されて\_SYSTEMMEM または D3DDDIPOOL\_グラフィックスアクセラレータ列挙子のそれぞれの**プール**のメンバー、 [ **D3DDDIARG\_CREATERESOURCE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)構造体。 さらに、マイクロソフトの Direct3D ランタイムがで次の列挙子のいずれかを指定して使用するビデオ メモリの種類について、ドライバーにヒントを提供、**プール**メンバー。

-   D3DDDIPOOL\_LOCALVIDMEM

    ランタイムは、ドライバーの使用のローカル ビデオ メモリをお勧めします。

-   D3DDDIPOOL\_NONLOCALVIDMEM

    ランタイムは、ドライバーがローカルでないビデオ メモリ (AGP メモリなど) を使用することをお勧めします。

ランタイムは、ユーザー モードへのヒントの表示パフォーマンスを向上させるためにドライバーを提供します。 たとえば、ランタイムを指定 D3DDDIPOOL\_NONLOCALVIDMEM 場合は、CPU が高速非ローカルのビデオ メモリを使用して実行すると、画面に書き込みます。

ユーザー モードのディスプレイ ドライバーを使って表示ミニポート ドライバーにヒントを通過する、 **pPrivateDriverData**のメンバー、 [ **D3DDDI\_ALLOCATIONINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddi_allocationinfo)と[ **DXGK\_ALLOCATIONINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfo)ベンダー固有の方法で構造体。 ディスプレイのミニポート ドライバーでビデオ メモリ マネージャーに、適切なメモリのセグメントのセグメントの識別子を返すことで使用することを示します、 **HintedSegmentId** 、DXGK のメンバー\_ALLOCATIONINFO 構造体ドライバーの呼び出しから[ **DxgkDdiCreateAllocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)関数。

、リソースの作成に使用されるビデオ メモリの種類に関係なく、ユーザー モードのディスプレイ ドライバーは、実行時に、セマンティックの相違点を公開する必要がありますしません。 ビデオ メモリの種類ごとに、ドライバーと同じ情報を表示する必要があり、値が同じ戻り値を返す必要があります。

 

 





