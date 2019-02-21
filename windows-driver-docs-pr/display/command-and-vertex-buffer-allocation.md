---
title: コマンドと頂点バッファーの割り当て
description: コマンドと頂点バッファーの割り当て
ms.assetid: 07666a6f-1d2e-4f30-bba8-a09b59225ecf
keywords:
- コマンド バッファー WDK Direct3D
- 頂点バッファー WDK Direct3D
- WDK Direct3D バッファー
- Direct3D バッファーの割り当てください。
- WDK Direct3D の暗黙的な頂点バッファー
- WDK Direct3D の明示的な頂点バッファー
- DDSCAPS2_VERTEXBUFFER
- DDSCAPS2_COMMANDBUFFER
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea323e33290e6a6a4181500c71f98bf73457e77f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557864"
---
# <a name="command-and-vertex-buffer-allocation"></a>コマンドと頂点バッファーの割り当て


## <span id="ddk_command_and_vertex_buffer_allocation_gg"></span><span id="DDK_COMMAND_AND_VERTEX_BUFFER_ALLOCATION_GG"></span>


Direct3D で使用されるバッファーの次の 3 つの種類があります。

-   内部使用のみで、作成される暗黙的な頂点バッファーつまり、アプリケーションは、それらを認識ではありません。 1 つの暗黙的な頂点バッファーは、常にコンテキストの作成後に作成し、Direct3D は、それらの頂点データを格納します。

-   明示的な頂点バッファーには、アプリケーションの要求に対する応答としてのみ作成されます。 Direct3D は、明示的な頂点バッファー、頂点のデータを格納します。

-   コマンド バッファーは、内部でのみ使用が作成されます。つまり、アプリケーションでは、コマンド バッファーの認識しません。 Direct3D では、コマンドのデータをコマンド バッファーに格納します。

暗黙的な頂点バッファーは、特別な頂点バッファーのバッチ処理のため、Direct3D によって内部的に使用します。 デバイスの初期化中に作成され、multibuffered ことができます。 それらは常に読み取り/書き込みがある置かないでビデオ メモリ内 (Microsoft DirectX 6.0 とそれ以降のバージョン) のため。 この種類のバッファーが、両方の DDSCAPS2 の不在によってマークされている\_筆者と DDSCAPS2\_COMMANDBUFFER フラグ。

明示的な頂点バッファーが作成され、アプリケーションによって制御されます。 これら multibuffered をすることはできず、しない限り、ローカルまたは非ローカルのビデオ メモリに配置することはできません、DDSCAPS\_WRITEONLY フラグを設定します。 明示的な頂点バッファーが付いている DDSCAPS\_すぐします。

コマンド バッファーは、Direct3D によってバッチ コマンドに使用されます。 Multibuffered ことができます、TLVERTEX またはクリッピングを行わない実行バッファー API 呼び出しを除くすべての Api を使用します。 この種類のバッファーが DDSCAPS2 フラグでマークされている\_COMMANDBUFFER します。 これらは明示的なフラグが設定されていないと、無効な命令が含まれるありませんが常に書き込み専用です。

既定では、Direct3D ランタイムは、すべてのこれらのバッファーを割り当てます。 暗黙的な頂点バッファーとコマンド バッファーについては、関連付けられたサーフェスを通じてアクセスします。 すべてのバッファーは、ドライバーに渡される[ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704)コールバック。

### <a name="span-iddriver-allocatedvertexandcommandbuffersspanspan-iddriver-allocatedvertexandcommandbuffersspanspan-iddriver-allocatedvertexandcommandbuffersspandriver-allocated-vertex-and-command-buffers"></a><span id="Driver-Allocated_Vertex_and_Command_Buffers"></span><span id="driver-allocated_vertex_and_command_buffers"></span><span id="DRIVER-ALLOCATED_VERTEX_AND_COMMAND_BUFFERS"></span>ドライバーによって割り当てられた頂点とコマンド バッファー

