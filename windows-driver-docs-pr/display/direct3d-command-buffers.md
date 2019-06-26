---
title: Direct3D コマンド バッファー
description: Direct3D コマンド バッファー
ms.assetid: d8c093fa-da5c-497c-9eb8-4f689eb96cbf
keywords:
- コマンド バッファー WDK Direct3D
- WDK Direct3D バッファー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5092a069e854cd7072bac69b53997e4e1f9d19d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384873"
---
# <a name="direct3d-command-buffers"></a>Direct3D コマンド バッファー


## <span id="ddk_direct3d_command_buffers_gg"></span><span id="DDK_DIRECT3D_COMMAND_BUFFERS_GG"></span>


次の図は、サンプルの論理コマンド バッファーの一部を示します。 ドライバーの[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)コールバックがコマンド バッファーへのポインターを受け取る、 **lpDDCommands**のメンバー、 [ **D3DHAL\_DRAWPRIMITIVES2DATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_drawprimitives2data)構造体。 コマンド バッファーは、常に順番に処理されます。

![direct3d サンプルの論理コマンド バッファーの部分を示す図](images/d3dcmbuf.png)

上記の図に示すようにコマンド バッファーを含む[ **D3DHAL\_DP2COMMAND** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2command)構造、場所、 **bCommand**各構造体のメンバーコマンドを識別します。 次のリストの可能なコマンド:

-   D3DDP2OP\_RENDERSTATE があることを示します**wStateCount**[**D3DHAL\_DP2RENDERSTATE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2renderstate)コマンドで次の構造バッファー。 ドライバーからこれらの構造体の各状態を解析し、それに応じてそのプライベート ドライバーの状態を更新する必要があります。 ドライバーを配列内の適切な状態を更新する必要がありますも**lpdwRStates**ポイント。 ドライバーがコマンド バッファーに要求された状態をサポートしていない場合、ドライバーはサポートされているいずれかで要求された値をオーバーライドします。

-   D3DDP2OP\_TEXTURESTAGESTATE があることを示します**wStateCount**[**D3DHAL\_DP2TEXTURESTAGESTATE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2texturestagestate)続く構造体コマンド バッファー。 ドライバーは、各構造体から状態を解析し、それに応じて、指定したテクスチャ ステージに関連付けられているドライバーのテクスチャの状態を更新する必要があります。 ドライバー状態をレポートしませんテクスチャ ステージ戻る Direct3D ランタイムにします。

    ドライバーは、実際に座標の数の設定に関係なく、8 つのテクスチャ座標セットまで解析を使用して、正しく必要です。

-   D3DDP2OP\_VIEWPORTINFO が示される 1 つ[ **D3DHAL\_DP2VIEWPORTINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2viewportinfo)コマンド バッファーに続く構造体。 ドライバーは、この構造を解析し、ドライバーの内部レンダリング コンテキストに格納されている、ビューポートの情報を更新する必要があります。

-   D3DDP2OP\_WINFO が示される 1 つ[ **D3DHAL\_DP2WINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2winfo)コマンド バッファーに続く構造体。 ドライバーは、この構造を解析し、ドライバーの内部レンダリング コンテキストに格納されている w バッファー情報を更新する必要があります。

-   残りの D3DDP2OP\_*Xxx*コマンドで表示するためにコマンド バッファーには、十分なデータ次あることを示す**wPrimitiveCount** (のメンバー、 [ **D3DHAL\_DP2COMMAND** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2command)構造) プリミティブ。 プリミティブのコマンドによって、ドライバーが D3DHAL を解析する必要があります\_DP2*Xxx*コマンド バッファーと頂点に関連付けられているデータからいずれかまたは両方、頂点バッファーとコマンド バッファーからの構造体。 すべての有効な D3DDP2OP を処理しようとする必要があります、ドライバー\_*Xxx* ; コマンドは、ドライバーが定義されているプリミティブ型を無視する選択できません。 詳細については、個々 の D3DHAL を参照してください。\_DP2*Xxx*リファレンス ページを構造体。

現在のコマンドによって、次の情報は、コマンド バッファーに格納されます。

-   インデックスのすべての D3DDP2OP 情報\_インデックス化されて*Xxx*プリミティブ コマンド。

-   頂点データを D3DDP2OP\_TRIANGLEFAN\_IMM と D3DDP2OP\_LINELIST\_IMM プリミティブ コマンド。

-   その他の操作は D3DDP2OP としても定義\_*Xxx*でオペコード、 [ **D3DHAL\_DP2OPERATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ne-d3dhal-_d3dhal_dp2operation)構造体。 これらは D3DDP2OP\_*Xxx*同じ名前の付いたコマンド。

コマンド バッファーには、場合によっては Direct3D でのみ認識されるコマンドが含まれています。 場合、ドライバーの[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)コールバックは、コマンドを認識していない、ドライバーは、Direct3D を呼び出す必要があります**D3dParseUnknownCommand**しようとするコールバックそれを解析します。 ときに**D3dParseUnknownCommand**ドライバーは、解析および処理コマンド バッファーを続行する必要がありますが正常に返されます。 場合**D3dParseUnknownCommand** D3DERR を返すことによって失敗した\_コマンド\_未解析、 **D3dDrawPrimitives2**の次のメンバーを設定する必要があります、 [ **D3DHAL\_DRAWPRIMITIVES2DATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_drawprimitives2data)構造体を返します。

-   **DwErrorOffset**、最初のオフセットを書き込む未処理[ **D3DHAL\_DP2COMMAND** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2command)されているバッファーへの一部の構造体**lpDDCommands**ポイント。

-   設定**ddrval** D3DERR に\_コマンド\_UNPARSED します。

初期化する方法については、 **D3dParseUnknownCommand**コールバックを参照してください[Direct3D ドライバーの初期化](direct3d-driver-initialization.md)します。

実装を簡略化する**D3dDrawPrimitives2**、ドライバー作成者がから解析コードをコピー、 *Perm3*サンプル コードと、ドライバー固有の表示と状態コードのみの更新を記述します。

**注**   、Microsoft Windows Driver Kit (WDK) に 3 dlabs Permedia3 サンプルのディスプレイ ドライバーが含まれていません (*Perm3.h*)。 Windows Server 2003 SP1 ドライバー開発キット (DDK)、DDK - WDHC web サイトの Windows ドライバー開発キットのページからダウンロードできるこのサンプル ドライバーを取得できます。

 

Direct3D には常に現在の表示状態の通知されません。 たとえば、実行バッファーは、ランタイムが検査されなかったドライバーに到達する前にします。 ドライバーを監視できる、レンダリング状態配列、 **lpdwRStates**のメンバー、 [ **D3DHAL\_DRAWPRIMITIVES2DATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_drawprimitives2data)構造体。 これは、状態の変更が発生すると、ドライバーを最新の状態で保持する内部レンダリング状態配列へのポインターです。

 

 





