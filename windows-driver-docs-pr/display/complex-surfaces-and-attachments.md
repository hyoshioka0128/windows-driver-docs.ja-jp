---
title: 複合サーフェスおよび添付ファイル
description: 複合サーフェスおよび添付ファイル
ms.assetid: fb75c534-b1ff-44d3-a8dc-dcf0f221b6ad
keywords:
- 描画サーフェイス WDK DirectDraw、複雑です
- DirectDraw サーフェス WDK Windows 2000 を表示する複雑です
- サーフェス WDK DirectDraw、複雑です
- 複雑なサーフェス WDK DirectDraw
- サーフェス WDK DirectDraw、添付ファイル
- 描画サーフェイス WDK DirectDraw、添付ファイル
- DirectDraw サーフェスの WDK Windows 2000 の表示、添付ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04f6fe1cf0643d10488e9bf23a7504b8751f4187
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572648"
---
# <a name="complex-surfaces-and-attachments"></a>複合サーフェスおよび添付ファイル


## <span id="ddk_complex_surfaces_and_attachments_gg"></span><span id="DDK_COMPLEX_SURFACES_AND_ATTACHMENTS_GG"></span>


サーフェスは、*複雑な*、関連付けられているサーフェスの大きなコレクションの一部であることを意味します。 キューブのさまざまな面をマップおよびフロント バッファーと関連付けられているバック バッファー、MIP マップのさまざまなレベルに複雑な面の例が含まれます。

DirectDraw ランタイムと呼ばれる概念を使用して*添付ファイルのサーフェス*複雑なサーフェスに別の単純なサーフェイスのリンクを管理します。 サーフェスを暗黙的に、アプリケーションが 1 回の呼び出しを行うときに接続できる**IDirectDraw7::CreateSurface** (フロント バッファーと考えられる Z バッファーをバック バッファー) の反転のチェーンを構築する場合と同様、明示的にまたはアプリケーションレンダー ターゲットを呼び出すことで Z バッファーを関連付けます**IDirectDrawSurface7::AddAttachedSurface**します。

 

 





