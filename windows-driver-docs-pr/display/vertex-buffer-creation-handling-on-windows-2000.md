---
title: Windows 2000 での頂点バッファーの作成処理
description: Windows 2000 での頂点バッファーの作成処理
ms.assetid: 4155a4c6-cbac-4a75-8ddf-5983fe5099c6
keywords:
- DirectX 8.0 リリース ノートには Windows 2000 の WDK の表示、頂点バッファー、作成処理
- 頂点バッファーの WDK DirectX 8.0、Windows 2000 での処理の作成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdb5c445d2547351318cf2c365cf6c602966725d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573241"
---
# <a name="vertex-buffer-creation-handling-on-windows-2000"></a>Windows 2000 での頂点バッファーの作成処理


## <span id="ddk_vertex_buffer_creation_handling_on_windows_2000_gg"></span><span id="DDK_VERTEX_BUFFER_CREATION_HANDLING_ON_WINDOWS_2000_GG"></span>


DirectX 8.0 では、DirectX 7.0 でのテクスチャと頂点 (およびインデックス) のバッファーを管理できます。 つまり、頂点バッファーのシステム メモリのコピーが常に維持され、ビデオ メモリ コピーは、その頂点バッファーが実際に必要な場合にのみ割り当てられています。

DDHAL が返す必要がありますいない場合は、ドライバーは、ビデオ メモリ内の頂点バッファーを割り当てられませんが、代わりに、システム メモリ内でバッファーを割り当て、ランタイムが必要です、\_ドライバー\_NOTHANDLED ではなく、DDHAL を返す必要がありますが、\_ドライバー\_処理済みと設定してエラーを示す、 **ddRVal** E の\_失敗します。 場合は、ドライバーは返します DDHAL\_ドライバー\_NOTHANDLED、ランタイムは、ドライバーによって返されるヒープ ビデオ メモリから、画面を割り当てるましょう。 このいずれか失敗して、アプリケーションまたは (これは意図ではない) ローカルまたは非ローカルのビデオ メモリに割り当てられている画面での結果にエラーが返されます。

そのため、ランタイムが自動的にシステム メモリ内での頂点バッファーを割り当てる場合は、設定**ddRVal** e\_失敗し、返す DDHAL\_ドライバー\_処理済みです。

 

 





