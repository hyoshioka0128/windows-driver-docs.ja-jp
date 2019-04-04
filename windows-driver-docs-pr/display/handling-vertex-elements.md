---
title: 頂点の要素の処理
description: 頂点の要素の処理
ms.assetid: b931b674-f8c4-4852-a66a-97d545059287
keywords:
- 頂点シェーダー宣言 WDK DirectX 9.0、頂点の要素の処理
- シェーダー宣言 WDK DirectX 9.0、頂点の要素の処理
- 頂点要素 WDK DirectX 9.0
- 頂点要素 WDK DirectX 9.0、頂点シェーダーの宣言
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 921f232be4ef716f33b6c803958e41447ed0b00f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551598"
---
# <a name="handling-vertex-elements"></a>頂点の要素の処理


## <span id="ddk_handling_vertex_elements_gg"></span><span id="DDK_HANDLING_VERTEX_ELEMENTS_GG"></span>


DirectX 9.0 バージョンのドライバーが処理できるシェーダー宣言での頂点の要素の数は、ドライバーのデバイスが固定機能やプログラミング可能な頂点の処理をサポートするかどうかによって異なります。 頂点シェーダー宣言の要素の詳細については、[宣言の分離と頂点シェーダーのコード](separating-declarations-and-code-for-vertex-shaders.md)を参照してください。

デバイスは、固定機能の頂点の処理をサポートする場合、ドライバーは、最大 17 頂点要素 (FVF コード) を処理する必要があります。

デバイスは、プログラミング可能な頂点の処理をサポートする場合、ドライバーは最大 64 個の頂点の要素を処理し、使用しないこれらの要素をスキップする必要があります。 各カラー チャネル (最大 4)、入力の頂点シェーダー 3 をサポートするデバイスの (最大 16) を登録するため\_0 と、後で宣言できるとは別に、最大 64 (16 \* 4) 頂点要素が可能です。 この最大数 64 は、D3DDECL から生成される最後の要素を含まない\_エンド マクロ。

 

 





