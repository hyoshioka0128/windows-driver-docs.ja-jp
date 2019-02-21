---
title: マルチ サンプリングのレンダリング
description: マルチ サンプリングのレンダリング
ms.assetid: 7c21b0e0-bdd3-4de3-a5c5-5adc2d2e2b33
keywords:
- DirectX 8.0 リリース ノート Windows 2000 の WDK 表示、マルチ サンプリングのレンダリング
- マルチ サンプリング WDK DirectX 8.0 のレンダリング
- multisamples WDK DirectX 8.0 のレンダリング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac2985f20054db932b8ab2bfe9d32dec00117cdb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527220"
---
# <a name="multisample-rendering"></a>マルチ サンプリングのレンダリング


## <span id="ddk_multisample_rendering_gg"></span><span id="DDK_MULTISAMPLE_RENDERING_GG"></span>


DirectX 8.0 では、サンプル アプリケーションの管理下にあるピクセルあたりの数を使用したマルチ サンプリングのレンダリングのサポートについて説明します。 **IDirect3DDevice8**インターフェイスの操作ウィンドウ表示モードと全画面表示の両方でのマルチ サンプリングをサポートしています。 さらに、バックエンド (フレーム バッファー) から直接、または (特別なフリップまたは blt 呼び出し) を使用して、フロント エンドでピクセルにサンプルの処理を実行するハードウェアをサポートするための十分な柔軟性があります。詳細については**IDirect3DDevice8**、DirectX 8.0 のドキュメントを参照してください。

 

 





