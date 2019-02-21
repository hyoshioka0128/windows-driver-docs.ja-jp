---
title: レポートのビデオ メモリ頂点バッファーとインデックス バッファーのサポート
description: レポートのビデオ メモリ頂点バッファーとインデックス バッファーのサポート
ms.assetid: fa0d7dd5-3bed-45db-a946-0761fd631a52
keywords:
- DirectX 8.0 WDK Windows 2000 のリリース ノートを表示するレポートの機能
- D3DCAPS8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b44870279b6357f38d6175e0006d768d17f0f4f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553708"
---
# <a name="reporting-support-for-video-memory-vertex-and-index-buffers"></a>レポートのビデオ メモリ頂点バッファーとインデックス バッファーのサポート


## <span id="ddk_reporting_support_for_video_memory_vertex_and_index_buffers_gg"></span><span id="DDK_REPORTING_SUPPORT_FOR_VIDEO_MEMORY_VERTEX_AND_INDEX_BUFFERS_GG"></span>


DirectX 8.0、ドライバーはまたはビデオ メモリの頂点とインデックス バッファーをサポートしていませんかどうかをランタイムにフラグを設定する 2 つの新しい Direct3D 機能フラグが追加されます。 これらのフラグが作成された、前に、ランタイムが見つかりませんだったかどうか、ドライバー実際をサポートしているビデオ メモリ頂点バッファーかどうか。 したがって、DirectX 8.0 は、execute バッファー (d3d バッファー) の作成と破棄ドライバーのエントリ ポイントをエクスポートする場合 1 つ追加するか、機能の両方のビット D3DDEVCAPS\_HWVERTEXBUFFER と D3DDEVCAPS\_にHWINDEXBUFFER**DevCaps** D3DCAPS8 構造体のフィールドで報告して**GetDriverInfo2**ランタイムにします。 D3DDEVCAPS フラグを設定\_ビデオまたは非ローカルのビデオ メモリ頂点バッファーと D3DDEVCAPS、ドライバーがサポートしている場合、HWVERTEXBUFFER\_HWINDEXBUFFER、ドライバーは、インデックス バッファーのビデオまたは非ローカルのビデオ メモリをサポートしている場合。

ランタイムにこれらの機能ビットのマスク (ランタイム自体にのみアプリケーションにはできません)、アプリケーションに機能を報告します。 そのため、場合でも、それらをエクスポートするには、ドライバーこれらの機能は、DirectX Cap ビューアー アプリケーションに表示されません。

これらの機能の適切なサポートは、Microsoft Windows Hardware Quality Labs (WHQL) テストの一部です。

 

 





