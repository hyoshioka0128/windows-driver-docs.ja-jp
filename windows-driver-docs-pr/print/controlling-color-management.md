---
title: 色の管理を制御します。
description: 色の管理を制御します。
ms.assetid: cb210b8d-fee1-4904-8c50-f03d2445085e
keywords:
- 色の管理 WDK の印刷を制御します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 765943a92ff35b77d246b574114c0999c78d139e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549455"
---
# <a name="controlling-color-management"></a>色の管理を制御します。





プリンターの色の管理は、アプリケーション、システム (GDI)、ドライバー、またはデバイスのハードウェアで制御できます。 内のフラグを調べることでどのコンポーネントが色補正を管理するドライバーを決定します、 [ **BRUSHOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff538261)と[ **XLATEOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff570634)グラフィックス DDI 描画関数の実装に渡される構造体。 次のフラグが定義されています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Flag</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>BRUSHOBJ で BR_DEVICE_ICM</p>
<p>XLATEOBJ で XO_DEVICE_ICM</p></td>
<td><p>色の管理は、ドライバーまたはデバイスで実行されています。</p></td>
</tr>
<tr class="even">
<td><p>BRUSHOBJ で BR_HOST_ICM</p>
<p>XO_HOST_ICM in XLATEOBJ</p></td>
<td><p>色の管理は、アプリケーションやシステム (GDI) で実行されています。</p></td>
</tr>
</tbody>
</table>

 

次のトピックでは、これらの色の管理シナリオのドライバー サポートについて説明します。

[システム コントロール](system-control.md)

[ドライバーの制御とデバイスの制御](driver-control-and-device-control.md)

[CMYK カラー領域をサポートしています。](supporting-cmyk-color-space.md)

[JPEG や PNG 画像の色の管理](color-management-of-jpeg-and-png-images.md)

 

 




