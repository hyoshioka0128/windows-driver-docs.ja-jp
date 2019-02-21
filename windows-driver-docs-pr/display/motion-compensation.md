---
title: 動き補正
description: 動き補正
ms.assetid: 3b5c91f9-6c22-4110-943a-5b833f32c014
keywords:
- 描画の WDK DirectDraw、動き補正
- DirectDraw WDK Windows 2000 の表示、動き補正
- 動き補正 WDK
- 圧縮されたビデオのデコード WDK DirectDraw
- ビデオのデコード WDK DirectDraw
- WDK DirectDraw をデコード
- デジタル ビデオのデコード WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 746476b34371e33ce1e161ed338560b44eac3e48
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527921"
---
# <a name="motion-compensation"></a>動き補正


## <span id="ddk_motion_compensation_gg"></span><span id="DDK_MOTION_COMPENSATION_GG"></span>


モーションの補正は、圧縮されたデジタル ビデオのデコードの処理の重要なステージの用語です。 多くのグラフィック アクセラレータ デバイスでは、何らかの種類の圧縮されたビデオ デコーディングをサポートするための高速化の機能を提供します。 モーションの補正プロセスが、最も頻繁にサポートされているビデオ デコーディングの部分であるために、圧縮されたビデオ デコーディングをサポートするデバイス ドライバー インターフェイスは動き補正 DDI と呼ばれます。 モーションの補正だけでなく、一部のデバイスは IDCT (逆の不連続コサイン変換) とソフトウェアのビデオ デコーダーがデコードの処理を高速化に使用できるその他のハードウェア機能を実行できます。 動き補正 DDI がこれらにも、その他の機能を提供するハンドルのデバイスに十分な柔軟性です。

ソフトウェアの MPEG デコーダーに入力データが定義されています。 場合は、デコーダーは mpeg-2 向けの mpeg-2 形式で入力です。 デコーダーの出力も定義されます。 これは、さまざまな形式で圧縮されていないフレームです。 ただし、それまでの間の形式のソフトウェア デコーダーの間に独自の専用のデータ形式を必要とする多くのデバイスのディスプレイ デバイスが適切に定義されていません。 そのため、動き補正デバイス ドライバー インターフェイスは柔軟性があり、中間形式は Guid として説明します。 ディスプレイ ドライバーが、サポート機能を表す Guid を報告し、ソフトウェア デコーダーは、その要件に最も一致する GUID を選択します。

動き補正機能を有効にするには、ドライバーは、次の手順を実行する必要があります。

-   実装を[ **DdGetDriverInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff549404)機能、設定、 **GetDriverInfo**のメンバー、 [ **DD\_HALINFO**](https://msdn.microsoft.com/library/windows/hardware/ff551627)この関数を指す構造体と[ **DrvGetDirectDrawInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff556229)が呼び出されます。 ドライバーの*DdGetDriverInfo*関数は、GUID を解析する必要があります\_MotionCompCallbacks GUID。

-   入力、 [ **DD\_MOTIONCOMPCALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff551660)コールバック型フラグを設定すると、適切なドライバー コールバック ポインターを含む構造体、 *DdGetDriverInfo*GUID を持つ関数が呼び出された\_MotionCompCallbacks GUID。 ドライバーを Microsoft DirectDraw に割り当てられたバッファーに、この初期化された構造体をコピーしする必要があります、 **lpvData**のメンバー、 [ **DD\_GETDRIVERINFODATA**](https://msdn.microsoft.com/library/windows/hardware/ff551550)ポイント、構造体し、をバッファーに書き込まれたバイト数を返す**dwActualSize**します。

 

 





