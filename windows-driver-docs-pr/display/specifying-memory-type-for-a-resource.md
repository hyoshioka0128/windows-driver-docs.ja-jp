---
title: リソースのメモリの種類の指定
description: リソースのメモリの種類の指定
ms.assetid: b4691de0-d3c9-4a6f-a9f4-aafb22ea3e97
keywords:
- ビデオメモリの種類 WDK ディスプレイ
- メモリの種類 WDK ディスプレイ
- リソースメモリの種類 WDK ディスプレイ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e2fe99adf82eb1cea8fe4bb24bcc00f60297f65
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825720"
---
# <a name="specifying-memory-type-for-a-resource"></a>リソースのメモリの種類の指定


ユーザーモードの表示ドライバーは、[リソースの作成要求](requesting-and-using-surface-memory.md)を受信するときに使用する必要があるメモリの種類に関する情報を受け取ります。 メモリ型は、 [**D3DDDIARG\_CREATERESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)構造体の**プール**メンバーの D3DDDIPOOL\_SYSTEMMEM または D3DDDIPOOL\_videomemory 列挙子を通じて、システムメモリまたはビデオメモリのどちらかとして指定されます. さらに、Microsoft Direct3D ランタイムは、**プール**メンバーで次の列挙子のいずれかを指定することによって、使用するビデオメモリの種類に関するヒントをドライバーに提供します。

-   D3DDDIPOOL\_LOCALVIDMEM

    ランタイムは、ドライバーがローカルのビデオメモリを使用することを推奨します。

-   D3DDDIPOOL\_NONLOCALVIDMEM

    ランタイムは、ドライバーが非ローカルビデオメモリ (たとえば、AGP メモリ) を使用することを推奨します。

ランタイムは、パフォーマンスを向上させるために、ユーザーモードの表示ドライバーにヒントを提供します。 たとえば、CPU が画面に書き込まれた場合に、非ローカルビデオメモリを使用して高速に実行される場合、ランタイムは D3DDDIPOOL\_NONLOCALVIDMEM を指定することがあります。

ユーザーモードの表示ドライバーは、ベンダー固有の方法で[**D3DDDI\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_allocationinfo)の割り当て情報構造と[**DXGK\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfo)の割り当て情報構造体の**pprivatedriverdata**メンバーを介して、ヒントをディスプレイミニポートドライバーに渡します。 ディスプレイのミニポートドライバーは、ビデオメモリマネージャーに対して、DXGK\_**HintedSegmentId**のメンバーにあるセグメントの識別子を、ドライバーの呼び出しから取得することによって、適切なメモリセグメントを示します。[**DxgkDdiCreateAllocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)関数。

リソースの作成に使用されるビデオメモリの種類に関係なく、ユーザーモードの表示ドライバーでは、セマンティクスの違いをランタイムに公開しないようにする必要があります。 つまり、ビデオメモリの種類ごとに、ドライバーは情報をまったく同じようにレンダリングする必要があり、同じ戻り値を返す必要があります。

 

 





