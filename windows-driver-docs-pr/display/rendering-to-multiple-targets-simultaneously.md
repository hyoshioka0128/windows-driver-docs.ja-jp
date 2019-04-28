---
title: 複数ターゲットへの同時レンダリング
description: 複数ターゲットへの同時レンダリング
ms.assetid: 72c56ea6-d5da-420a-91f4-c7fa09daf67e
keywords:
- 複数のターゲット WDK DirectX 9.0 のレンダリング
- 複数のレンダー ターゲット WDK DirectX 9.0
- 同時のレンダー ターゲット WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 274a1282a81fdcaef07cde5fc8f3871ee8ef4a6a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379840"
---
# <a name="rendering-to-multiple-targets-simultaneously"></a>複数ターゲットへの同時レンダリング


## <span id="ddk_rendering_to_multiple_targets_simultaneously_gg"></span><span id="DDK_RENDERING_TO_MULTIPLE_TARGETS_SIMULTANEOUSLY_GG"></span>


バージョンのドライバーに表示できる複数のターゲットに同時に、ドライバーは、そのデバイスをサポートしていることを示す場合複数 DirectX 9.0 はレンダー ターゲットです。 デバイスをサポートするためのレンダー ターゲットの数を示すために、ドライバー設定で数値、 **NumSimultaneousRTs** D3DCAPS9 構造体のメンバー。 単一のターゲットへのレンダリングがサポートされている場合のみ、ドライバーを 1 にこの数を設定する必要があります。 ドライバーへの応答で D3DCAPS9 構造体を返す、 **GetDriverInfo2** 」の説明に従って D3DCAPS8 構造体を返すにする方法と同様にクエリ[DirectX 8.0 スタイル Direct3D の機能を Reporting](reporting-directx-8-0-style-direct3d-capabilities.md)します。 このクエリのサポートについては、「[サポート GetDriverInfo2](supporting-getdriverinfo2.md)します。

レンダー ターゲットで複数のレンダリング ターゲット グループは同一の次元を持つ必要がありますが、さまざまな表面の形式を持つことができます。

ドライバーの受信、D3DDP2OP\_SETRENDERTARGET2 オペレーション コード、複数のグループで、レンダー ターゲットのいずれかの色のバッファーを設定するアプリケーションが要求した場合。

DirectX 9.0 ドライバーでは、同時に複数のターゲットの表示をサポートする場合、特定の機能をサポートする必要があり、拡張機能をサポートすることができます。 次のトピックでは、これらの必須および省略可能な機能について説明します。

[複数のレンダー ターゲットに対して必要な機能](required-features-for-multiple-render-targets.md)

[レンダー ターゲットで複数のオプションの機能](optional-features-for-multiple-render-targets.md)

 

 





