---
title: 色の管理を制御する
description: 色の管理を制御する
ms.assetid: cb210b8d-fee1-4904-8c50-f03d2445085e
keywords:
- 色の管理 WDK の印刷を制御します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6efc0ab1515a569ab7839db5836dac80e069d53
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374666"
---
# <a name="controlling-color-management"></a>色の管理を制御する





プリンターの色の管理は、アプリケーション、システム (GDI)、ドライバー、またはデバイスのハードウェアで制御できます。 内のフラグを調べることでどのコンポーネントが色補正を管理するドライバーを決定します、 [ **BRUSHOBJ** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_brushobj)と[ **XLATEOBJ** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_xlateobj)グラフィックス DDI 描画関数の実装に渡される構造体。 次のフラグが定義されています。

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

 

 




