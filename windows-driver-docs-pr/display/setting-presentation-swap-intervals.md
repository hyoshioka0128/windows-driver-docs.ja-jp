---
title: プレゼンテーション スワップの間隔の設定
description: プレゼンテーション スワップの間隔の設定
ms.assetid: 01626dbc-d7ac-482a-a07e-0f5ee3ffb05f
keywords:
- DirectX 8.0 WDK Windows 2000 のリリース ノートを表示するレポートの機能
- D3DCAPS8
- プレゼンテーション スワップ間隔 WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 805203a2b95eef4894411d6ac44becd1b5522dfa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390446"
---
# <a name="setting-presentation-swap-intervals"></a>プレゼンテーション スワップの間隔の設定


## <span id="ddk_setting_presentation_swap_intervals_gg"></span><span id="DDK_SETTING_PRESENTATION_SWAP_INTERVALS_GG"></span>


ドライバーは常に設定する必要があります、 **PresentationIntervals** Direct3D ハードウェアの機能を報告する場合に 0 に D3DCAPS8 構造体のメンバー。 ランタイムは、D3DPRESENT し割り当てます\_間隔\_既定値として 1 つの値。 さらに、ランタイム割り当てますの次のプレゼンテーション、ドライバーが機能のビットを指定する方法に応じてスワップ間隔、 **Caps2** D3DCAPS8 のメンバー。

-   場合、ドライバー、DDCAPS2\_ビット FLIPNOVSYNC、ランタイムも設定**PresentationIntervals** D3DPRESENT に\_間隔\_イミディ エイト。

-   ドライバーが、DDCAPS2 を指定する場合\_ビット FLIPINTERVAL、ランタイムも設定**PresentationIntervals** D3DPRESENT に\_間隔\_、2 つの D3DPRESENT\_間隔\_3、および D3DPRESENT\_間隔\_4 つです。

 

 





