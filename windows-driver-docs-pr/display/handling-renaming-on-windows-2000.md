---
title: Windows 2000 での名前変更の処理
description: Windows 2000 での名前変更の処理
ms.assetid: d8f533f8-3037-47c0-986b-bd283bb3804d
keywords:
- DirectX 8.0 WDK Windows 2000 のリリース ノートを表示する頂点バッファー、Windows 2000 で名前を変更します。
- 頂点バッファーの WDK DirectX 8.0、Windows 2000 で名前を変更します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6395e2ecd2df7d8f82efc80e4562d6c536062f0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365935"
---
# <a name="handling-renaming-on-windows-2000"></a>Windows 2000 での名前変更の処理


## <span id="ddk_handling_renaming_on_windows_2000_gg"></span><span id="DDK_HANDLING_RENAMING_ON_WINDOWS_2000_GG"></span>


頂点を正しく実行するためには名前を変更するバッファーがの特性を理解する重要な**fpVidMem** Windows 2000 以降では、画面のグローバル オブジェクトに格納されたポインター。 解釈**fpVidMem**サーフェスが格納されているメモリの種類によって異なります。 システムと非ローカルの両方のビデオ メモリ (AGP) サーフェス、 **fpVidMem**サーフェスを所有しているプロセスのユーザー モード アドレス空間に直接のポインターです。

ローカルのビデオ メモリ サーフェスでは、 **fpVidMem**ビデオ メモリの先頭からのオフセットです。 これをユーザー モードのポインターに変換をユーザー モード プロセスにマップされているビデオ メモリのベース アドレスを追加する必要があります。 このベース アドレスが記載されて、 **fpProcess**特定のプロセスの DirectDraw ローカル オブジェクトのフィールド。

**FpVidMem**このユーザー モードのポインターを生成するための手段はやや複雑なビデオ メモリの非ローカルの画面がユーザー モードのポインターだけです。 Windows 2000 のカーネルが AGP ヒープし、サーフェスの割り当てを管理を維持する方法を理解する必要があります。 最初の重要な点が、非ローカル ヒープの場合、カーネルによって管理されるヒープの開始アドレスできない可能性があります、ヒープの実際のアドレス空間には 実際には、通常、そのヒープから割り当てが有効なことはできないことを確認するように設計、数値のオフセットを**NULL** (0) のアドレス。

実際のアドレス空間に対応していない概念のアドレス空間内に存在するとしてヒープ AGP の考慮すると役立つ場合があります。 **FpStart** AGP、ヒープのフィールドは、この概念のアドレス空間内のヒープのベース アドレス。 AGP のヒープから割り当てられたサーフェスがさらに、 **fpHeapOffset**もこの概念のアドレス空間にあります。 したがって、 **fpHeapOffset**この概念のヒープのベースからのオフセットは、ヒープ自体の開始からのオフセットではありません。 さらに、実際のアドレス空間へのポインターではありません。 サーフェスのメモリにアクセスするユーザー モード プロセスで**fpHeapOffset** (ポインターの算術演算) を通じてユーザー モード プロセスのアドレス空間に割り当てる必要があります。 サーフェスを作成すると、カーネルは、以下に示す数式に従ってこのマッピングを実行します。

サーフェスの指定 (**pSurface**)、カーネル モード AGP ヒープ (**pvmHeap**) と特定のユーザー モード プロセスにヒープのマッピング (**pMap**)、次の数式を使用する実際、ユーザー モードのコンピューティング**fpVidMem**サーフェスの場合。

```cpp
fpVidMem = pMap->pvVirtAddr +
    (pSurface->fpHeapOffset âˆ’ pvmHeap->fpStart)
```

**pvVirtAddr**は、特定のプロセスに AGP ヒープのユーザー モードのマッピングのベース アドレスです。 **fpStart**上記で説明した概念のアドレス空間に AGP ヒープのベースのオフセットと**fpHeapOffset**同じ概念のアドレス空間のベースから画面の開始のオフセットです。

