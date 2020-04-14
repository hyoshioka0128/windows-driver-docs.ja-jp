---
title: PDEV の初期化とクリーンアップ
description: PDEV の初期化とクリーンアップ
ms.assetid: 26651869-861a-4be8-bc6c-df3704ca714e
keywords:
- WDK GDI の描画, 初期化, PDEV の初期化
- グラフィックスドライバーの初期化 WDK Windows 2000 display、PDEV
- GDI WDK Windows 2000 display、initialization、PDEV
- グラフィックスドライバー WDK Windows 2000 display、initialization、PDEV
- PDEV WDK GDI
- Dr・ Ablepdev
- WDK GDI の描画、PDEV クリーンアップ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a560feca6edb4e15ffb38e806bfee392acba33a0
ms.sourcegitcommit: 8adf72e64e6eddb62b8b7de01f79a748a2112f62
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2020
ms.locfileid: "81224692"
---
# <a name="pdev-initialization-and-cleanup"></a>PDEV の初期化とクリーンアップ


## <span id="ddk_pdev_initialization_and_cleanup_gg"></span><span id="DDK_PDEV_INITIALIZATION_AND_CLEANUP_GG"></span>


各カーネルモードグラフィックドライバーは、GDI によって管理される1つの論理デバイスを表します。 さらに、ドライバーは1つ以上の*Pdev*構造を管理できます。 PDEV は、物理デバイスを論理的に表現したものです。 これは、ハードウェア、論理アドレス、およびサポート可能なサーフェイスの種類によって特徴付けられています。

-   **ハードウェアの種類**: ハードウェアの種類によって特徴付けられた pdev をサポートするドライバーの例として、1つのドライバーで LaserWhiz、LaserWhiz II、LaserWhiz スーパープリンターがサポートされる場合があります。 GDI によって渡されるデバイス名は、ドライバーでサポートされているデバイスの合計セットから要求される論理デバイスを指定します。

-   **論理アドレス**: 1 つのドライバーで、LPT1、COM2、および \\という名前のサーバー \\SERVER1\\PSLASER に接続されているプリンターをサポートできます (たとえば、)。 さらに、複数の VGA ディスプレイを同時にサポートできるディスプレイドライバーでは、0x3CE、0x2CE などのポート番号で区別することができます。 プリンターの論理アドレスとその他のハードコピー出力デバイスは、GDI によって決定されます。[**EngWritePrinter**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engwriteprinter)関数は、出力を適切な宛先に送信します。 表示では、独自の論理アドレスを暗黙的に決定するか、 [**Devmodew**](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)のプライベートセクションからアドレスを取得することができます。

    DEVMODEW 構造体は、ドライバーに必要な環境設定を提供します。たとえば、デバイスの名前や、プリンターまたはディスプレイドライバーに固有のその他の情報などです。

-   **サーフェイス**: 各 pdev には一意のサーフェイスが必要です。 たとえば、プリンタードライバーが2つの印刷ジョブで同時に動作し、それぞれが横向きや縦の形式などの異なるページ形式を必要とする場合、各印刷ジョブには異なる PDEV が必要です。 同様に、ディスプレイドライバーは同じディスプレイの2つのデスクトップをサポートする場合があり、各デスクトップは異なる PDEV と surface を必要とします。 必要なサーフェイスごとに、そのサーフェイスに対して異なる PDEV を作成するための[**Dr・ ablepdev**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev)関数が呼び出されます。

*Drベンダー Ablepdev*への呼び出しに応答して、ドライバーはいくつかの構造を通じて、ハードウェアデバイスの機能に関する情報を GDI に返します。

[**GDIINFO**](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_gdiinfo)構造体は、GDI が*dr*を呼び出す前にゼロで埋められます。 ドライバーは、次の情報を GDI に伝えるために GDIINFO に入力します。

-   ドライバーのバージョン番号

-   基本的なデバイステクノロジ (ラスターとベクター)

-   印刷可能なページのサイズと解像度

-   カラーパレットとグレースケール情報

-   フォントとテキストの機能

-   ハーフトーンサポート

-   スタイルのステップ番号

ドライバーは、サポートしているフィールドだけを入力し、残りは無視します。

ドライバーは、 [**DEVINFO**](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdevinfo)構造体に、この pdev のグラフィックス機能を記述するフラグを設定します。 ほとんどの場合、DEVINFO からの情報は、ドライバーが提供できるグラフィックスサポートのレベルを GDI に伝えます。 たとえば、高音音部記号の描画が必要な場合、DEVINFO 内の情報は、ドライバーがベジエ曲線を処理できるかどうか、または GDI が代わりに複数の線セグメントを送信する必要があるかどうかを GDI に伝えます。 ドライバーはサポートされているだけのフィールドを入力し、他のフィールドはそのままにしておきます。

ドライバーが提供する必要のあるもう1つの重要な情報は、標準の塗りつぶしパターンを表すサーフェイスのハンドルを格納したバッファーへのポインター (*Phsurfpatterns*) です。 標準の塗りつぶしパターンに加えて、 *Phsurfpatterns*には null を含めることができ、これにより GDI はデバイスの解像度とピクセルサイズに応じて自動的にパターン画面を作成します。 標準パターンで[ブラシを実現](realizing-brushes.md)するために GDI が呼び出されると、 [**DrvRealizeBrush**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvrealizebrush)関数を呼び出して、要求されたパターンに定義されているブラシを認識します。

GDI は、デバイスをサポートするカーネルドライバーに対して、 [**Dr・ Ablepdev**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev) a Handle ( *hdriver*) を渡します。 プリンタドライバの場合、 *Hdriver*はプリンタへのハンドルを提供し、 **EngWritePrinter**などの呼び出しでスプーラに対して使用されます。

GDI が*Dr・ ablepdev*を呼び出す場合、ドライバーは、作成された pdev をサポートするために必要なメモリを割り当てる必要があります。これは、異なるモードの他の pdev 構造を作成するために*Dr・ ablepdev*が呼び出された場合でも同様です。 (1 つのドライバーには複数のアクティブな PDEVs がありますが、一度に有効にできるのは1つだけです)。ただし、GDI が[**DrvEnableSurface**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablesurface)を呼び出すまでは、実際のサーフェイスはサポートされません。

デバイスの画面でビットマップの割り当てが必要な場合、画面が有効になるまで (通常は[**DrvEnableSurface**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablesurface)関数内)、割り当ては必要ありません。 アプリケーションはデバイスに実際に書き込む前にデバイス情報を要求することがよくありますが、大きなビットマップの割り当てを待機すると、貴重なリソースを節約し、システムの初期化中にドライバーのパフォーマンスを向上させることができます。

PDEV のインストールが完了すると、GDI は[**DrvCompletePDEV**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcompletepdev)関数を呼び出して、物理デバイスのインストールが完了したことをドライバーに通知します。 また、この関数は、ドライバーに PDEV への論理ハンドルを提供します。これは、ドライバーが GDI 関数の呼び出しで使用します。

ドライバーの[**DrvDisablePDEV**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablepdev)関数を呼び出すと、指定された物理デバイスが不要になったことが示されます。 この関数では、ドライバーは物理デバイスで使用されているメモリとリソースを解放する必要があります。

[画面を有効または無効](enabling-and-disabling-the-surface.md)にする方法についても参照してください。

 

 