必要に応じて、Direct3D ドライバーは、コールバック関数を指定して頂点とコマンドのバッファーの割り当てを実行します。 Direct3D のドライバーが記入をこれらのコールバック関数を指定する、 [ **DD\_D3DBUFCALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff550557)構造とポイント、 **lpD3DBufCallbacks**のメンバー[ **DD\_HALINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551627)を構造体。 DD\_HALINFO がによって返される[ **DrvGetDirectDrawInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff556229)ドライバーの DirectDraw コンポーネントの初期化に応答します。 コールバックは、DD で報告される\_D3DBUFCALLBACKS 構造体には。

-   [*CanCreateD3DBuffer*](https://msdn.microsoft.com/library/windows/hardware/ff539361)

-   [*CreateD3DBuffer*](https://msdn.microsoft.com/library/windows/hardware/ff540616)

-   [*DestroyD3DBuffer*](https://msdn.microsoft.com/library/windows/hardware/ff552754)

-   [*LockD3DBuffer*](https://msdn.microsoft.com/library/windows/hardware/ff568216)

-   [*UnlockD3DBuffer*](https://msdn.microsoft.com/library/windows/hardware/ff570106)

同じ方法でこれらの関数を呼び出す、 *DdXxxSurface*コールバック (など[ *DdCanCreateSurface*](https://msdn.microsoft.com/library/windows/hardware/ff549213)) と場合にのみ、DDSCAPS\_EXECUTEBUFFERフラグが設定されています。 バッファーの作成フラグは DDSCAPS\_WRITEONLY、DDSCAPS2\_すぐ、および DDSCAPS2\_COMMANDBUFFER します。

ドライバーをチェックして、要求されているバッファーの種類を決定する、 **ddsCaps**のメンバー、 [ **DD\_画面\_ローカル**](https://msdn.microsoft.com/library/windows/hardware/ff551733)構造体渡される、 **CanCreateExecuteBuffer**と**CreateExecuteBuffer**コールバックを次のフラグ。

-   DDSCAPS\_筆者は、ドライバーが、明示的な頂点バッファーを割り当てることを示します。

-   DDSCAPS\_COMMANDBUFFER では、ドライバーがコマンド バッファーを割り当てることを示します。

-   どちらのフラグが設定されている場合、ドライバーは、暗黙的な頂点バッファーを割り当てる必要があります。

内部的には、ドライバーは、頂点とコマンド バッファーと順番にこれらのバッファーを割り当てます。 Direct3D は、ハードウェアが、他のキューに登録されたバッファーから非同期的にレンダリング中に、特定のペアを格納します。 これは、ダイレクト メモリ アクセス (DMA) と非常に便利です。

Multibuffering セット内のバッファーは、システムまたはビデオ メモリでは、さまざまなメモリの種類ですることができます。 ドライバーは、最初のバッファーを作成する呼び出されると、セットをすぐに作成し、Direct3D にセットの最初のバッファーを返します。 ドライバーは、セット内の各バッファーを割り当てるために使用されるメモリの種類を指定するのにフラグを使用します。 ドライバーは、呼び出しごとにシステム メモリ内で新しいバッファーを返す必要があります[ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704)場合、D3DHALDP2\_SWAPVERTEXBUFFER または D3DHALDP2\_SWAPCOMMANDBUFFER フラグ設定されています。 かどうか、返されたバッファーはビデオ メモリ、対応する D3DHALDP2\_VIDMEMVERTEXBUF または D3DHALDP2\_VIDMEMCOMMANDBUF フラグを設定する必要があります。

場合によっては、Direct3D は、次のバッファーの最小サイズを要求します。 サイズが大きすぎる場合、ドライバーはシステム メモリ (バッキング画面) 内でバッファーを割り当てる必要があります。 サイズが小さすぎる場合より大きなバッファーを提供するドライバーが許可されています。 ドライバーはの追跡バッファーの数とどのようなメモリ型されていて、終了時にすべてをクリーンアップします。

 

 