AGP の概念のベース アドレスには、ドライバーが通知されるヒープを通じて、 [ **DdGetDriverInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff549404)コールバック。 ときに*DdGetDriverInfo* GUID を使用して呼び出した\_UpdateNonLocalHeap、 **fpGARTLin**渡されたデータの構造体のフィールドは、同じ値として**fpStart**、つまり、AGP の開始のベース アドレスは、概念のアドレス空間でヒープします。 ドライバーの値の通知されず、残念ながら**pvVirtAddr**ドライバーに渡されたデータ構造体のいずれかを使ってドライバーに表示されていないとします。 そのため、その値がから計算されるように、 **fpVidMem**初期作成する方法、頂点バッファーのカーネルによって計算します。 指定された、 **fpVidMem**現在を差し引くだけで、カーネルによって計算された、 **fpHeapOffset**ヒープの少ない**fpStart**します。 指定された、 **fpHeapOffset**の新しい値の名前を変更、頂点バッファーをスワップする新しいメモリの**fpVidMem**簡単に計算することができます。

次のコード フラグメントを示して、新しいコンピューティング**fpVidMem** AGP サーフェス ロックの呼び出しで。

```cpp
// Get the vertex buffer's surface local and global from the
// lock data
LPDDRAWI_DDRAWSURFACE_LCL*pLcl = pLockData->lpDDSurface;
LPDDRAWI_DDRAWSURFACE_GBL*pGbl = pLcl->lpGbl;

// Get heap this vertex buffer was allocated from
LPVVIDEOMEMORY pHeap = pGbl->lpVidMemHeap;

// Get the current fpVidMem for the vertex buffer
FLATPTR fpCurrentVidMem = pGbl->fpVidMem;

// Compute the virtual base address of the mapping of this AGP
// into the process owning this vertex buffer.
FLATPTR pvVirtAddr = fpCurrentVidMem âˆ’
                     (pGbl->fpHeapOffset âˆ’ pHeap->fpStart);

// Given the fpHeapOffset of the nonlocal video memory to be
// swapped into the new vertex buffer compute the new fpVidMem
// as follow
FLATPTR fpNewVidMem = pvVirtAddr + (fpNewHeapOffset âˆ’ pHeap->fpStart);

// Now store the new fpVidMem in the surface global object and
// also in the lock data.
pGbl->fpHeapOffset = fpNewHeapOffset;
pGbl->fpVidMem = fpNewVidMem;
pLockData->lpSurfData = fpNewVidMem;

// Return success and driver handled
pLockData->ddRVal = DD_OK;
return DDHAL_DRIVER_HANDLED;
```

非ローカルのビデオ メモリをユーザー モード プロセスにアクセスできるように、ユーザー モード プロセスにマップおよびコミットされるメモリの必要があります。 頂点バッファーの名前変更が実行されているときにこれ行われることを確認することが重要ですを使用して、頂点バッファーの新しいメモリを割り当てることが、**への Eng * * * Xxx*関数[ **HeapVidMemAllocAligned**](https://msdn.microsoft.com/library/windows/hardware/ff567267). これは、メモリがコミットされ、使用する前にマップされていることを保証します。 **HeapVidMemAllocAligned**として使用できる、AGP ヒープと、そのため、このポインターの概念のアドレス空間へのオフセットを返します、 **fpHeapOffset**直接します。

場合は、ドライバーは返します DDHAL\_ドライバー\_AGP サーフェイス カーネル コードのロックの値を返しますの処理**lpSurfData**で、 [ **DD\_LOCKDATA**](https://msdn.microsoft.com/library/windows/hardware/ff551637)ランタイムとアプリケーションのデータ構造体。 場合は、ドライバーは返します DDHAL\_ドライバー\_NOTHANDLED カーネルは、単の値を返します**fpVidMem**ユーザー モードにします。 したがって、DDHAL を返す必要はありません\_ドライバー\_限り処理済み**fpVidMem**新しいユーザー モードのポインターをポイントするように更新します。 ただし、ことをお勧め、ドライバーが両方とも設定**fpVidMem**と**lpSurfData**戻って DDHAL\_ドライバー\_処理済みです。

 

 





