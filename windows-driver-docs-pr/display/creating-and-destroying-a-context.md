---
title: コンテキストの作成と破棄
description: コンテキストの作成と破棄
ms.assetid: 31462b0a-ed06-4138-ab91-7ec98bc5ff14
keywords:
- WDK の Direct3D のコンテキストを作成します。
- WDK の Direct3D のコンテキストを破棄します。
- D3dContextCreate
- D3dContextDestroy
- WDK Direct3D のコンテキストを破棄します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c054cfb77603e54fd25747a864b075afe8fd91da
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370220"
---
# <a name="creating-and-destroying-a-context"></a>コンテキストの作成と破棄


## <span id="ddk_creating_and_destroying_a_context_gg"></span><span id="DDK_CREATING_AND_DESTROYING_A_CONTEXT_GG"></span>


ドライバーは、作成し、レンダリングを実行する必要があること、状態情報をカプセル化するデバイス固有のコンテキストを初期化する必要があります。 状態がコンテキスト間で共有されません。このため、ドライバーは、作成した各コンテキストの完全な状態情報を維持する必要があります。

コンテキストを作成するには、ドライバーは、次の操作を行う必要があります。

-   デバイス固有のコンテキストを割り当てると、0 に初期化します。

-   参照してください[ **D3dContextCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_contextcreatecb)そのコールバック内で実行する追加の手順についてはします。 **D3dContextCreate**アプリケーションは、HAL の Direct3D デバイスを作成するときに呼び出されるコールバック。 ドライバーは、このコールバックを実装する必要があります。

ドライバーによって作成されたすべてのテクスチャ ハンドルを参照できる必要があります[ **D3dCreateSurfaceEx** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)内に作成したコンテキストでします。 これによりへの呼び出し時に、このコンテキスト内で作成したテクスチャに関連するすべてのドライバー固有のデータをクリーンアップするドライバー、 [ **D3dContextDestroy** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_contextdestroycb)関数を作成します。

Direct3D の呼び出し[ **D3dContextDestroy** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_contextdestroycb) Direct3D HAL デバイスが破棄されることをアプリケーションが要求したとき。 ドライバーは、指定したコンテキストに割り当てられている、すべてのリソースを解放する必要があります。 これらのリソース リソースが含まれる、たとえば、テクスチャ、頂点とピクセル[シェーダー](direct3d-shaders.md)、[宣言と頂点シェーダーのコード](separating-declarations-and-code-for-vertex-shaders.md)、およびリソースの[非同期クエリ](supporting-asynchronous-query-operations.md).

 

 





