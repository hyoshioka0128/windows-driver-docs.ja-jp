---
title: 標準モードと非標準モードの切り替え
description: 標準モードと非標準モードの切り替え
ms.assetid: 15939910-b325-47ff-b4ed-bbaeec4149bd
keywords:
- 非標準の表示モード WDK DirectX 9.0、標準モードと非標準モードの切り替え
- 標準モードと非標準モードの切り替え (WDK DirectX 9.0)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 278efa270816e81d35e61710a2f23233f20d8ddd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829361"
---
# <a name="switching-between-standard-and-nonstandard-modes"></a>標準モードと非標準モードの切り替え


## <span id="ddk_switching_between_standard_and_nonstandard_modes_gg"></span><span id="DDK_SWITCHING_BETWEEN_STANDARD_AND_NONSTANDARD_MODES_GG"></span>


DirectX 9.0 ドライバーは標準の表示モードの標準のプライマリサーフェイスを作成し、非標準モードのダミーのプライマリサーフェイスを作成します。これにより、ランタイムは必要に応じてモードを切り替えることができます。 両方のサーフェイスは同じビデオメモリを表しますが、異なる形式で表示されます。 次の順序でページフリップが要求されると、ドライバーは標準モードと非標準モードを切り替えます。

1.  アプリケーションがモードスイッチを要求します。

    アプリケーションは、 **Changedisplaysettings**関数を呼び出して、ビデオモードを一致するビット深度に変更します。 10:10:10:2 モードでは、ビットの深さは1ピクセルあたりの32ビットです。 **Changedisplaysettings**の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

2.  標準のプライマリサーフェイスがドライバーによって作成されます。

    ランタイムは、ドライバーの[*dd/face*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))関数を呼び出して、プライマリサーフェイスの作成を要求します。 この主な画面では、標準の表示形式 (たとえば、D3DFMT\_A8B8G8R8) が使用され、バックバッファーはありません。

3.  ドライバーは、ダミーのプライマリサーフェスチェーンを作成します。

    ランタイムは、ドライバーの*ddの*デバイス関数を呼び出して、ダミーのプライマリサーフェイスの作成を要求します。 ランタイムは、このサーフェイスが非標準の表示モードを使用していることを示すために、このサーフェイスの[**DDSCAPS2**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550292(v=vs.85))構造体の**DWCAPS2**メンバーに DDSCAPS2\_extendedformatprimary (0x40000000) 機能ビットを指定します (たとえば、D3DFMT\_A2R10G10B10)。 ランタイムでは、DDSCAPS2 の**Dwcaps**メンバーの DDSCAPS\_OFFSCREENPLAIN 機能ビットも指定して、サーフェイスに明示的なピクセル形式があることを示します。

    この画面は既存のプライマリサーフェイスの別の名前であるため、ドライバーは、画面にさらにビデオメモリを割り当てないようにする必要があります。

    この画面では、ランタイムは、DDSCAPS\_フリップと DDSCAPS\_、 **Dwcaps**の複雑な機能ビットと、ランタイムが標準のプライマリサーフェイス反転チェーンを設定するのと同じように、アタッチされたバックバッファーのセットを指定します。 ドライバーは、これらのバックバッファーに対して、ドライバーの*dd記憶*用関数に対する後続の呼び出しが行われないため、これらのバックバッファーにビデオメモリを割り当てる必要があります。つまり、ランタイムは、標準プライマリに対して複数の surface オブジェクトを作成します。

4.  ドライバーは、サーフェイスを非標準の形式に反転させます。

    ディスプレイデバイスは標準形式を出力しますが、アプリケーションはこれらのバックバッファーのいずれかに非標準のイメージを合成します。 このイメージが表示可能になると、ランタイムは、ドライバーの[*Ddflip*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_flip)関数の呼び出しで、非標準サーフェスの1つをターゲットとして指定します。 次に、ドライバーはディスプレイデバイスを再プログラムして、非標準の形式を出力します。

5.  アプリケーションが実行されます。

    アプリケーションは、非標準のバッファー間でドライバーの*Ddflip*関数の呼び出しをさらに生成し、ドライバーは非標準の形式を引き続き表示します。 また、アプリケーションでは、D3DDP2OP\_BLT 操作コードを使用してドライバーの[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)関数の呼び出しを生成し、バックバッファーをフロントバッファーにコピーすることもできますが、これらの呼び出しは常に2つの非標準の surface オブジェクト間で行われます。 ドライバーがウィンドウモードで非標準の形式をサポートしていない場合、ドライバーは非標準および標準の表面形式間の blts を処理しません。 ウィンドウモードの場合の詳細については、「 [2 次元演算のサポート](supporting-two-dimensional-operations.md)」を参照してください。

6.  ドライバーは、画面を標準形式に戻します。

    アプリケーションが閉じられるか最小化されると、ランタイムは、ドライバーの*Ddflip*関数の呼び出しで、標準形式のプライマリサーフェイスを変換先として指定します。 次に、ドライバーはディスプレイデバイスを再プログラムして、標準形式を出力します。

7.  ドライバーはダミーサーフェイスを破棄します。

    ドライバーがダミーサーフェイスを破棄する場合は、標準形式がディスプレイデバイスで再プログラミングされていることを確認する必要があります。

 

 





