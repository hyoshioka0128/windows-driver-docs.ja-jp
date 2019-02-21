---
title: 属性の GDI で管理されたブラシ
description: 属性の GDI で管理されたブラシ
ms.assetid: 8ca38ba1-824d-45be-9039-13222d3400c3
keywords:
- レンダリング エンジンの GDI WDK Windows 2000 の表示
- グラフィックス ドライバー WDK Windows 2000 の表示、レンダリング エンジン
- 描画の WDK GDI レンダリング エンジン
- WDK GDI のレンダリング エンジン
- GDI WDK Windows 2000 の表示、パターン
- グラフィックス ドライバー WDK Windows 2000 の表示、パターン
- WDK GDI のパターン
- WDK GDI ブラシします。
- ブラシ WDK GDI の実現
- WDK GDI を描画ブラシします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57544d900f40aaf1a09b69a958edcd86ae9b04e2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530858"
---
# <a name="gdi-managed-attributes-brushes"></a>GDI マネージ属性:ブラシ


## <span id="ddk_gdi_managed_attributes_brushes_gg"></span><span id="DDK_GDI_MANAGED_ATTRIBUTES_BRUSHES_GG"></span>


GDI では、すべての属性も管理します。 GDI によってドライバーにブラシとして属性が渡されます。ドライバー*ことに気付きました*便利な内部形式に変換して、これらのブラシ。 GDI は、このドライバーの変換後の情報を保持します。 GDI では、境界、相関関係、現在の位置、線のスタイルなど、ブラシのすべての状態も保持されます。 ドライバーは、情報をキャッシュできますが、いずれかの状態を維持するためには、想定されません。 初期化とブラシの実現、以外は、GDI は、デバイス上に描画するためにのみ、ドライバーを呼び出します。 GDI、領域、ロック変換の処理と*ポインター除外*ドライバーを呼び出す前にします。

ドライバーは、実現されていないブラシを使用する必要があるときに、呼び出して GDI します。 GDI では、ブラシのメモリを割り当てるし、それを実現し、必要に応じて、ディザーにドライバーを呼び出し。

 

 





