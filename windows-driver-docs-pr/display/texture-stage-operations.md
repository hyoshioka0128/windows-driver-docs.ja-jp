---
title: テクスチャ ステージの操作
description: テクスチャ ステージの操作
ms.assetid: da2213bb-41f1-440b-8f69-19f69e739954
keywords:
- 複数のテクスチャ WDK Direct3D テクスチャ ステージ
- WDK Direct3D のテクスチャ
- テクスチャ管理 WDK Direct3D、ステージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7020feff0a5f9706d4d7e2229f6f77ac95693321
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581120"
---
# <a name="texture-stage-operations"></a>テクスチャ ステージの操作


## <span id="ddk_texture_stage_operations_gg"></span><span id="DDK_TEXTURE_STAGE_OPERATIONS_GG"></span>


アプリケーションを呼び出してのテクスチャのブレンド操作を実行します、 **IDirect3DDevice7::SetTextureStageState**メソッド。 複数のテクスチャのブレンド操作は、一連のテクスチャのブレンド単位の段階によって実行されます。 これらの各は、さまざまなテクスチャのブレンド パラメーターで選択されている操作を実行する個別にプログラミングすることができます。 説明については**IDirect3DDevice7::SetTextureStageState**、Direct3D SDK のドキュメントを参照してください。

Direct3D では、各描画の段階で導入される 1 つ以上のテクスチャを指定するためのメカニズムは提供されません。 パイプラインでは、テクスチャのステージの間に発生する彩度が定義されているが、各ステージではできるだけ遅く発生する必要があります。

次の操作は、D3DTEXTUREOP で列挙されますが PC98 互換性コンプライアンス必要です。

-   D3DTOP\_を無効にします。

-   D3DTOP\_SELECTARG1, D3DTOP\_SELECTARG2

-   D3DTOP\_変調

-   D3DTOP\_追加

-   D3DTOP\_BLENDTEXTUREALPHA

既定値は D3DTOP\_、第 1 段階で変調と D3DTOP\_の他のすべてのステージを無効にします。 D3DTOP\_変調が旧バージョンと互換性のため、第 1 段階の使用しますが、既定では、すべてのテクスチャ リングする必要がありますを無効にします。

 

 





