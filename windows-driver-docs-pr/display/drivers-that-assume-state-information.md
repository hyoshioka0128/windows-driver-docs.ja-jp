---
title: 状態情報を前提としているドライバー
description: 状態情報を前提としているドライバー
ms.assetid: c4dfb701-c547-4e94-8fd8-05571508137c
keywords:
- サーフェス WDK DirectDraw、中
- 描画 blt WDK DirectDraw、状態情報
- DirectDraw 中 WDK Windows 2000 の表示、状態情報
- 中 WDK DirectDraw、状態情報
- blt WDK DirectDraw、状態情報
- WDK DirectDraw を状態します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8389c49c4763282bb684e23e66a320e30bf3a0e1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358426"
---
# <a name="drivers-that-assume-state-information"></a>状態情報を前提としているドライバー


## <span id="ddk_drivers_that_assume_state_information_gg"></span><span id="DDK_DRIVERS_THAT_ASSUME_STATE_INFORMATION_GG"></span>


ほとんどは、操作を実行するときに、ブリット機能の状態を設定するドライバーを表示します。 ただし、一部のディスプレイ ドライバーでは、既知の状態にあるブリット機能が予想されます。 たとえば、一部のディスプレイ ドライバーでは、原点が透過的な blt よりも標準 blt 具合に設定されているとします。 このような場合は、状態は、DirectDraw を使用して、後にリセットするのには。

固定の配信元とするか、ソースと宛先表面の別の配信元と、2 つの画面間の転送を実現できます。 ディスプレイ ドライバーが変わらない、配信元が必要ですが、DirectDraw セカンダリ画面へのアクセスに変更した場合、古いポインターを保存して、操作が終了したときに復元する必要があります。

これにより、操作を実行するレジスタを以前の状態に復元できるようにするまで待機 DirectDraw、パフォーマンスが低下します。 これは、非同期から DirectDraw の速度が含まれているためにです。

注意が必要では、このような場合、表示状態に加えられる変更を最小限に抑える。 それ以外の場合のパラメーターを渡すために使用できるスタックのルームを浪費もこのシナリオでは、配信元を移動します。

 

 





