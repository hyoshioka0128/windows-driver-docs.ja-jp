---
title: ドライバー側サーフェス構造の作成
description: ドライバー側サーフェス構造の作成
ms.assetid: d5e2e6ee-8853-4a17-b1c6-48c75474b2b7
keywords:
- コンテキスト WDK Direct3D、ドライバー側サーフェスの構造体
- surface のドライバー側 WDK Direct3D を構造体します。
- D3dCreateSurfaceEx
- サーフェスの WDK DirectDraw、ドライバー側構造体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3782f52d3fcca7a1b8cae772791d5ff48ba5a81
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370208"
---
# <a name="creating-driver-side-surface-structures"></a>ドライバー側サーフェス構造の作成


## <span id="ddk_creating_driver_side_surface_structures_gg"></span><span id="DDK_CREATING_DRIVER_SIDE_SURFACE_STRUCTURES_GG"></span>


DirectDraw ランタイムが呼び出す、ドライバーの[ **D3dCreateSurfaceEx** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)エントリ ポイントを呼び出した後、 [ *DdCreateSurface* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))エントリポイントと、画面に割り当てられたメモリ。 ランタイム呼び出し*D3dCreateSurfaceEx* DDSCAPS でタグ付けされたこれらのサーフェスののみ\_テクスチャ、DDSCAPS\_EXECUTEBUFFER、DDSCAPS\_3DDEVICE、または DDSCAPS\_ZBUFFER フラグ。

呼び出しの前に[ **D3dCreateSurfaceEx**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)ランタイムは、画面へのハンドルとして整数値を割り当てます。 この値は、 **dwSurfaceHandle** 、DDRAWI のメンバー\_DDSURFACE\_多くの構造 (によって示されるよう、 **lpSurfMore** 、DDRAWI のメンバー\_DDSURFACE\_ローカル構造)。 参照してください[ **DD\_画面\_詳細**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_more)と[ **DD\_画面\_ローカル**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_local)、これは、DDRAWI のエイリアスです。\_DDSURFACE\_よりと DDRAWI\_DDSURFACE\_ローカル構造体。

これらの整数値では、1 から開始され、できるだけ小さくして保持されます。 (0 は、サーフェスのハンドルの保証された無効な値です)。目的は、ドライバーが、独自の構造体にポインターの配列を保持できます。 ハンドルを受信するとすぐ (と*D3dCreateSurfaceEx*と呼びます) が配列の末尾を越えるを配列の再割り当てして続行します。 Direct3D ランタイムないハンドル値を渡しますドライバーを使用してドライバーをそのハンドルが表示される前に*D3dCreateSurfaceEx*します。 ただし、ドライバーが範囲外にあるか、解放されたハンドル テーブル内のスロットを参照するハンドル値に十分な堅牢にする必要があります (対象のハンドルは[ *DdDestroySurface* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_destroysurface)されました呼ばれます)。 0 は、保証された無効な値であるためハンドル テーブル内の 0 エントリを再利用できるその他の目的に注意してください。 *Perm3*サンプル ドライバーは、配列の現在の長さを格納する 0 個のエントリを使用します。

**注**   、Microsoft Windows Driver Kit (WDK) に 3 dlabs Permedia3 サンプルのディスプレイ ドライバーが含まれていません (*Perm3.h*)。 Windows Server 2003 SP1 ドライバー開発キット (DDK)、DDK - WDHC web サイトの Windows ドライバー開発キットのページからダウンロードできるこのサンプル ドライバーを取得できます。

 

 

 





