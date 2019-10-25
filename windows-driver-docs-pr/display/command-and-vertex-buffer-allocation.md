---
title: コマンド バッファーと頂点バッファーの割り当て
description: コマンド バッファーと頂点バッファーの割り当て
ms.assetid: 07666a6f-1d2e-4f30-bba8-a09b59225ecf
keywords:
- コマンドバッファー WDK Direct3D
- 頂点バッファー WDK Direct3D
- WDK Direct3D のバッファー
- 割り当て (Direct3D バッファーを)
- 暗黙的な頂点バッファー WDK Direct3D
- 明示的な頂点バッファー WDK Direct3D
- DDSCAPS2_VERTEXBUFFER
- DDSCAPS2_COMMANDBUFFER
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fd78cb7061552d5fd2f5a959b5fdbe7c8592c19
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839805"
---
# <a name="command-and-vertex-buffer-allocation"></a>コマンド バッファーと頂点バッファーの割り当て


## <span id="ddk_command_and_vertex_buffer_allocation_gg"></span><span id="DDK_COMMAND_AND_VERTEX_BUFFER_ALLOCATION_GG"></span>


Direct3D で使用されるバッファーには、次の3種類があります。

-   暗黙的な頂点バッファー。内部でのみ使用するために作成されます。つまり、アプリケーションでは認識されません。 1つの暗黙的な頂点バッファーは、コンテキストの作成後に常に作成され、Direct3D は頂点データを格納します。

-   明示的な頂点バッファー。アプリケーション要求への応答としてのみ作成されます。 その後、Direct3D は、明示的な頂点バッファーに頂点データを格納します。

-   コマンドバッファー。内部でのみ使用するために作成されます。つまり、アプリケーションはコマンドバッファーを認識しません。 Direct3D はコマンドバッファーにコマンドデータを格納します。

暗黙の頂点バッファーは、バッチ処理のために Direct3D によって内部的に使用される特殊な頂点バッファーです。 これらは、デバイスの初期化中に作成され、マルチバッファーにすることができます。 これらは常に読み取り/書き込み可能であるため、ビデオメモリに入れないでください (Microsoft DirectX 6.0 およびそれ以降のバージョンの場合)。 この種類のバッファーは、DDSCAPS2\_VERTEXBUFFER と DDSCAPS2\_COMMANDBUFFER フラグの両方がないとマークされます。

明示的な頂点バッファーは、アプリケーションによって作成および制御されます。 これらは、DDSCAPS\_WRITEONLY フラグが設定されていない限り、マルチバッファーにすることはできません。また、ローカルまたは非ローカルのビデオメモリに入れることもできません。 明示的な頂点バッファーは、DDSCAPS\_VERTEXBUFFER でマークされます。

コマンドバッファーは、コマンドをバッチ処理するために Direct3D によって使用されます。 これらは、複数のバッファーを使用し、TLVERTEX またはクリッピングされていない実行バッファー API 呼び出しを除くすべての Api で使用できます。 この種類のバッファーは、フラグ DDSCAPS2\_COMMANDBUFFER によってマークされます。 明示的なフラグが設定されておらず、無効な命令が含まれていない場合でも、これらは常に書き込み専用です。

既定では、これらのバッファーはすべて Direct3D ランタイムによって割り当てられます。 暗黙的な頂点バッファーとコマンドバッファーには、関連付けられているサーフェスを介してアクセスします。 すべてのバッファーは、ドライバーの[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)コールバックに渡されます。

### <a name="span-iddriver-allocated_vertex_and_command_buffersspanspan-iddriver-allocated_vertex_and_command_buffersspanspan-iddriver-allocated_vertex_and_command_buffersspandriver-allocated-vertex-and-command-buffers"></a><span id="Driver-Allocated_Vertex_and_Command_Buffers"></span><span id="driver-allocated_vertex_and_command_buffers"></span><span id="DRIVER-ALLOCATED_VERTEX_AND_COMMAND_BUFFERS"></span>ドライバーによって割り当てられる頂点とコマンドバッファー

