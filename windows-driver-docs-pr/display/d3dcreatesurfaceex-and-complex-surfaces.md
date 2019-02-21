---
title: D3dCreateSurfaceEx と複雑な表面
description: D3dCreateSurfaceEx と複雑な表面
ms.assetid: aabe01bd-a7b8-4533-970e-4e1e49ba6596
keywords:
- コンテキスト WDK の Direct3D D3dCreateSurfaceEx
- D3dCreateSurfaceEx
- 複雑なサーフェス WDK Direct3D
- 暗黙的な表面の添付ファイル WDK Direct3D
- 明示的な表面の添付ファイル WDK Direct3D
- surface WDK Direct3D の添付ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12d29059a8a4300dc447ae2a59257bf7389823e3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527703"
---
# <a name="d3dcreatesurfaceex-and-complex-surfaces"></a>D3dCreateSurfaceEx と複雑な表面


## <span id="ddk_d3dcreatesurfaceex_and_complex_surfaces_gg"></span><span id="DDK_D3DCREATESURFACEEX_AND_COMPLEX_SURFACES_GG"></span>


説明したよう[の作成と破棄 DirectDraw サーフェス](creating-and-destroying-directdraw-surfaces.md)DirectDraw ドキュメントでは、複雑な画面の作成と配列に渡されるサーフェスの[ *DdCreateSurface*](https://msdn.microsoft.com/library/windows/hardware/ff549263). ただし、複雑な場合でも、ルート画面へのポインターのみに渡される[ **D3dCreateSurfaceEx**](https://msdn.microsoft.com/library/windows/hardware/ff542840)します。 ドライバーをルート画面の添付ファイルの一覧を移動し、接続されているすべてのサーフェス側ドライバーのコピーを作成する必要があります。 キューブ マップの MIP マップの作成を処理しようとして、ドライバーの場合は、この難しい操作できます。

DirectDraw surface の添付ファイルの暗黙的および明示的な 2 種類があります。 暗黙的な添付ファイルは、複雑なサーフェスの作成中に形成されます。 たとえば、アプリケーションでは、プライマリのフリッピング チェーンを作成するとき、プライマリとバック バッファーが、1 つによって作成、 **CreateSurface** API 呼び出しとにアタッチされているもう 1 つによって暗黙的に、 **CreateSurface**呼び出します。 別の例は、1 つで、一連の MIP マップが作成される場所、MIP マップ チェーン**CreateSurface** API 呼び出し。 さまざまな画面が作成されたときに明示的な添付ファイルの形式が**CreateSurface**によって明示的に呼び出しが関連付けられている**AddAttachedSurface**します。

DirectX のランタイムがドライバーを呼び出す方法とタイミング[ **D3dCreateSurfaceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff542840)関数と、ドライバーがサーフェスを処理する方法は、暗黙的または明示的にこれらのサーフェスが関連付けられているかどうかに依存します。 2 つのサーフェスが明示的に接続されているときに、これらのサーフェスの両方によって作成されたを別々 に呼び出して**CreateSurface**への呼び出しで各画面保存されましたが、 **D3dCreateSurfaceEx**する前に、画面の添付ファイルが作成されました。 ただしの場合は、暗黙的に接続されている画面が 1 つだけ**CreateSurface**と**D3dCreateSurfaceEx**サーフェスのチェーン全体の呼び出しが行われます。 そのため、処理するときに、 **D3dCreateSurfaceEx**呼び出し、ドライバーは接続されているハンドルを特定し、ドライバーに接続されている各画面の側のデータ構造を作成するサーフェスの一覧を実行する必要があります。 ただし、接続されている画面の一覧には、暗黙的または明示的にアタッチされるサーフェスの組み合わせを含めることができます。 ドライバーは既に通知を受けているを指定して明示的に接続されているサーフェス**D3dCreateSurfaceEx**おそらく、このような画面を再処理する必要がないとします。

ドライバーは、DDAL を使用して、明示的および暗黙的な添付ファイルを区別できる\_に暗黙の型のフラグが格納されている、 **dwFlags**のフィールド、 [ **DD\_ATTACHLIST**](https://msdn.microsoft.com/library/windows/hardware/ff550466)データ構造体。 場合 DDAL\_暗黙の型が設定されている、 **dwFlags**フィールド、添付ファイルが暗黙的なと独立した[ **D3dCreateSurfaceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff542840)呼び出しが表示される、添付の画面。 このフラグが設定されていない場合は、添付ファイルが明示的な接続されている画面の結果で、独自**D3dCreateSurfaceEx**呼び出します。 ドライバーでこのフラグを調べると、親画面の一環として、接続されている画面を処理する必要があるかどうかを判断できます**D3dCreateSurfaceEx**を呼び出すかどうか、個別または**D3dCreateSurfaceEx**を呼び出す接続されている画面の加えられました。

詳細については、画面の添付ファイルのセクションをご覧ください。 [DirectDraw ドライバー基礎](directdraw-driver-fundamentals.md)に含まれるサンプル コードを参照してくださいと[ **D3dCreateSurfaceEx**](https://msdn.microsoft.com/library/windows/hardware/ff542840)します。

 

 





