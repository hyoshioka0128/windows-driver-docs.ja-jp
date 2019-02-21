---
title: 頂点バッファーのコールバックと Windows 2000
description: 頂点バッファーのコールバックと Windows 2000
ms.assetid: d3b92bc9-d4f1-4079-86f1-53c04bcab443
keywords:
- DirectX 8.0 WDK Windows 2000 のリリース ノートを表示する頂点バッファー、コールバック
- 頂点バッファーの WDK DirectX 8.0、コールバックおよび Windows 2000
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6091eb4bb6539f35d864913ec7076b5c1d848b9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550220"
---
# <a name="vertex-buffer-callbacks-and-windows-2000"></a>頂点バッファーのコールバックと Windows 2000


## <span id="ddk_vertex_buffer_callbacks_and_windows_2000_gg"></span><span id="DDK_VERTEX_BUFFER_CALLBACKS_AND_WINDOWS_2000_GG"></span>


Windows 2000 の初期の製品版のリリースでの DirectX 7.0 ドライバーを防止する、ランタイムによって呼び出されているからバッファー (D3D バッファー) のコールバックを実行します。 これにより、また、ドライバーは、頂点バッファーの作成要求の通知を送信できなくなり、そのため、ビデオ メモリ、または非ローカルのビデオ メモリ バッファーを作成またはこのシナリオで使用します。 ビデオ メモリ頂点バッファーと、DirectX 8.0 で DirectX 8.0 で DirectX 7.0 が付属しているのバージョンでは有効です。 さらに、Windows 2000 Service Pack 1 (SP1) により、ビデオ メモリ頂点バッファーと、Windows 2000 の将来のバージョンは、ビデオ メモリ頂点バッファーを有効になります。 ただし、DirectX 8.0 をインストールする以外の Windows 2000 でのビデオ メモリ頂点バッファーを有効にする回避策はありません。

 

 