Direct3D ドライバーは、コールバック関数を指定することによって、頂点とコマンドバッファーの割り当てを必要に応じて実行します。 これらのコールバック関数を提供するために、Direct3D ドライバーは、 [**dd\_D3DBUFCALLBACKS**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_d3dbufcallbacks)構造体を入力し、 [**dd\_HALINFO**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_halinfo)構造体の**lpD3DBufCallbacks**メンバーを参照します。 HALINFO は、ドライバーの DirectDraw コンポーネントの初期化に応じて[**DrvGetDirectDrawInfo**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgetdirectdrawinfo)によって返されます。\_ DD\_D3DBUFCALLBACKS 構造体で報告されるコールバックは次のとおりです。

-   [*CanCreateD3DBuffer*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_cancreatesurface)

-   [*CreateD3DBuffer*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurface)

-   [*DestroyD3DBuffer*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552754(v=vs.85))

-   [*LockD3DBuffer*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568216(v=vs.85))

-   [*UnlockD3DBuffer*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570106(v=vs.85))

これらの関数は、 *Ddxxx サーフェイス*のコールバックと同じ方法で呼び出されます ( [*ddxxxsurface*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549213(v=vs.85))場合)。 executebuffer フラグが設定されている場合のみ、ddxxxsurface\_ます。 バッファー作成フラグは、DDSCAPS\_WRITEONLY、DDSCAPS2\_VERTEXBUFFER、および DDSCAPS2\_COMMANDBUFFER です。

ドライバーは、 [**DD\_サーフェイス**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_local)の**ddscaps**メンバーを確認することによって、要求されているバッファーの種類を**特定します**。これを行うには、 **CANCREATEEXECUTEBUFFER**に渡されるローカル構造\_次のフラグ:

-   DDSCAPS\_VERTEXBUFFER は、ドライバーが明示的な頂点バッファーを割り当てる必要があることを示します。

-   DDSCAPS\_COMMANDBUFFER は、ドライバーがコマンドバッファーを割り当てる必要があることを示します。

-   どちらのフラグも設定されていない場合、ドライバーは暗黙的な頂点バッファーを割り当てます。

このドライバーは、内部的に頂点とコマンドバッファーを割り当て、これらのバッファーを循環します。 Direct3D は、ハードウェアが他のキューに置かれているバッファーから非同期にレンダリングする間に、指定されたペアを入力します。 これは、ダイレクトメモリアクセス (DMA) で非常に便利です。

マルチバッファリングセット内のバッファーは、異なるメモリ型 (システムメモリまたはビデオメモリ内) に存在することがあります。 最初のバッファーを作成するためにドライバーが呼び出されると、すぐに設定が作成され、Direct3D に設定されたの最初のバッファーが返されます。 ドライバーは、フラグを使用して、セット内の各バッファーを割り当てるために使用したメモリの種類を指定します。 D3DHALDP2\_SWAPVERTEXBUFFER または D3DHALDP2\_SWAPCOMMANDBUFFER フラグが設定されている場合、ドライバーは[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)を呼び出すたびに、システムメモリ内に新しいバッファーを返す必要があります。 返されたバッファーがビデオメモリ内にある場合は、対応する D3DHALDP2\_VIDMEMVERTEXBUF または D3DHALDP2\_VIDMEMCOMMANDBUF フラグを設定する必要があります。

Direct3D は、次のバッファーの最小サイズを要求することがあります。 サイズが大きすぎる場合、ドライバーはシステムメモリ (バッキングサーフェイス) にバッファーを割り当てます。 サイズが小さすぎる場合、ドライバーはより大きなバッファーを提供できます。 ドライバーは、バッファーの数とメモリの種類を追跡し、終了時にすべてをクリーンアップする必要があります。

 

 





