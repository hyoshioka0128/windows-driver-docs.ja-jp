---
title: コンテキストの作成と破棄
description: コンテキストの作成と破棄
ms.assetid: 31462b0a-ed06-4138-ab91-7ec98bc5ff14
keywords:
- コンテキスト WDK Direct3D, 作成
- コンテキスト WDK Direct3D, 破棄
- D3dContextCreate
- D3dContextDestroy
- コンテキスト WDK Direct3D を破棄しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c26b590256bf9a682979fd04634fe2dbebb9294d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839029"
---
# <a name="creating-and-destroying-a-context"></a>コンテキストの作成と破棄


## <span id="ddk_creating_and_destroying_a_context_gg"></span><span id="DDK_CREATING_AND_DESTROYING_A_CONTEXT_GG"></span>


ドライバーは、レンダリングを実行するために必要な状態情報をカプセル化するデバイス固有のコンテキストを作成し、初期化する必要があります。 状態はコンテキスト間で共有されていません。そのため、ドライバーは、作成する各コンテキストの完全な状態情報を保持する必要があります。

コンテキストを作成するには、ドライバーが次の操作を実行する必要があります。

-   デバイス固有のコンテキストを割り当て、ゼロで初期化します。

-   そのコールバック内で実行する追加の手順については、「 [**D3dContextCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_contextcreatecb) 」を参照してください。 **D3dContextCreate**コールバックは、アプリケーションが Direct3D HAL デバイスを作成するときに呼び出されます。 ドライバーは、このコールバックを実装する必要があります。

ドライバーは、作成されたコンテキスト内で[**D3dCreateSurfaceEx**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)によって作成されたすべてのテクスチャハンドルを参照できる必要があります。 これにより、ドライバーは、 [**D3dContextDestroy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_contextdestroycb)関数の呼び出しが行われたときに、このコンテキスト内で作成されたテクスチャに関連するドライバー固有のすべてのデータをクリーンアップできます。

Direct3d は、Direct3D HAL デバイスが破棄されることをアプリケーションが要求すると、 [**D3dContextDestroy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_contextdestroycb)を呼び出します。 ドライバーは、指定されたコンテキストに割り当てられているすべてのリソースを解放する必要があります。 これらのリソースには、テクスチャリソース、頂点シェーダーとピクセル[シェーダー](direct3d-shaders.md)、[頂点シェーダーの宣言とコード](separating-declarations-and-code-for-vertex-shaders.md)、[非同期クエリ](supporting-asynchronous-query-operations.md)のリソースなどがあります。

 

 





