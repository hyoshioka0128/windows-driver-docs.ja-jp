---
title: Direct3D サーフェイス ハンドル
description: Direct3D サーフェイス ハンドル
ms.assetid: cefede2e-3e82-4de3-ae49-4982578fd2fe
keywords:
- コンテキスト WDK Direct3D サーフェイスを処理します。
- 画面は、WDK Direct3D を処理します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6de7eb01e57cbe98153f9c4708df9b32ab3cf2e5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384863"
---
# <a name="direct3d-surface-handles"></a>Direct3D サーフェイス ハンドル


## <span id="ddk_direct3d_surface_handles_gg"></span><span id="DDK_DIRECT3D_SURFACE_HANDLES_GG"></span>


Microsoft DirectX 7.0 デバイス ドライバー インターフェイス (DDI) は、Direct3D のランタイム コンポーネントとして解析コマンド ストリームの可能なドライバーにコマンドを渡す前にモデルを昇格する設計されています。 さらに、将来のハードウェアで使用できるように、コマンド ストリームをフォーマットする必要があります。

これらの目標に向かう 1 つの重要な変更は、所有する、更新、およびドライバーによって書式設定された構造体に、Direct3D/DirectDraw ランタイムによって所有されている中間構造からすべての画面に関連するデータの移動です。

サーフェスは、コマンド ストリームに埋め込まれているハンドルによって参照されます。 これらの頻度の高い操作で、ドライバーから参照できる、サーフェイスの独自の表現、ハンドルなどのヘルパー関数を使用して、画面のロックを使用しなくても[ **EngLockDirectDrawSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-englockdirectdrawsurface).

これらのハンドルを割り当てるためのメカニズムが呼び出されるドライバーのエントリ ポイント[ **D3dCreateSurfaceEx**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)します。 このエントリ ポイントが、既存の呼び出しの直後と呼ばれる[ *DdCanCreateSurface* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549213(v=vs.85))と[ *DdCreateSurface* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85)) 、エントリ ポイントと後、画面には、ビデオ メモリ アドレスをハンドルを割り当てられています。 **D3dCreateSurfaceEx**時間、ドライバーの表面の構造とサーフェスの構造に、DirectDraw ランタイムのコピーからすべての関連情報をコピーします。 ドライバー側コピーのサイズなどの画面のデータに必要な形式、および**fpVidMem** (のメンバー、 [ **DD\_画面\_GLOBAL** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_global)構造体)。

ハンドルは、デバイスごとに、プロセスごとに一意である、ランタイムが保証されます。 ハンドルは、それぞれのコンテキストで一意であるとは限りませんし、このドライバーでさらに詳しく説明されているいくつかの影響を与えます[ドライバー側画面構造の作成](creating-driver-side-surface-structures.md)です。

対応がない**DestroySurfaceEx**でドライバー側サーフェスの構造が破棄されるため、呼び出す[ *DdDestroySurface* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_destroysurface)時間。

 

 





