---
title: コマンド バッファーと頂点バッファー
description: コマンド バッファーと頂点バッファー
ms.assetid: e23013d2-d545-42e5-9787-e4a90921153b
keywords:
- コマンド バッファー WDK Direct3D
- 頂点バッファー WDK Direct3D
- WDK Direct3D バッファー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7560faa0a27216251438b8697d885b1b3ddcd365
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343035"
---
# <a name="command-and-vertex-buffers"></a>コマンド バッファーと頂点バッファー


## <span id="ddk_command_and_vertex_buffers_gg"></span><span id="DDK_COMMAND_AND_VERTEX_BUFFERS_GG"></span>


[ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704) DDI は、2 種類のバッファーを使用: コマンド バッファーと頂点バッファー。 コマンド バッファーには、手順後に、execute バッファーと同じ構造内のデータにはが含まれています。 コマンド バッファーには、インデックスとインデックスなしのプリミティブと、場合によっては、インラインの頂点のデータが含まれます。 コマンド バッファーは、どちらの API レベルは、バッファーまたは Direct3D 内部コマンド バッファーを実行できます。 主な入力構造については、次を参照してください。 [ **D3DHAL\_DRAWPRIMITIVES2DATA**](https://msdn.microsoft.com/library/windows/hardware/ff545957)します。

内部コマンド バッファーと、ドライバーは、メモリを割り当てるし、multibuffering を行うことができます。 内部コマンド バッファーは、書き込み専用です。 命令の形式で確認できます[ **D3DHAL\_DP2COMMAND**](https://msdn.microsoft.com/library/windows/hardware/ff545454)します。

場合、D3DHALDP2\_USERMEMVERTICES フラグを設定すると、頂点バッファーがユーザー メモリのポインターで指定します。 それ以外の場合、頂点バッファーは、API レベル実行バッファーや内部の暗黙的な頂点バッファーでは、API レベルの頂点バッファーにできる DirectDrawSurface です。

API を作成できる、頂点バッファーを破棄、ロックし、頂点バッファーのロックを解除および使用できる、 **IDirect3DVertexBuffer7::ProcessVertices**変換先のバッファーをソースから頂点を処理するメソッド。 **IDirect3DDevice7::DrawPrimitiveVB**と**IDirect3DDevice7::DrawIndexedPrimitiveVB**メソッドは、プライマリ API レベルの呼び出し。 頂点バッファーを最適化することが最適化された頂点バッファーをロックすることはできません。 これら 3 つのメソッドの説明については、Direct3D SDK のドキュメントを参照してください。

 

 





