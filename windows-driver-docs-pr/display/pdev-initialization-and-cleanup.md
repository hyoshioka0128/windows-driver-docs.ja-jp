---
title: PDEV の初期化とクリーンアップ
description: PDEV の初期化とクリーンアップ
ms.assetid: 26651869-861a-4be8-bc6c-df3704ca714e
keywords:
- 描画の WDK GDI、初期化、PDEV 初期化
- 初期化中のグラフィックス ドライバー WDK Windows 2000 の表示、PDEV
- GDI WDK Windows 2000 の表示、初期化、PDEV
- グラフィック ドライバー WDK Windows 2000 を表示、初期化、PDEV
- PDEV WDK GDI
- DrvEnablePDEV
- 描画 WDK GDI、PDEV クリーンアップ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 073bc821d31ffe81d38719a337baf4553608ad25
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375024"
---
# <a name="pdev-initialization-and-cleanup"></a>PDEV の初期化とクリーンアップ


## <span id="ddk_pdev_initialization_and_cleanup_gg"></span><span id="DDK_PDEV_INITIALIZATION_AND_CLEANUP_GG"></span>


各カーネル モードのグラフィックス ドライバーでは、GDI によって管理される 1 つの論理デバイスを表します。 ドライバーが 1 つまたは複数を管理する、 *PDEV*構造体。 PDEV は、物理デバイスの論理表現です。 これは、ハードウェア、論理アドレス、およびサポートできるサーフェスの種類によって分類されます。

-   **ハードウェアの種類**âˆ' としてハードウェアの種類によって分類 PDEV をサポートしているドライバーの例は、1 つのドライバーが LaserWhiz、LaserWhiz II、および LaserWhiz スーパー プリンターをサポート可能性があります。 GDI によって渡されるデバイス名では、論理デバイスがドライバーでサポートされているデバイスの合計セットから要求を指定します。

-   **論理アドレス**âˆ' 1 つのドライバーは、LPT1、COM2、およびという名前のサーバーに接続されたプリンターをサポートできる\\ \\SERVER1\\PSLASER の例では、します。 さらに、VGA ディスプレイを同時に 1 つ以上をサポートできるディスプレイ ドライバーは、0x2CE、0x3CE などのポート番号によってそれらの間で区別し、具合です。 プリンターの論理アドレスとその他のハード コピーの出力デバイスは GDI; によって決まります[ **EngWritePrinter** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engwriteprinter)関数は、適切な送信先に出力を転送します。 表示する、独自の論理アドレスを暗黙的に決定かのプライベート セクションからアドレスを取得[ **DEVMODEW**](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)します。

    DEVMODEW 構造体は、デバイスとプリンターまたはディスプレイ ドライバーのいずれかに固有の他の情報の名前など、必要な環境の設定でドライバーを提供します。

-   **サーフェス**âˆ' Each PDEV 固有の画面が必要です。 たとえば、プリンター ドライバーが同時に 2 つの印刷ジョブで作業する場合は、それぞれ、横と縦の形式などの別のページの形式を必要とする各印刷ジョブが必要です異なる PDEV。 同様に、ディスプレイ ドライバーは、同じの表示では、別の PDEV と画面を必要とする各デスクトップの 2 つのデスクトップをサポートする場合があります。 それぞれの面が必要なへの呼び出し、 [ **DrvEnablePDEV** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev)サーフェスの異なる PDEV を作成する関数。

呼び出しに応答*DrvEnablePDEV*ドライバーは、いくつかの構造を GDI をハードウェア デバイスの機能に関する情報を返します。

[ **GDIINFO** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_gdiinfo)構造は、GDI の呼び出しの前にゼロで埋められます*DrvEnablePDEV*します。 GDIINFO GDI に次の情報を通信するために、ドライバーを入力します。

-   ドライバーのバージョン番号

-   基本的なデバイス テクノロジ (ラスター ベクトルとの比較)

-   サイズと解像度の印刷可能ページ

-   パレットの色およびグレースケール情報

-   フォントとテキストの機能

-   ハーフトーン サポート

-   手順の番号のスタイル

ドライバーは、サポート フィールドのみを入力し、残りの部分を無視する必要があります。

ドライバーを設定、 [ **DEVINFO** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdevinfo)この PDEV のグラフィックス機能を記述するフラグを含む構造体。 ほぼすべての場合、DEVINFO からの情報は GDI をドライバーが提供できるグラフィックスのサポートのレベルに通知されます。 たとえば、高音音部記号の描画が必要な場合は、ベジエ曲線をドライバーが処理できるかどうか、またはかどうか GDI がする必要があります複数の線分を代わりに送信 DEVINFO 内の情報 GDI は指示します。 ドライバーは、サポートするために同じ数のフィールドを入力し、まま、他のユーザー必要があります。

もう 1 つの重要な情報のドライバーが提供する必要がありますが、ポインター (*phsurfPatterns*) 標準の塗りつぶしのパターンを表すサーフェスのハンドルを入力バッファーにします。 標準の塗りつぶしのパターンだけでなく*phsurfPatterns* GDI デバイスの解像度とピクセル サイズに従って自動的にパターンの画面を作成すると、null を含めることができます。 GDI が呼び出されたとき[ブラシを実現](realizing-brushes.md)が呼び出す、標準のパターンを持つ、 [ **DrvRealizeBrush** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvrealizebrush)要求パターンに対して定義されているブラシを実現する関数。

GDI 渡します[ **DrvEnablePDEV** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev)ハンドルを*hDriver*デバイスをサポートしているカーネル ドライバーの。 プリンター ドライバー、 *hDriver*プリンターを識別するハンドルを提供しなどの呼び出しで使用されます**EngWritePrinter**スプーラーにします。

GDI を呼び出すたびに*DrvEnablePDEV*、ドライバーは、作成される PDEV をサポートするために必要なメモリを割り当てる必要がありますも*DrvEnablePDEV*を呼び出して別のモードには、他の PDEV 構造を作成するには. (ドライバーがいくつかのアクティブな PDEVs が、一度に 1 つのみを有効にすることができます。)ただし、実際の画面は、GDI 呼び出されるまでサポートされていません[ **DrvEnableSurface**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablesurface)します。

サーフェスが有効になるまでには、割り当てが必要ないデバイスの画面には、ビットマップの割り当てが必要とする場合 (通常、 [ **DrvEnableSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablesurface)関数)。 アプリケーションは、多くの場合、実際には、デバイスに書き込む前にデバイス情報を要求を貴重なリソースを保存し、システムの初期化中にドライバーのパフォーマンスを向上できます大きなビットマップの割り当てを待機しています。

GDI を呼び出す、PDEV のインストールが完了すると、 [ **DrvCompletePDEV** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcompletepdev)物理デバイスのインストールが完了したことをドライバーに通知する関数。 この関数には、GDI 関数の呼び出しで、ドライバーを使用すると、PDEV に GDI の論理のハンドルを持つドライバーも提供します。

ドライバーへの呼び出し[ **DrvDisablePDEV** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablepdev)関数では、特定の物理デバイスが不要になったことを示します。 この関数では、ドライバーは、メモリと物理デバイスで使用されるリソースを解放する必要があります。

参照にも[を有効にして、画面を無効化](enabling-and-disabling-the-surface.md)します。

 

 





