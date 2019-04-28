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
ms.openlocfilehash: 7c204a83447a8f64cdbc14b76552da3f729024a5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372757"
---
# <a name="supporting-graphics-output"></a>グラフィックス出力のサポート


## <span id="ddk_supporting_graphics_output_gg"></span><span id="DDK_SUPPORTING_GRAPHICS_OUTPUT_GG"></span>


ドライバーを処理する特定のグラフィックス操作は、描画サーフェイスとハードウェアの機能によって異なります。 サーフェスが標準の形式である場合*DIB*GDI がドライバーでサポートされていないすべての表示操作を処理します。 いずれかをドライバーが接続できる、[描画関数](optional-display-driver-functions.md)とハードウェアのサポートを活用するためにそれらを実装します。

デバイス管理の画面では、ドライバー、する必要があります少なくとも、サポート、グラフィックスの出力関数[ **DrvCopyBits**](https://msdn.microsoft.com/library/windows/hardware/ff556182)、 [ **DrvTextOut** ](https://msdn.microsoft.com/library/windows/hardware/ff557277) 。、および[ **DrvStrokePath**](https://msdn.microsoft.com/library/windows/hardware/ff556316)します。 必要に応じて、他のグラフィックス出力関数のいずれかをサポートできます。 サポートしている[ **DrvBitBlt**](https://msdn.microsoft.com/library/windows/hardware/ff556180)、たとえば、パフォーマンスを向上させることができます。 一部の関数が必要であり、一定レベルの機能で適切な GCAPS フラグを設定してその機能を示すためにデバイスを許可する他のユーザー、 [ **DEVINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff552835)構造体。

ドライバーのすべての描画呼び出しは常に単一スレッドで画面の種類に関係なくです。

以下のトピックでは、ドライバーが、次の操作を実装する方法について説明します。

[描画の直線と曲線](drawing-lines-and-curves.md)

[描画とパスを入力](drawing-and-filling-paths.md)

[ビットマップのコピー](copying-bitmaps.md)

[ハーフトーン](halftoning.md)

[イメージ カラーの管理](image-color-management.md)

 

 





