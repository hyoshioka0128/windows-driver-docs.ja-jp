---
title: ハードウェアのエミュレーション層
description: ハードウェアのエミュレーション層
ms.assetid: 79ca4e7f-f335-4e71-8abb-811d98976cc9
keywords:
- WDK DirectDraw、ハードウェア エミュレーション レイヤーの描画
- DirectDraw WDK Windows 2000 の表示、ハードウェアのエミュレーション層
- ハードウェアのエミュレーション層 WDK DirectDraw
- HEL WDK DirectDraw
- WDK DirectDraw のエミュレーション
- 透過的な blt WDK DirectDraw
- 機能は、WDK DirectDraw をビットします。
- bits WDK DirectDraw の上限を設定します。
- サーフェスの WDK DirectDraw、機能ビット
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6030bbe421152dad292196fadfff694bc6a5342f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550070"
---
# <a name="hardware-emulation-layer"></a>ハードウェアのエミュレーション層


## <span id="ddk_hardware_emulation_layer_gg"></span><span id="DDK_HARDWARE_EMULATION_LAYER_GG"></span>


DirectDraw ハードウェアのエミュレーション層 (HEL) では、DirectDraw ドライバーのエミュレーションを実行します。 (DirectDraw の一部としてマイクロソフトによって作成された) HEL では、ユーザー モードでこのエミュレーションを実行します。

たとえば、DirectDraw ドライバーには、機能が含まれている場合 (*cap*) blt のビットが設定が、透過的な転送、DirectDraw ドライバーは呼び出されません blt および透過的な転送 HEL の。 透過的な blt では、場合、HEL の表示のメモリ ポインターが渡されます、色キーをバッキング画面から各バイトを比較します。 バイトにカラー キーが一致しない場合、HEL はこれを CPU を使用して宛先表面にコピーします。 このエミュレーションにもサポートされていないその他の操作の発生またはかどうか、カードの表示メモリ不足です。

DirectDraw では、DirectDraw ドライバーに失敗した操作は、HEL に渡されません。 HEL または DirectDraw ドライバーには、特定の操作が失敗した場合、エラー コードは、アプリケーションに返されます。

 

 





