---
title: グラフィックス DDI のフォントおよびテキストの関数のサポート
description: グラフィックス DDI のフォントおよびテキストの関数のサポート
ms.assetid: c8abf3bd-7a5a-4a48-988e-a1de1b426656
keywords:
- フォント WDK グラフィック
- フォント、GDI WDK Windows 2000 の表示
- グラフィックス ドライバー WDK Windows 2000 の表示、フォント
- GDI WDK Windows 2000 の表示、テキスト出力
- グラフィックス ドライバー WDK Windows 2000 の表示、テキスト出力
- テキスト出力 WDK グラフィック
- WDK の GDI やフォントの描画
- WDK GDI の描画、テキスト出力
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3f8d85aad1255505674b5672949cd426fb44d72
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372786"
---
# <a name="supporting-graphics-ddi-font-and-text-functions"></a>グラフィックス DDI のフォントおよびテキストの関数のサポート


## <span id="ddk_supporting_graphics_ddi_font_and_text_functions_gg"></span><span id="DDK_SUPPORTING_GRAPHICS_DDI_FONT_AND_TEXT_FUNCTIONS_GG"></span>


GDI は、多数のデバイスのフォントのすべての関数を処理できます。 一部のドライバーでは、ただしを描画できます独自のフォント、またはデバイスの表面に、デバイスのフォント。 その他のドライバーは、フォント ドライバーは、GDI にグリフ ビットマップやアウトライン、ほかのグリフのメトリックを提供できます。 このような場合は、ドライバーが、いくつかの利用可能なフォント関数をサポートする必要があります。

テキスト出力は、一般的な関数です。 サーフェスが標準形式のビットマップの場合は、GDI は、ドライバーがパフォーマンスを強化するために呼び出しをフックしない限り、出力、すべてのテキストを処理できます。 デバイス管理の画面では、ドライバーはテキスト出力をサポートする必要があります。

次のトピックでは、管理機能のフォントとテキストのサポートに関する情報を提供します。

[管理とフォントを最適化します。](managing-and-optimizing-fonts.md)

[テキストの描画](drawing-text.md)

 

 





