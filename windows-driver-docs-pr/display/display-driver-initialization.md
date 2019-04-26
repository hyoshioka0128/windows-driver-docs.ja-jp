---
title: ディスプレイ ドライバーの初期化
description: ディスプレイ ドライバーの初期化
ms.assetid: a4cc7780-b6fb-486a-b54b-96c90d4fe1f5
keywords:
- ディスプレイ ドライバー WDK Windows 2000 では、初期化しています
- ディスプレイ ドライバーの初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 756481872c11416a31cddbc1909f5c7cda022c5e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357942"
---
# <a name="display-driver-initialization"></a>ディスプレイ ドライバーの初期化


## <span id="ddk_display_driver_initialization_gg"></span><span id="DDK_DISPLAY_DRIVER_INITIALIZATION_GG"></span>


」の説明に従って、ディスプレイ ドライバーの初期化はグラフィックス ドライバーの初期化に似ています[サポートの初期化と終了関数](supporting-initialization-and-termination-functions.md)します。 このセクションでは、ディスプレイ ドライバー固有の初期化の詳細を提供します。

ビデオのミニポートとディスプレイ ドライバーの初期化は、NT エグゼクティブと Win32 サブシステムが読み込まれ、初期化後に発生します。 システムでは、ビデオのミニポート ドライバーまたはレジストリで、有効になっているドライバーが読み込まれる、いるビデオのミニポート ドライバーと使用するディスプレイ ドライバーのペアを判断します。 GDI では、このプロセス中にウィンドウ マネージャーによって提供される情報に基づいて、すべての必要なディスプレイ ドライバーが表示されます。

基本的なドライバーの初期化手順をデスクトップが作成され、次の図に示したを表示します。

![ディスプレイ ドライバーの初期化を示す図](images/202-01.png)

1.  最初のデバイス コンテキストを作成する GDI が呼び出された場合 (*DC*) ビデオ ハードウェアには、GDI は、ディスプレイ ドライバー関数を呼び出す[ **DrvEnableDriver**](https://msdn.microsoft.com/library/windows/hardware/ff556210)します。 戻り時に**DrvEnableDriver**で GDI の提供、 [ **DRVENABLEDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff556206)ドライバーのグラフィックス DDI バージョン番号とすべてのエントリ ポイントの両方を保持する構造体呼び出し可能なグラフィックス ドライバーによって実装される DDI 関数 (以外の**DrvEnableDriver**)。

2.  GDI を呼び出してドライバーの[ **DrvEnablePDEV** ](https://msdn.microsoft.com/library/windows/hardware/ff556211)ドライバーの物理デバイスの特性の説明を要求する関数。 呼び出しで GDI 渡しますで、 [ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837)構造体は、GDI に設定しようとするモードを識別します。 GDI は、表示または基になるミニポート ドライバーがサポートされていないモードを要求している場合、ディスプレイ ドライバーはこの呼び出しに失敗する必要があります。

3.  ディスプレイ ドライバーは、GDI によって制御される論理デバイスを表します。 次の図に示すように、1 つの論理デバイスは、いくつかの物理デバイスを管理できます、各特徴のハードウェア、論理アドレスは、サーフェスがサポートされている型。 ディスプレイ ドライバーでは、作成、デバイスをサポートするためにメモリを割り当てます。 ディスプレイ ドライバーは、1 つ以上を管理する時に呼び出すことができます*PDEV*同じ物理デバイスの場合は、特定の物理デバイスの時刻に 1 つだけ PDEV を有効にすることができます。 個別の各 PDEV が作成された GDI の呼び出し[ **DrvEnablePDEV**](https://msdn.microsoft.com/library/windows/hardware/ff556211)、各呼び出しが別の面で使用されるもう 1 つの PDEV を作成します。

    ドライバーには、1 つ以上の PDEV をサポートする必要があります、ために、グローバル変数は使用しないでください。

    次の図は物理デバイスと論理を示しています。

    ![物理デバイスと論理を示す図](images/202-03.png)

4.  物理デバイスのインストールが完了すると、GDI 呼び出し[ **DrvCompletePDEV**](https://msdn.microsoft.com/library/windows/hardware/ff556181)します。 この関数は、デバイスの GDI 関数を要求するときに使用する物理デバイスの GDI で生成されたハンドルを持つドライバーを提供します。

5.  初期化の最終段階では、ビデオ ハードウェアのサーフェスを作成 GDI の呼び出しによって[ **DrvEnableSurface**](https://msdn.microsoft.com/library/windows/hardware/ff556214)、ハードウェアのグラフィックス出力できます。 によって、デバイスと、環境では、ディスプレイ ドライバーには、2 つの方法のいずれかの画面が有効にします。
    -   ドライバーは、GDI 関数を呼び出すことによって、独自の画面を管理**EngCreateDeviceSurface**メソッドは必要なハードウェアを標準形式のビットマップをサポートしていませんはハードウェアの省略可能です。
    -   GDI は、画面を管理できるとして完全に、*エンジン管理画面*ハードウェア デバイスの標準形式のビットマップとして編成表面場合。 ドライバーを呼び出すことができます[ **EngModifySurface** ](https://msdn.microsoft.com/library/windows/hardware/ff564976)に変換する、*デバイスで管理された*はプライマリのビットマップ*エンジン管理*します。 ドライバーは、描画操作をフックすることができますも。

いずれかの既存の GDI ビットマップ ハンドルは、有効な表面ハンドルです。 ドライバーを呼び出すことができます[ **EngModifySurface** ](https://msdn.microsoft.com/library/windows/hardware/ff564976)エンジンに管理されたビットマップにデバイス管理の主なビットマップに変換します。 サーフェスがエンジンに管理された場合は、GDI がいずれかまたはすべての描画操作を処理できます。 ドライバーが処理する必要がありますには、少なくとも、デバイスの管理を画面には場合、 [ **DrvTextOut**](https://msdn.microsoft.com/library/windows/hardware/ff557277)、 [ **DrvStrokePath**](https://msdn.microsoft.com/library/windows/hardware/ff556316)、および[**DrvBitBlt**](https://msdn.microsoft.com/library/windows/hardware/ff556180)します。


自動的に有効 DirectDraw を呼び出した後に GDI [ **DrvEnableSurface**](https://msdn.microsoft.com/library/windows/hardware/ff556214)します。 DirectDraw の DirectDraw が初期化された後、ドライバーを使用しますできます*ヒープ マネージャー*を実行する[*オフスクリーン メモリ*](video-present-network-terminology.md#off_screen_memory)管理します。 参照してください[DirectDraw と GDI](directdraw-and-gdi.md)詳細についてはします。


ディスプレイ ドライバーを実装する必要があります[ **DrvNotify** ](https://msdn.microsoft.com/library/windows/hardware/ff556252) DN では特に、通知イベントを受信するために\_描画\_開始イベント。 GDI は、キャッシュを初期化する時期を決定するために使用できるように、描画を開始する直前にこのイベントを送信します。

参照してください、[プラグ アンド プレイ](https://msdn.microsoft.com/library/windows/hardware/ff547125)ブート プロセスに関する詳細についてはします。



 





