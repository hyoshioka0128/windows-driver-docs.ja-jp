---
title: Direct3D コマンド バッファー
description: Direct3D コマンド バッファー
ms.assetid: d8c093fa-da5c-497c-9eb8-4f689eb96cbf
keywords:
- コマンドバッファー WDK Direct3D
- WDK Direct3D のバッファー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af1c0573331cc68ae9c999a9c025158c478f2806
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839747"
---
# <a name="direct3d-command-buffers"></a>Direct3D コマンド バッファー


## <span id="ddk_direct3d_command_buffers_gg"></span><span id="DDK_DIRECT3D_COMMAND_BUFFERS_GG"></span>


次の図は、論理コマンドのサンプルバッファーの一部を示しています。 ドライバーの[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)コールバックは、 [**D3DHAL\_DRAWPRIMITIVES2DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_drawprimitives2data)構造体の**lpDDCommands**メンバーのコマンドバッファーへのポインターを受け取ります。 コマンドバッファーは常に順次処理されます。

![direct3d サンプル論理コマンドバッファーの部分を示す図](images/d3dcmbuf.png)

上の図に示すように、コマンドバッファーには[**D3DHAL\_DP2COMMAND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2command)構造体が含まれています。ここでは、各構造体の**bcommand**メンバーがコマンドを識別します。 使用可能なコマンドを次に示します。

-   D3DDP2OP\_RENDERSTATE は、コマンドバッファーに続く**Wstatecount**[**D3DHAL\_DP2RENDERSTATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2renderstate)構造体があることを示します。 ドライバーは、これらの各構造の状態を解析し、それに応じてプライベートドライバーの状態を更新する必要があります。 また、ドライバーは、 **lpdwRStates**がポイントする配列内の適切な状態を更新する必要があります。 ドライバーがコマンドバッファーで要求された状態をサポートしていない場合、ドライバーは、要求された値を、サポートされているもので上書きする必要があります。

-   D3DDP2OP\_TEXTURESTAGESTATE は、コマンドバッファーに続く**Wstatecount**[**D3DHAL\_DP2TEXTURESTAGESTATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2texturestagestate)構造体があることを示します。 ドライバーは、これらの各構造の状態を解析し、それに応じて、指定されたテクスチャステージに関連付けられているドライバーのテクスチャの状態を更新する必要があります。 ドライバーは、テクスチャステージの状態を Direct3D ランタイムに報告しません。

    ドライバーは、実際に使用する座標セットの数に関係なく、最大8つのテクスチャ座標セットを適切に解析する必要があります。

-   D3DDP2OP\_VIEWPORTINFO は、コマンドバッファーに後に続く[**D3DHAL\_DP2VIEWPORTINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2viewportinfo)構造体が1つあることを示します。 ドライバーは、この構造を解析し、ドライバーの内部レンダリングコンテキストに格納されているビューポート情報を更新する必要があります。

-   D3DDP2OP\_WINFO は、コマンドバッファーに後に続く[**D3DHAL\_DP2WINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2winfo)構造体が1つあることを示します。 ドライバーは、この構造体を解析し、ドライバーの内部レンダリングコンテキストに格納されている w バッファー情報を更新する必要があります。

-   残りの D3DDP2OP\_*Xxx*コマンドは、 **wPrimitiveCount** ( [**D3DHAL\_DP2COMMAND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2command)構造体のメンバー) プリミティブをレンダリングするための十分なデータがコマンドバッファーにあることを示しています。 プリミティブコマンドに応じて、ドライバーは、D3DHAL\_DP2*Xxx*構造体をコマンドバッファーから、頂点に関連付けられたデータを、頂点バッファーとコマンドバッファーのいずれかまたは両方から解析する必要があります。 ドライバーは、すべての有効な D3DDP2OP\_*Xxx*コマンドを処理しようとする必要があります。つまり、ドライバーは、定義されている特定のプリミティブ型を無視することはできません。 詳細については、個々の D3DHAL\_DP2*Xxx*の構造リファレンスページを参照してください。

現在のコマンドに応じて、次の追加情報がコマンドバッファーに格納されます。

-   すべての D3DDP2OP\_インデックス付き*Xxx*プリミティブコマンドのインデックス情報。

-   D3DDP2OP\_TRIANGLEFAN\_IMM および D3DDP2OP\_LINELIST の頂点データ\_IMM プリミティブコマンド。

-   追加の操作は、 [**D3DHAL\_DP2OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ne-d3dhal-_d3dhal_dp2operation)構造体の D3DDP2OP\_*Xxx*オペコードとしても定義されています。 これらは、同じ名前の D3DDP2OP\_*Xxx*コマンドと同じです。

コマンドバッファーには、Direct3D でのみ認識されるコマンドが含まれている場合があります。 ドライバーの[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)コールバックがコマンドを認識しない場合、ドライバーは Direct3D's **D3dParseUnknownCommand** callback を呼び出して、解析を試行します。 **D3dParseUnknownCommand**が正常に返された場合、ドライバーはコマンドバッファーの解析と処理を続行する必要があります。 D3DERR\_COMMAND\_を返さずに**D3dParseUnknownCommand**が失敗した場合、 **D3dDrawPrimitives2**は[**D3DHAL\_DRAWPRIMITIVES2DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_drawprimitives2data)構造体の次のメンバーを設定し、を返します。

-   **Dwerroroffset**で、 **lpDDCommands**ポイントを格納するバッファーの一部である、最初の未処理の[**D3DHAL\_DP2COMMAND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2command)構造体のオフセットを書き込みます。

-   **Ddrval**を D3DERR\_COMMAND\_未解析に設定します。

**D3dParseUnknownCommand**コールバックを初期化する方法の詳細については、「 [Direct3D ドライバーの初期化](direct3d-driver-initialization.md)」を参照してください。

**D3dDrawPrimitives2**の実装を簡単にするために、ドライバー作成者は*Perm3*サンプルコードから解析コードをコピーし、ドライバー固有のレンダリングと状態更新コードのみを記述できます。

Microsoft Windows Driver Kit (WDK) には、3Dlabs Permedia3 sample display Driver (*Perm3*) が含まれていない  **ことに注意**してください。 このサンプルドライバーは、Windows Server 2003 SP1 Driver Development Kit (DDK) から入手できます。このドライバーは、WDHC web サイトの DDK-Windows Driver Development Kit ページからダウンロードできます。

 

Direct3D には、常に現在のレンダリング状態が通知されるとは限りません。 たとえば、実行バッファーは、ドライバーに到着する前にランタイムによって検査されません。 ドライバーは、 [**D3DHAL\_DRAWPRIMITIVES2DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_drawprimitives2data)構造体の**lpdwRStates**メンバーを使用して、レンダリング状態の配列を追跡できます。 これは、状態の変更が発生したときにドライバーが最新の状態に保つための内部レンダリング状態配列へのポインターです。

 

 





