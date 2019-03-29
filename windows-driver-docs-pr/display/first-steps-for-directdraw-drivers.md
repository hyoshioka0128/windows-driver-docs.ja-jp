---
title: DirectDraw ドライバーの最初の手順
description: DirectDraw ドライバーの最初の手順
ms.assetid: 0bb00060-7887-447f-a3c9-394ae5ac84db
keywords:
- 描画の WDK DirectDraw、DirectDraw ドライバー
- DirectDraw WDK Windows 2000 の表示、DirectDraw ドライバー
- DirectDraw ドライバー WDK Windows 2000 の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cedcc900ae4de2ff7ff05059d6053ade2e6c1b55
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578032"
---
# <a name="first-steps-for-directdraw-drivers"></a>DirectDraw ドライバーの最初の手順


## <span id="ddk_first_steps_for_directdraw_drivers_gg"></span><span id="DDK_FIRST_STEPS_FOR_DIRECTDRAW_DRIVERS_GG"></span>


DirectDraw 機能を実装するのには既存のドライバーを変更します。 ドライバーが使用できない場合に、DirectDraw 部分 Windows Driver Kit (WDK) のサンプル コードで始まり、ドライバーの初期化、ロックを取得し、作業を反転します。 基本機能から表示パフォーマンスが向上するより強力な機能を追加できます。

DirectDraw を必要とする最小ドライバーの機能は、ロック、ロック解除、およびサーフェスを反転する機能です。 ハードウェア関連の操作をサポートするいると仮定すると、ドライバーのサポートを追加することも blt (ゲーム速度の重要なは、透過的な blt を含む) の拡大、およびビデオ再生の重要なオーバーレイします。

 

 





