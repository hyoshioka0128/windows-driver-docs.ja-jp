---
title: フォントの管理と最適化
description: フォントの管理と最適化
ms.assetid: 5cfc2174-c605-4399-97a6-62f51df21c16
keywords:
- フォント WDK のグラフィックスの管理と最適化
- GDI WDK Windows 2000 の表示、フォント、管理と最適化
- グラフィック ドライバー WDK Windows 2000 を表示するフォント、管理と最適化
- プロデューサー WDK グラフィック
- WDK GDI のコンシューマー
- グリフは WDK グラフィック
- GDI WDK Windows 2000 を表示するテキストを出力するには、管理と最適化
- グラフィック ドライバー WDK Windows 2000 を表示するテキストを出力するには、管理、およびフォントを最適化します。
- WDK GDI やフォントを描画、管理および最適化します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b36bc13e44ba7c0291a73e72bfbd9894ac342cb9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379016"
---
# <a name="managing-and-optimizing-fonts"></a>フォントの管理と最適化


## <span id="ddk_managing_and_optimizing_fonts_gg"></span><span id="DDK_MANAGING_AND_OPTIMIZING_FONTS_GG"></span>


A*プロデューサー*ドライバー フォントを生成することです。 グリフについては、グリフのメトリック、ビットマップ、および概要など、出力として生成します。 A*コンシューマー*フォントを使用するドライバーします。 グリフの情報をテキスト出力を生成するための入力として受け取り、またはハードウェアの独自のフォントをデバイス管理の表面に描画する必要があります。 ドライバーは、プロデューサーとコンシューマーの両方を指定できます。 処理中に、プリンター ドライバーをプロデューサーとして機能するなど、 [ **DrvQueryFontData** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvqueryfontdata)グリフのメトリックと以降の機能を処理中にコンシューマーとして提供する呼び出しを[ **DrvTextOut** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout)呼び出します。

フォントのプロデューサーまたはフォントのコンシューマーがある場合にのみ、フォントを処理するために、ドライバーが必要です。 ドライバーが GDI でフォント メトリックを含む、このフォントについての情報を指定する必要があります、ハードウェアに常駐しているフォントがある場合は、 [ **IFIMETRICS** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_ifimetrics) Unicode から個々 のグリフへのマッピングを構成します。id、個々 のグリフの属性、およびカーニング テーブル。 ドライバーをサポートする必要があります関数もあります。 一部の関数は、両方でフォント ドライバーとドライバーをドライバーに固有またはデバイスに固有のフォントを使用する必要があります。 他のユーザーは、フォント ドライバーにのみ必要です。

フォントの機能のサポートは、ドライバーの機能に依存します。 一般的な種類は次のとおりです。

[メトリック関数](font-metric-functions.md)

[グリフ関数](font-driver-functions.md)

[TrueType 関数](truetype-font-driver-functions.md)

 

 





