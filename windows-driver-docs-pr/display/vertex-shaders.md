---
title: 頂点シェーダー
description: 頂点シェーダー
ms.assetid: dfc421f7-b2fe-4023-a47b-cfd59fe5bdb4
keywords:
- 頂点シェーダー WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a178533248397eb06a2f3c6d6de62ed76710fffc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558625"
---
# <a name="vertex-shaders"></a>頂点シェーダー


## <span id="ddk_vertex_shaders_gg"></span><span id="DDK_VERTEX_SHADERS_GG"></span>


DirectX 8.0 DDI をサポートするすべてのドライバーは、新しい DP2 トークン D3DDP2OP をサポートする必要があります\_SETVERTEXSHADER プログラミング可能な頂点シェーダーは、ハードウェアでサポートされていない場合でもです。 これは、ため D3DDP2OP\_SETVERTEXSHADER はプログラミング可能な頂点の処理だけでなく、固定関数を使用する場合は、頂点データの受信の FVF コードをドライバーに伝達するようするメカニズムです。

D3DDP2OP\_の使用には、現在のプログラミング可能な頂点シェーダーのいずれかのハンドルまたは固定機能の頂点処理の頂点のデータの FVF コードのドライバーに通知する SETVERTEXSHADER を使用できます。 ハンドル領域は、頂点シェーダーは、ランタイムによって管理され、FVF の有効なコードが含まれています。 そのため、頂点シェーダーのハンドルが参照できる、D3DDP2OP によって以前に作成したプログラム可能な頂点シェーダーのハンドルのいずれか\_CREATEVERTEXSHADER DP2 トークン、または頂点の FVF コードには、fixed 関数頂点処理によって処理される書式設定します。

D3DDP2OP、プログラミング可能な頂点の処理をサポートしていないハードウェアのドライバーを処理する必要があります\_SETVERTEXSHADER FVF コードを確認する (ため、実行する処理) 頂点データには、0 のストリームにバインドします。 これは、機能は、メモリ (UM) プリミティブのユーザーを処理するときに特に重要です。 この場合、指定された頂点データの FVF コードを決定する唯一の方法は、D3DDP2OP\_SETVERTEXSHADER トークンです。 ハンドルの最下位ビットは、(1) に設定されている場合、ハンドルが頂点シェーダーのハンドラーです。 最下位ビットがオフ (0) のハンドルの場合は、レガシ FVF コードです。

頂点の FVF コード D3DDP2OP で指定されているとの競合のバッファーする場合\_SETVERTEXSHADER、ドライバーは、頂点バッファーの FVF コードを無視して続行する必要があります。

DirectX のランタイムでは、プログラミング可能な頂点の処理をサポートしていないドライバーを頂点シェーダーのハンドルとして FVF コードのみが渡されることを保証します。 ただし、このようなドライバーには、渡される FVF コードがサポートされていることを確認するデバッグ コードが必要です。

 

 





