---
title: コマンド バッファーと頂点バッファー
description: コマンド バッファーと頂点バッファー
ms.assetid: e23013d2-d545-42e5-9787-e4a90921153b
keywords:
- コマンドバッファー WDK Direct3D
- 頂点バッファー WDK Direct3D
- WDK Direct3D のバッファー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 605b3c56c0786642b4b1a02eaf5a4daf90e408f0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839803"
---
# <a name="command-and-vertex-buffers"></a>コマンド バッファーと頂点バッファー


## <span id="ddk_command_and_vertex_buffers_gg"></span><span id="DDK_COMMAND_AND_VERTEX_BUFFERS_GG"></span>


[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) DDI では、コマンドバッファーと頂点バッファーという2種類のバッファーを使用します。 コマンドバッファーには、実行バッファーと同様の構造で、命令の後にデータが含まれます。 コマンドバッファーには、インデックス付きのプリミティブなプリミティブと、場合によってはインライン頂点データを含めることができます。 コマンドバッファーには、API レベルの実行バッファーまたは Direct3D 内部コマンドバッファーのいずれかを指定できます。 メイン入力構造の詳細については、「 [**D3DHAL\_DRAWPRIMITIVES2DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_drawprimitives2data)」を参照してください。

内部コマンドバッファーを使用すると、ドライバーはメモリを割り当て、マルチバッファリングを行うことができます。 内部コマンドバッファーは書き込み専用です。 命令の形式は、 [**D3DHAL\_DP2COMMAND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2command)で確認できます。

D3DHALDP2\_USERMEMVERTICES フラグが設定されている場合、頂点バッファーはユーザーメモリポインターによって指定されます。 それ以外の場合、頂点バッファーは、API レベルの実行バッファー、内部の暗黙的な頂点バッファー、または API レベルの頂点バッファーとして使用できる DirectDrawSurface です。

頂点バッファー API は、頂点バッファーの作成、破棄、ロック、ロック解除を行うことができます。また、 **IDirect3DVertexBuffer7::P Roの頂点**メソッドを使用して、コピー元のバッファーからコピー先のバッファーに頂点を処理できます。 **IDirect3DDevice7::D rawprimitivevb**メソッドと**IDirect3DDevice7::D rawindexedprimitivevb**メソッドは、API レベルの主要な呼び出しです。 頂点バッファーは最適化することもできますが、最適化された頂点バッファーをロックすることはできません。 これら3つの方法の説明については、Direct3D SDK のドキュメントを参照してください。

 

 





