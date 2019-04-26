---
title: 反転の間隔
description: 反転の間隔
ms.assetid: 9372d63c-e2a7-4f70-a4f0-c50df9183f75
keywords:
- 図面ページ WDK DirectDraw、間隔を反転します。
- DirectDraw WDK Windows 2000 の表示、間隔の反転
- 反転 WDK DirectDraw、間隔をページします。
- WDK DirectDraw、間隔の反転
- ポストされた反転 WDK DirectDraw
- 提供終了済み WDK DirectDraw を反転します。
- DDCAPS2_FLIPNOVSYNC
- DDCAPS2_FLIPINTERVAL
- DDFLIP_NOVSYNC
- DDFLIP_INTERVAL2
- DDFLIP_INTERVAL3
- DDFLIP_INTERVAL4
- DDERR_WASSTILLDRAWING
- 保留中の WDK DirectDraw を反転させます。
- ページ フリップ WDK DirectDraw を描画、タイミング
- DirectDraw フリッピング WDK Windows 2000 を表示するタイミング
- WDK の DirectDraw を反転するページのタイミング
- WDK DirectDraw を反転、タイミング
- WDK DirectDraw を反転するタイミング
- WDK の DirectDraw を画面の回転
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae28d4406f78466634d321f5c0ee240596f0cefd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347572"
---
# <a name="flip-intervals"></a>反転の間隔


## <span id="ddk_flip_intervals_gg"></span><span id="DDK_FLIP_INTERVALS_GG"></span>


DirectX 6.0 以降、DirectDraw には、フリップ コマンドを実行するときに決定するアプリケーションの機能が追加されました。 これらの機能のサポートは、ハードウェア機能に応じて、既存のドライバーを追加できます。

アプリケーションの呼び出しに関連するタイミングを記述するときに、次の用語が使用される**反転**:

<span id="Posted"></span><span id="posted"></span><span id="POSTED"></span>**投稿**  
アプリケーションを呼び出す時間**反転**DirectDraw 呼び出してドライバーの[ *DdFlip* ](https://msdn.microsoft.com/library/windows/hardware/ff549306)エントリ ポイント。

<span id="Retired"></span><span id="retired"></span><span id="RETIRED"></span>**提供終了**  
新しい画面を表示する、ハードウェアが開始される時刻。

DirectDraw の以前のバージョンで反転が常に廃止上または近く、垂直同期次投稿に使用されたとき。 DirectX 6.0 とそれ以降のバージョンでは、アプリケーションは、こと、フリップを破棄する、すぐには、投稿、または、いくつかの反転が投稿された後に垂直方向の同期の数を設定しているときに正確に指定できます。 2 つの機能のビットがある (DDCAPS2\_FLIPNOVSYNC と DDCAPS2\_で FLIPINTERVAL、 [ **DDCORECAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff549248)構造) と 4 つのフラグ (DDFLIP\_NOVSYNC、DDFLIP\_INTERVAL2、DDFLIP\_INTERVAL3、および DDFLIP\_で INTERVAL4、 [ **DD\_FLIPDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551520)構造体) を有効にするには機能です。

場合は、ドライバー設定 DDCAPS2\_、DDFLIP 受信 FLIPNOVSYNC、\_NOVSYNC フラグ、 **dwFlags** 、DD のメンバー\_FLIPDATA 構造体。 DDFLIP\_NOVSYNC フラグは、それが投稿されるとすぐに、フリップを破棄することを示します。 ただし、ここでは、ハードウェアできる必要があります、少なくともスキャンごとの行ごとにバッファーを切り替えます。 ドライバーは DDCAPS2 のサポートを指定しないでください\_FLIPNOVSYNC 場合は、表示は実際にインベントリ削除されません、反転、[次へ] の垂直同期まで場合でも、ドライバーはすぐに返します。

DDFLIP の末尾に数値\_INTERVAL2、DDFLIP\_INTERVAL3、および DDFLIP\_INTERVAL4 フラグは、ハードウェアがポストされた、インベントリから削除するまでの待機数の垂直同期の反転を表します。 たとえば、DDFLIP\_INTERVAL2 は、ハードウェアが 2 つの垂直同期をカウントする必要がありますし、上または 2 つ目の垂直同期の近くの反転をインベントリから削除することを意味します。

ドライバーが DDCAPS2 を公開している場合\_FLIPINTERVAL、し、DirectDraw の最上位バイトの反転を遅延する垂直方向の同期の数を配置、 **dwFlags**のメンバー、 [ **DD\_FLIPDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551520)構造体。 DDFLIP\_INTERVAL2、DDFLIP\_INTERVAL3、および DDFLIP\_INTERVAL4 フラグが true に定義されている、ドライバーはこれら 3 つのフラグをビット フラグとして扱っていない必要があります。 さらに、ドライバーが DDCAPS2 を公開している場合\_FLIPINTERVAL、DirectDraw によりの最上位バイト、 **dwFlags**メンバーは状況に応じて設定すると、DDFLIP\_INTERVAL2、DDFLIP\_INTERVAL3、および DDFLIP\_INTERVAL4 フラグが設定されていません。 DDFLIP\_NOVSYNC により、最上位バイトに配置することに 0 を最上位バイトの既定値になりますと 1 つ、反転の既定の動作を呼び出すためですが、ポストされた後、上または最初の垂直同期の近くの反転をインベントリから削除するがします。

DirectX の 1.0 以降、返す DDERR するドライバーの必要が\_WASSTILLDRAWING、反転するが保留中の (つまり、ときに、フリップが送信されてが、廃止されていない) されるたびにします。 この要件は、フリップ間隔に拡張されます。 DDFLIP\_NOVSYNC 反転は、そのため、保留中は決してからポストバックされるときに提供終了、ドライバーを返さないで DDERR\_WASSTILLDRAWING などの反転の結果として。 逆に、DDFLIP のいずれかを使用して\_INTERVAL2、DDFLIP\_INTERVAL3、または DDFLIP\_INTERVAL4 フラグは、ドライバーを DDERR を返す必要があることを意味\_WASSTILLDRAWING 長期間のための期間投稿とフリップをインベントリから削除の間を拡張できます。

DirectDraw がオーバーレイのサーフェスを使用したこれらのフラグの使用を妨害しないが、DDCAPS2 を設定する場合でも、それらを尊重するドライバーが必要ない\_FLIPINTERVAL または DDCAPS2\_FLIPNOVSYNC 機能ビット。 ドライバー、機能があるが、アプリケーションは、この機能を利用する可能性が低い場合は、オーバーレイのこれらのフラグを尊重することもできます。

**注**   、DDFLIP\_INTERVAL2、DDFLIP\_INTERVAL3、および DDFLIP\_INTERVAL4 フラグはハードウェアの機能を利用するためのものです。 ドライバーは、要求されたページ フリップの再試行が可能になるまで、ドライバーでのループでこれらのフラグをエミュレートするためにしないようにします。 DirectDraw ドライバーの呼び出し中には、重要なオペレーティング システムのミュー テックスが保持されている、ために、このような実装は、システムのパフォーマンスに影響ことができます。

 

 

 





