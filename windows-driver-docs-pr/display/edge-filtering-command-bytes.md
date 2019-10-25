---
title: エッジフィルター処理コマンドバイト数
description: エッジフィルター処理コマンドバイト数
ms.assetid: eefb580a-133d-4c9e-a8d2-2d114107e2ea
keywords:
- マクロによる WDK DirectX VA のブロック、deblocking フィルターコントロール
- deblocking filter control WDK DirectX VA
- エッジフィルター WDK DirectX VA
- 読み取りバックバッファー WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: baa4fd3b1339be795952b4392ca6fa659742dee1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838960"
---
# <a name="edge-filtering-command-bytes"></a>エッジフィルター処理コマンドバイト数


## <span id="ddk_edge_filtering_command_bytes_gg"></span><span id="DDK_EDGE_FILTERING_COMMAND_BYTES_GG"></span>


各エッジフィルター制御コマンドは、1バイトで構成されます。 DXVA で定義されている*DXVA\_DeblockingEdgeControl*定数では、ブロックの端をどのように処理するかを定義し*ます*。 バイトの最上位7ビットには*EdgeFilterStrength*変数が含まれ、最下位ビットは*EdgeFilterOn*フラグです。

エッジフィルター処理は、「263付属 J」で指定されているとおりに実行されます。*EdgeFilterStrength*変数は、実行するフィルター処理の強度を指定します。 *EdgeFilterOn*フラグは、フィルター処理を実行するかどうかを指定します。 *EdgeFilterOn*は、エッジをフィルター処理する場合は1、それ以外の場合は0になります。

エッジフィルター ( *EdgeFilterOn*が1に等しいエッジ) は、 *EdgeFilterStrength*で指定された強さの値で実行され、出力は 0 ~ 2<sup>(BPP)</sup> -1 の範囲にクリッピングされます。 すべてのブロックに対するトップエッジフィルター処理は、すべてのブロックの左端のフィルター処理の前に実行されます。これは、トップエッジフィルターに使用されるサンプルの値が、左エッジフィルター処理のフィルター解除の前に再構築された値である必要があるためです。

[**DXVA\_ピクチャパラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)構造体の**b deblock限定**メンバーが、現在の deblock フィルターコマンドバッファーの外部にあるマクロブロックのサンプル値が影響を受けないことを示している場合、 *EdgeFilterOn*フラグはバッファー内の deblocking フィルターコマンドを使用して、マクロブロックによってカバーされる領域の左端と最上位のすべての端に対してゼロ。

### <a name="span-idread-back_buffersspanspan-idread-back_buffersspanspan-idread-back_buffersspanread-back-buffers"></a><span id="Read-Back_Buffers"></span><span id="read-back_buffers"></span><span id="READ-BACK_BUFFERS"></span>読み取り/バックバッファー

[**DXVA\_ピクチャパラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)構造体の**b readbackrequests**メンバーが1の場合、1つの読み取り/バックコマンドバッファーがアクセラレータに渡されます。 このバッファー内のデータは、結果として得られる最終的な画像マクロブロックデータ (該当する場合) をホストに返すためにアクセラレータによってコマンドを実行します。 暗号化プロトコルが使用されている場合、アクセラレータは、エラーを示すメッセージ、エラーのあるデータ、または暗号化されたデータ (暗号化プロトコルによって指定されている可能性があります) を返すことによって、読み取り要求に応答する場合があります。

アクセラレータに渡される読み取り/バックコマンドバッファーには、読み取るマクロブロックのマクロブロックコントロールコマンドの1つの**Wmbaddress**メンバーで構成される、読み取り戻るコマンドが含まれている必要があります。 **Wmbaddress**メンバーは、ラスタースキャンの順序で現在のマクロブロックのマクロブロックアドレスを指定する16ビット値です。 ラスタースキャンの順序 ( [**DXVA\_ピクチャパラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)構造体の**wPicWidthInMBminus1**と**wPicHeightInMBminus1**のメンバーに基づく) は、次のように定義されています。

-   0は、左上のマクロブロックのアドレスです。

-   **wPicWidthInMBminus1**は、右上にあるマクロブロックのアドレスです。

-   **wPicHeightInMBminus1** x (**wPicWidthInMBminus1**+ 1) は、左下のマクロブロックのアドレスです。

-   (**wPicHeightInMBminus1**+ 1) x (**wPicWidthInMBminus1**+ 1)-1 は、右下のマクロブロックのアドレスです。

[**DXVA\_ピクチャパラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)構造体の**bBPPminus1**メンバーに指定されている*BPP*が8の場合、マクロブロックデータは8ビットの符号なし値の形式で返されます (したがって、black はと Y = 16、Cb = Cr = 128、白はとです。Y = 235、Cb = Cr = 128)。 *BPP*が8より大きい場合、データは16ビットの符号なしの値の形式で返されます。

マクロブロックデータは、読み取り戻るコマンドバッファー自体のコピーの形式で、アクセラレータからホストに返されます。その後、次の32バイトのアラインメント境界への埋め込みが行われます。 次に、輝度およびクロミナンスデータのマクロブロックデータ値が、各マクロブロックの各ブロックのブロックごとに64サンプルという形式で、読み取り戻るコマンドバッファーに送信された順に返されます。

マクロブロック内の残存差ブロックは、MPEG 2 の図6-10、6-11、および 6-12 (マクロブロックの Y ブロックの場合はラスタースキャンの順序、その後に Cb の4:2:0 ブロック、その後に Cr の4:2:0 ブロックが続きます) で指定された順序で返されます。4:2:2 または4:4:4 のサンプリング操作の場合、4:2:0 ブロックの後には Cb の4:2:2 ブロックが続き、その後に Cr の4:2:2 ブロックが続きます。4:4:4 サンプリング操作の場合、4:2:2 ブロックの後に Cb の4:4:4 ブロックが続き、その後に Cr の4:4:4 ブロックが続きます。

 

 





