---
title: ヘッドの作成
description: ヘッドの作成
ms.assetid: 0b6d4aa0-e3c9-45df-998d-d6dfca5ab720
keywords:
- ヘッド WDK DirectX 9.0
- 複数ヘッドハードウェア WDK DirectX 9.0、ヘッドの作成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c90b9baa1566ebd0f2a1c51fa138198218486d56
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839773"
---
# <a name="creating-heads"></a>ヘッドの作成


## <span id="ddk_creating_heads_gg"></span><span id="DDK_CREATING_HEADS_GG"></span>


Microsoft DirectX 9.0 ドライバーは、複数のヘッドカードごとに1つの Microsoft Direct3D コンテキストを作成し、各ヘッドカードの各ヘッドに Microsoft DirectDraw オブジェクトを作成します。 そのため、複数のヘッドカードの作成プロセスには、ヘッドパーツとクロスヘッドパーツがあります。 ヘッドごとの部分は、約 DirectDraw DDI 呼び出しに相当します。これは、Direct3D DDI 呼び出しのクロスヘッドパートです。

さまざまなヘッド間の接続ポイントは、ドライバーの[**D3dCreateSurfaceEx**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)関数によって作成される Direct3D ハンドルです。 ドライバーは、グループ内のすべてのヘッドの各サーフェイスに対して、一意の Direct3D ハンドルを割り当てます。 マスターヘッド上の Direct3D コンテキストは、これらのすべてのハンドルを管理し、任意のヘッドで作成された任意のレンダーターゲットをターゲットにすることができます。特に、下位ヘッドの反転チェーンのバックバッファーです。 各下位ヘッドの**D3dCreateSurfaceEx**関数は、マスターヘッドによって管理されるハンドル参照テーブルを更新できる必要があります。 その後、これらのハンドルは、マスターヘッドのドライバーの[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)関数の呼び出しでのみ使用されます。

ドライバーは、マスターヘッドにテクスチャおよびその他のリソースを作成するだけです。

ドライバーは、次の順序に従ってヘッドを作成し、使用します。

1.  各ヘッドに対して、表示モードと主反転サーフェスを設定するために次の操作が実行されます。
    -   ランタイムは、表示モードを設定します。
    -   ランタイムは、DirectDraw オブジェクトを作成します。
    -   ランタイムは、主反転チェーンと Z バッファーを作成します。 ランタイムは、各サーフェス (Z バッファーを含む) の[**DDSCAPS2**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550292(v=vs.85))構造体の**DwCaps2**メンバーに**DDSCAPS2\_additionalprimary** (0x80000000) 機能ビットを指定して、複数のヘッドカード。 ランタイムは、ドライバーの[*Dd/フェイス*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))関数を呼び出します。
    -   ランタイムは、ドライバーの[**D3dCreateSurfaceEx**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)関数を、最初にマスターに対して、もう1つは**AdapterOrdinalInGroup**によって定義された下位図形の順序で呼び出します。 この呼び出しでは、ランタイムがパスする Direct3D ハンドルは、グループ内のすべてのヘッドで一意であることが保証されます。 ドライバーは、下位のヘッドのハンドルルックアップテーブルに参照を挿入できます。 ただし、Direct3D コンテキストは下位ヘッドに作成されないので、下位ヘッドに対して[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)コマンドは発行されません。 したがって、この参照を挿入する必要はありません。
    -   ランタイムがすべてのヘッド (マスターを含む) に対して[*DdD3dCreateSurfaceEx Urface*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))を呼び出すと、マスターヘッドの DirectDraw オブジェクトの下位の各ヘッドの反転チェーンに対してさらに[](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)呼び出しが行われます。 ドライバーは、各下位ヘッドの前面、背面、深度/ステンシルバッファーごとに、マスターヘッドのハンドルルックアップテーブルにエントリを作成します。

2.  ランタイムは、マスターヘッドの DirectDraw オブジェクトに対してのみ、ドライバーの[*D3dContextCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_contextcreatecb)関数を呼び出します。 これは、アプリケーションの実行中に使用される唯一のコンテキストです。

3.  アプリケーションがテクスチャとリソースの作成を要求すると、ランタイムはマスタヘッドを介してドライバーの[*DdD3dCreateSurfaceEx Urface*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))および[](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)関数を呼び出します。

4.  アプリケーションでレンダリングの呼び出しが行われると、ランタイムは適切な操作コードを使用して、マスターヘッドでドライバーの[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)関数を呼び出します。

    アプリケーションで他の操作を実行すると、次の呼び出しがマスターヘッドと下位ヘッドにルーティングされます。

    -   手順 1. で説明したように、下位の各ヘッドの反転チェーンのハンドルを使用してドライバーを提供する[**D3dCreateSurfaceEx**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)呼び出しが行われます。 これらのハンドルは、通常、アプリケーションが下位のいずれかのヘッドのスワップチェーンのバックバッファーにフレームをレンダリングするときに、 **D3DDP2OP\_SETRENDERTARGET** operation コードトークンと共に使用されます。
    -   ランタイムは、各ヘッド (マスターと下位) でドライバーの[*Ddflip*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_flip)関数を呼び出して、これらのヘッドのプライマリサーフェイスにバッファーを戻します。 この呼び出しは、1つのヘッドから別のヘッドのプライマリサーフェイスへのバックバッファーを提示することはありません。 各ヘッドの反転チェーンは完全に独立しています。
    -   ランタイムは、ドライバーの[*Ddblt*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_blt)関数を呼び出して、任意のヘッドのフロントバッファーにバックバッファーをコピーする場合があります。 この呼び出しは、1つのヘッドから別のヘッドのフロントバッファーにバックバッファーをコピーしません。
    -   この呼び出しは Direct3D コンテキストではなくモニターの状態に関連しているため、ランタイムは任意のヘッドでドライバーの[*DdGetScanLine*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getscanline)関数を呼び出すことができます。
    -   ランタイムは、任意のヘッドのバックバッファーに対してドライバーの[*Ddlock*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_lock)関数を呼び出すことができます。

    アプリケーションでは、各ヘッドに Z バッファーを割り当てるか、各ヘッドで順番に1つの Z バッファーを割り当てることができます。 前者の場合、ランタイムは、手順 1. で説明されているように、各ヘッド (マスターと下位) でドライバーの[*ddの*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))参照元関数を呼び出します。 後者の場合、ランタイムは、マスターヘッド上でのみドライバーの*ddの*"関数" を呼び出します。 どちらの場合も、ランタイムはドライバーの[**D3dCreateSurfaceEx**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)関数を呼び出して、グループ内のすべてのヘッドで一意なすべての Z バッファーにハンドルを提供します。

 

 





