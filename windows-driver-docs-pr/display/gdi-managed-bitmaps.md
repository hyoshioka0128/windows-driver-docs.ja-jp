---
title: GDI で管理されたビットマップ
description: GDI で管理されたビットマップ
ms.assetid: 4b575574-7090-4010-962b-80cac059bfa5
keywords:
- レンダリング エンジンの GDI WDK Windows 2000 の表示
- グラフィックス ドライバー WDK Windows 2000 の表示、レンダリング エンジン
- 描画の WDK GDI レンダリング エンジン
- WDK GDI のレンダリング エンジン
- ビットマップ、GDI WDK Windows 2000 の表示
- ビットマップ グラフィックス ドライバー WDK Windows 2000 の表示
- WDK GDI、ビットマップの描画
- WDK GDI ビットマップ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce336f19ea9ecf5376ee974ede0b2963b149cff4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556993"
---
# <a name="gdi-managed-bitmaps"></a>GDI で管理されたビットマップ


## <span id="ddk_gdi_managed_bitmaps_gg"></span><span id="DDK_GDI_MANAGED_BITMAPS_GG"></span>


GDI ビットマップのすべての管理*DIB*など、1、4、8、16、24、および 32 ビット/ピクセル形式。 GDI できるすべての線の描画入力、テキスト出力、およびビット ブロック転送 (bitblt) に関する操作を実行のビットマップ。 これにより、ドライバーまたはそのハードウェアは特別なサポートを提供する関数を実装するか、GDI のすべてのグラフィックス レンダリングの操作を行います。

デバイスがある場合、*フレーム バッファー* DIB 形式で GDI 実行できる、フレーム バッファーに直接のいずれかまたはすべてのグラフィックス出力、ドライバーのサイズが減少します。 デバイスが非標準形式フレーム バッファーを使用する場合、ドライバーが必要なすべて実装する必要があります[描画関数](optional-display-driver-functions.md)します。 発生するパフォーマンス コストが、GDI はほとんどの描画機能をシミュレートまだできます: GDI を使用して処理することができますし、コピー元の形式に戻す描画が完了したらする前に、標準の形式のビットマップにピクセルをコピーする必要があります。

 

 





