---
title: オーバーレイのサポート
description: オーバーレイのサポート
ms.assetid: 325a08b2-c357-49b7-a9c3-878c44bc2d26
keywords:
- 図面ページ WDK DirectDraw、オーバーレイのサーフェスを反転します。
- Windows 2000 の WDK の表示を切り替える DirectDraw サーフェスのオーバーレイ
- WDK DirectDraw、オーバーレイのサーフェスの反転 ページ
- WDK DirectDraw を反転するには、サーフェスをオーバーレイします。
- サーフェス WDK DirectDraw をオーバーレイします。
- サーフェス WDK DirectDraw、オーバーレイします。
- WDK の DirectDraw を画面の回転
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bfb67c70958b55682303b6bc4b7e723d9eb6e68
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558518"
---
# <a name="overlay-support"></a>オーバーレイのサポート


## <span id="ddk_overlay_support_gg"></span><span id="DDK_OVERLAY_SUPPORT_GG"></span>


DirectDraw には、オーバーレイもサポートしています。 *オーバーレイ画面*は、その下にある画面で、物理ビットを変更することがなく、プライマリの画面の上部に表示されることができます。 オーバーレイでは、レジスタ、オーバーレイの画面を含むプライマリ画面上の四角形を定義する設定されます。 アナログ デジタル コンバーター (DAC) では、四角形の場所を変更します。 スキャン ラインは、オーバーレイの確保を示す四角形に達するまで、surface、プライマリ メモリ内のデータを読み取ります。 オーバーレイでは、その行が完了したら、元のプライマリ画面イメージを続行するまで、オーバーレイの画面から読み取ります。 これは、プライマリ画面から、オーバーレイへの切り替え戻るスキャン ラインのすべてのパスで行われます、オーバーレイが完全に表示されるまで継続されます。

オーバーレイ画面には、プライマリ画面よりも別のピクセルの深度を持つことができます。 たとえば、8 ビット/ピクセル (bpp) は、プライマリのサーフェイスでの問題に見えるかもしれませんが、ビデオ クリップには、期待を表示する 16 ビット/ピクセルに必要があります。 ピクセルの深度は、プライマリの画面とオーバーレイの間でシームレスに切り替わります。 DirectDraw でのオーバーレイの詳細については、次を参照してください。、 [DirectX の拡張機能のビデオ ポート](video-port-extensions-to-directx.md)セクション。

オーバーレイは、プライマリの画面とまったく同じ方法で反転します。 DirectDraw surface オブジェクトは、スキャン ラインがオーバーレイを外接する四角形に達したとき新しいオーバーレイ サーフェイスが読み込まれるように、ポインターを交換します。 説明されている同じフリッピング アルゴリズム[タイミング、反転](timing-a-flip.md)解除を行うようにします。

 

 





