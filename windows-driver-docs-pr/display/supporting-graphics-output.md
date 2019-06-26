---
title: グラフィックス出力のサポート
description: グラフィックス出力のサポート
ms.assetid: 2ac9b01d-9dca-44b4-9645-9c5eefb2ef1b
keywords:
- GDI WDK Windows 2000 の表示、グラフィックス出力
- グラフィックス ドライバー WDK Windows 2000 の表示、出力
- 描画の WDK GDI グラフィックス出力
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 814734f90b35c3ccb4a17ae5294af600a22b490c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355538"
---
# <a name="supporting-graphics-output"></a>グラフィックス出力のサポート


## <span id="ddk_supporting_graphics_output_gg"></span><span id="DDK_SUPPORTING_GRAPHICS_OUTPUT_GG"></span>


ドライバーを処理する特定のグラフィックス操作は、描画サーフェイスとハードウェアの機能によって異なります。 サーフェスが標準の形式である場合*DIB*GDI がドライバーでサポートされていないすべての表示操作を処理します。 いずれかをドライバーが接続できる、[描画関数](optional-display-driver-functions.md)とハードウェアのサポートを活用するためにそれらを実装します。

デバイス管理の画面では、ドライバー、する必要があります少なくとも、サポート、グラフィックスの出力関数[ **DrvCopyBits**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcopybits)、 [ **DrvTextOut** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout) 。、および[ **DrvStrokePath**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokepath)します。 必要に応じて、他のグラフィックス出力関数のいずれかをサポートできます。 サポートしている[ **DrvBitBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt)、たとえば、パフォーマンスを向上させることができます。 一部の関数が必要であり、一定レベルの機能で適切な GCAPS フラグを設定してその機能を示すためにデバイスを許可する他のユーザー、 [ **DEVINFO** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdevinfo)構造体。

ドライバーのすべての描画呼び出しは常に単一スレッドで画面の種類に関係なくです。

以下のトピックでは、ドライバーが、次の操作を実装する方法について説明します。

[描画の直線と曲線](drawing-lines-and-curves.md)

[描画とパスを入力](drawing-and-filling-paths.md)

[ビットマップのコピー](copying-bitmaps.md)

[ハーフトーン](halftoning.md)

[イメージ カラーの管理](image-color-management.md)

 

 





