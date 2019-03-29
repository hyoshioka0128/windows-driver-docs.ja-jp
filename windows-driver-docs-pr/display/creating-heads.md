---
title: ヘッドの作成
description: ヘッドの作成
ms.assetid: 0b6d4aa0-e3c9-45df-998d-d6dfca5ab720
keywords:
- ヘッド WDK DirectX 9.0
- 複数ヘッド ハードウェア WDK DirectX 9.0、ヘッドの作成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67e358921c652b2219a77caecbb3e6468c6b33e4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573184"
---
# <a name="creating-heads"></a>ヘッドの作成


## <span id="ddk_creating_heads_gg"></span><span id="DDK_CREATING_HEADS_GG"></span>


Microsoft DirectX 9.0 ドライバーは、各ヘッドが複数のカードで複数ヘッド カードごとに 1 つのマイクロソフトの Direct3D コンテキストと各 head Microsoft DirectDraw オブジェクトを作成します。 したがって、複数ヘッド カード作成プロセスでは、ヘッドの部分とクロス ヘッドの部分があります。 先頭部分は、DirectDraw DDI 呼び出し、Direct3D DDI 呼び出しにまたがるヘッドの一部にほぼ対応します。

さまざまなヘッド間の接続ポイントは、ドライバーのによって作成された Direct3D ハンドル[ **D3dCreateSurfaceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff542840)関数。 ドライバーは、グループ内のすべてのヘッドで各画面に一意の Direct3D ハンドルを割り当てます。 Master head で Direct3D コンテキストは、これらすべてのハンドルを管理し、任意のヘッダーで作成されるすべてのレンダー ターゲットを対象にできます下位ヘッドの反転で最も顕著なバック バッファーにチェーンします。 **D3dCreateSurfaceEx**関数の各下位 head は master head によって管理されているハンドルのルックアップ テーブルを更新できる必要があります。 その後、これらのハンドルが、ドライバーの呼び出しで使用されてのみ[ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704) master head 関数。

ドライバーでは、master head で、テクスチャやその他のリソースがのみ作成します。

ドライバーは作成し、次の順序での説明に従って、ヘッドを連携します。

1.  表示を設定する各 head では、以下の操作の実行モードとプライマリ反転サーフェス。
    -   ランタイムは、表示モードを設定します。
    -   ランタイムは、DirectDraw オブジェクトを作成します。
    -   ランタイムは、プライマリのフリッピング チェーンや Z バッファーを作成します。 ランタイムを指定します、 **DDSCAPS2\_ADDITIONALPRIMARY**ビット (0x80000000) 機能、 **dwCaps2**のメンバー、 [ **DDSCAPS2**](https://msdn.microsoft.com/library/windows/hardware/ff550292)を複数ヘッド カードの追加のプライマリ画面を示すために各サーフェス (Z バッファーを含む) の構造体します。 ランタイムが呼び出す、ドライバーの[ *DdCreateSurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549263)関数。
    -   ランタイムが呼び出す、ドライバーの[ **D3dCreateSurfaceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff542840)関数、およびによって定義された順序で最初に、マスター **AdapterOrdinalInGroup**下位図形の。 この呼び出しでは、Direct3D は、グループ内のすべてのヘッドで一意になるランタイムのパスが保証されるを処理します。 ドライバーは、下位の頭のハンドルのルックアップ テーブルに参照を挿入できます。 ただし、Direct3D のコンテキストに作成されないため、下位ヘッド、いいえ[ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704)のコマンドは、下位ヘッドに発行します。 そのため、この参照を挿入する必要はありません。
    -   ランタイム呼び出し後[ *DdCreateSurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549263)のすべてのヘッド (マスターを含む)、さらに[ **D3dCreateSurfaceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff542840)呼び出しが行われます各下位 head は master head の DirectDraw オブジェクトのチェーンを反転の。 ドライバーは、各ヘッドが下位の前面、戻る、および/深度ステンシル バッファーの master head のハンドルのルックアップ テーブルにエントリを作成します。

2.  ランタイムが呼び出す、ドライバーの[ *D3dContextCreate* ](https://msdn.microsoft.com/library/windows/hardware/ff542178) master head で、DirectDraw オブジェクトに対してのみ関数。 これは、アプリケーションの実行中に使用される唯一のコンテキストです。

3.  アプリケーションは、テクスチャとリソースを作成する要求、ランタイムは、ドライバーを呼び出して[ *DdCreateSurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549263)と[ **D3dCreateSurfaceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff542840) master head を使用して関数。

4.  ランタイムが呼び出す、ドライバーのアプリケーションでは、レンダリングの呼び出しを行う、 [ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704)に対して適切な操作のコードを使用して、master head 関数。

    アプリケーションでは、その他の操作を実行するときに、次の呼び出しは、マスターおよび下位のヘッドにルーティングされます。

    -   1 つは、手順の説明に従って[ **D3dCreateSurfaceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff542840)各ヘッドが下位のチェーンの反転のハンドルでドライバーを指定する呼び出しは行われます。 これらのハンドルは、通常の使用、 **D3DDP2OP\_SETRENDERTARGET**アプリケーション下位ヘッドのスワップ チェーンのいずれかのバック バッファーにフレームをレンダリングするときに、操作コード トークンです。
    -   ランタイムが呼び出す、ドライバーの[ *DdFlip* ](https://msdn.microsoft.com/library/windows/hardware/ff549306)で各ヘッド (マスターおよび下位) これらヘッドのサーフェスをプライマリにバック バッファーを提示する関数。 この呼び出しは決してを別のヘッドのプライマリ画面に 1 つのヘッドからバック バッファーを表示します。 各ヘッドの反転のチェーンは完全に独立します。
    -   ランタイムは、ドライバーを呼び出すことができます[ *DdBlt* ](https://msdn.microsoft.com/library/windows/hardware/ff549205)バック バッファーを任意のヘッダーの前面のバッファーにコピーする関数。 この呼び出しはことはありません、もう 1 つの head フロント バッファーに、1 つのヘッドからバック バッファーをコピーします。
    -   ランタイムは、ドライバーを呼び出すことができます[ *DdGetScanLine* ](https://msdn.microsoft.com/library/windows/hardware/ff549497)この呼び出しに関連するモニターと Direct3D のコンテキストではなくの状態のために、任意のヘッダーに機能します。
    -   ランタイムは、ドライバーを呼び出すことができます[ *DdLock* ](https://msdn.microsoft.com/library/windows/hardware/ff549599)任意のヘッダーのバック バッファーに対して関数。

    アプリケーションでは、各ヘッドで Z バッファーを割り当てすることか、各ヘッドを順番に使用する 1 つの Z バッファーを割り当てることができます。 前者の場合、共通言語ランタイムは、ドライバーの[ *DdCreateSurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549263)関数が各ヘッド (マスターおよび下位) には」の説明に従ってステップ 1。 後者の場合、共通言語ランタイムは、ドライバーの*DdCreateSurface* master head でのみ機能します。 いずれの場合も、共通言語ランタイムは、ドライバーの[ **D3dCreateSurfaceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff542840)関数は、グループ内のすべてのヘッド全体で一意のすべての Z バッファーへのハンドルを指定します。

 

 





