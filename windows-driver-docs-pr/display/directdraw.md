---
title: DirectDraw
description: DirectDraw
ms.assetid: b7f1194e-0f5e-444e-a71c-6a4a836547d9
keywords:
- DirectDraw WDK Windows 2000 の表示
- Windows 2000 ディスプレイ ドライバー モデル WDK、DirectDraw
- ドライバー モデル WDK Windows 2000 では、DirectDraw を表示します。
- ヘッダー ファイルの WDK DirectDraw
- DirectDraw WDK Windows 2000 の表示、ヘッダー ファイル
- 描画の WDK DirectDraw
- 描画の WDK DirectDraw、ヘッダー ファイル
- グラフィックス WDK Windows 2000 を表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d450f33a45a569e407a702eff00301cffe34cce
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549641"
---
# <a name="directdraw"></a>DirectDraw


## <span id="ddk_directdraw_gg"></span><span id="DDK_DIRECTDRAW_GG"></span>


このセクションでは、Microsoft DirectDraw インターフェイスと、アーキテクチャについて説明し、DirectDraw ドライバー ライターの実装に関するガイドラインを提供します。 ガイドラインは、Microsoft Windows 2000 以降に書き込まれます。 リーダーは、DirectDraw Api に習熟し、あるドライバー モデルの表示、Windows 2000 を確実に把握する必要があります。

Microsoft Windows 2000 以降の Microsoft DirectDraw ドライバーを作成しているドライバーの作成者は、次のヘッダー ファイルを使用してください。

-   *ddrawint.h*基本型、定数、および構造体が DirectDraw ドライバーが含まれています。

-   *ddraw.h*基本型、定数、およびアプリケーションとドライバーの両方で使用する構造体が含まれています。

-   *dvp.h*ドライバーは、DirectDraw ビデオ ポート拡張機能 (VPE) をサポートしているときに使用されます。

-   *dxmini.h*ビデオのミニポート ドライバーには、カーネル モードのビデオ トランスポート、DxApi インターフェイスのサポートが含まれていますときに使用されます (で指定された関数、 [ **DXAPI\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff557395)。構造)。

-   *ddkmapi.h*ビデオ キャプチャ ドライバーでのアクセスに使用、 [ **DxApi** ](https://msdn.microsoft.com/library/windows/hardware/ff557364)関数。 DirectDraw、DxApi インターフェイスに呼び出します。

-   *dmemmgr.h*ドライバーが、DirectDraw ランタイムではなく、独自のメモリ管理を実行するときに使用されます。

-   *ddkernel.h*ドライバーには、カーネル モードのサポートが含まれています。 ときに使用されます。

-   *dx95type.h*により、既存の Windows 98 を簡単に移植するためにドライバー作成者/Me ドライバーを Windows 2000 以降。 このヘッダー ファイルでは、2 つのプラットフォーム上で異なる名前をマップします。

*Ddraw.h*ヘッダー ファイルは、Windows SDK に付属; 他のすべてのヘッダー ファイルが、Windows Driver Kit (WDK) に含まれています。 Windows ドライバー開発キット (DDK) には、DirectDraw ドライバーのサンプル コードも含まれています、 *p3samp*ビデオ ディスプレイのディレクトリ。

DirectDraw ドライバー関数では、コールバック、ページを参照し、構造体が記載[DirectDraw ドライバー関数](https://msdn.microsoft.com/library/windows/hardware/ff553825)と[DirectDraw ドライバー構造](https://msdn.microsoft.com/library/windows/hardware/ff553831)します。

DirectDraw の詳細については、Windows SDK を参照してください。 DirectDraw ドライバー作成者に電子メールで質問やご意見を送信できる <em>directx@microsoft.com</em>します。

 

 





