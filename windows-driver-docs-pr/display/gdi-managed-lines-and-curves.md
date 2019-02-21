---
title: GDI で管理された直線と曲線
description: GDI で管理された直線と曲線
ms.assetid: 1a7625ec-6994-488c-a722-cf436a83e213
keywords:
- レンダリング エンジンの GDI WDK Windows 2000 の表示
- グラフィックス ドライバー WDK Windows 2000 の表示、レンダリング エンジン
- 描画の WDK GDI レンダリング エンジン
- WDK GDI のレンダリング エンジン
- WDK GDI の行
- GDI WDK Windows 2000 の表示、行
- グラフィックス ドライバー WDK Windows 2000 の表示、行
- WDK の GDI や線の描画
- GDI WDK Windows 2000 の表示、曲線
- グラフィックス ドライバー WDK Windows 2000 の表示、曲線
- WDK GDI、曲線の描画
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 737e734d23f1ab355bb2ad16ef0f2812215e46e5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550434"
---
# <a name="gdi-managed-lines-and-curves"></a>GDI で管理された直線と曲線


## <span id="ddk_gdi_managed_lines_and_curves_gg"></span><span id="DDK_GDI_MANAGED_LINES_AND_CURVES_GG"></span>


GDI は、直線と曲線の強化された定義を提供します。 Microsoft Windows の場合は true としてでした、デバイス座標の整数のエンドポイントに行が必要はありません 3.x です。 これにより、総丸めなしのグラフィック オブジェクトを変換するドライバーができます。 GDI では、基本的な曲線は楕円ベジエ曲線 (立方スプライン) です。 ベジエ曲線は、多くのハイエンド デバイスでサポートされると、すべての GDI の内部操作が処理されます。 デバイスのベジエ曲線を処理しない場合、GDI 分割曲線を直線セグメントにで描画するドライバーを呼び出す前にします。

GDI は、四角形と同様に、パスの形式で格納する領域をダウンロードできます。 ドライバーは、台形またはいっぱいになるのために spans にパスを分解することができます。

 

 





