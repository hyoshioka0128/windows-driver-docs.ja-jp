---
title: マルチサンプル サーフェスの作成処理
description: マルチサンプル サーフェスの作成処理
ms.assetid: 78557c9d-b741-4eb9-b8e2-56387cad80c4
keywords:
- DirectX 8.0 リリース ノート Windows 2000 の WDK 表示、multisample 表示、作成します。
- マルチ サンプリング WDK DirectX 8.0 を表示、作成します。
- WDK DirectX multisamples 8.0 では、作成のレンダリング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3205ee3101c9249ffd0061c8d924b06169d4a201
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360374"
---
# <a name="handling-the-creation-of-multisampled-surfaces"></a>マルチサンプル サーフェスの作成処理


## <span id="ddk_handling_the_creation_of_multisampled_surfaces_gg"></span><span id="DDK_HANDLING_THE_CREATION_OF_MULTISAMPLED_SURFACES_GG"></span>


サンプルの数で見つかるマルチ サンプリングされた画面が作成されるときに、 **ddsCapsEx.dwCaps3**の[ **DD\_画面\_詳細**](https://msdn.microsoft.com/library/windows/hardware/ff551737)構造体。 このフィールドは保持 D3DMULTISAMPLE 列挙型の値の 1 つ\_型。 ように、ビット フィールドではない**wFlipMSTypes**または**wBltMSTypes**します。 場合は、画面は、マルチ サンプルではありません**dwCaps3** D3DMULTISAMPLE の値を持つ\_NONE (0)。

かどうか、マルチ サンプリング サーフェイスでの作成要求を満たすことができるかどうかを判断するとき、ドライバーは考慮されません、D3DRS の現在の値\_MULTISAMPLEANTIALIAS が状態を表示します。 ドライバー D3DRS に設定する要求が失敗することはできません\_MULTISAMPLEANTIALIAS **FALSE**します。 そのため、コンテキストのマルチ サンプリングのレンダリングを実行する機能を適用するかに影響が時間を作成することの制限も D3DRS\_MULTISAMPLEANTIALIAS は**FALSE**その時点で。

 

 





