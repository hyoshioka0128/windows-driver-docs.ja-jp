---
title: Edge のフィルター処理のコマンド (バイト)
description: Edge のフィルター処理のコマンド (バイト)
ms.assetid: eefb580a-133d-4c9e-a8d2-2d114107e2ea
keywords:
- マクロ ブロック WDK DirectX va なので、フィルター コントロールを非ブロック化
- フィルター コントロール WDK DirectX VA 非ブロック化
- フィルター処理の WDK DirectX VA をエッジします。
- 読み取りバック バッファー WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 933880b385a3bf0098e0d90ea6d64a025b926ea4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553498"
---
# <a name="edge-filtering-command-bytes"></a>Edge のフィルター処理のコマンド (バイト)


## <span id="ddk_edge_filtering_command_bytes_gg"></span><span id="DDK_EDGE_FILTERING_COMMAND_BYTES_GG"></span>


コントロールのコマンドをフィルター処理する各エッジは、1 バイトで構成されます。 *DXVA\_DeblockingEdgeControl*で定義された定数*dxva.h*エッジの非ブロック化する方法を定義します。 処理されます。 バイトの 7 の最上位ビットを含む、 *EdgeFilterStrength*変数、および最下位ビットは、 *EdgeFilterOn*フラグ。

指定されている H.263 Annex J. として実行エッジ フィルタ リング*EdgeFilterStrength*変数を実行する、フィルター選択の強度を指定します。 *EdgeFilterOn*フラグは、実行するかどうかは、フィルター処理を指定します。 *EdgeFilterOn*エッジでは、フィルター処理される場合は 0 を場合は 1 です。

エッジ フィルタ リング (のエッジの*EdgeFilterOn* 1) は強度値で指定された実行と等しく*EdgeFilterStrength*と 0 ~ 2 の範囲に出力をクリッピング<sup>(BPP)</sup> - 1。 上端までのすべてのブロックのフィルター処理は、上部エッジ フィルタ リングを使用するサンプルの値は左端のフィルター処理するため、deblocking フィルター処理する前にそれらの再構築された値でなければならないために、すべてのブロックの左端をフィルター処理する前に実行されます。

場合、 **bPicDeblockConfined**のメンバー、 [ **DXVA\_PictureParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff564012)構造がそのサンプルを示しますマクロ ブロックの外側の値、現在の非ブロック化フィルター コマンド バッファーは影響しません、 *EdgeFilterOn*フラグは、左、バッファー内のフィルターのコマンドを非ブロック化をマクロ ブロック対象領域の上部にあるすべての端に 0 です。

### <a name="span-idread-backbuffersspanspan-idread-backbuffersspanspan-idread-backbuffersspanread-back-buffers"></a><span id="Read-Back_Buffers"></span><span id="read-back_buffers"></span><span id="READ-BACK_BUFFERS"></span>読み取りバック バッファー

1 つの読み戻しコマンド バッファーがアクセラレータに渡されるときに、 **bPicReadbackRequests**のメンバー、 [ **DXVA\_PictureParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff564012)構造体は 1 です。 このバッファー内のデータをホストに (非ブロック化、該当する場合) の後、結果として得られる最終的な画像マクロ ブロック データを返す、アクセラレータのコマンドです。 暗号化プロトコルを使用している場合、アクセラレータがバックアップ - 読み取り要求 (暗号化プロトコルによって指定できます) と、エラーを示す値、エラーのあるデータ、または暗号化されたデータを返すことによって応答があります。

アクセラレータに渡された読み戻しコマンド バッファーは、1 つから成る読み戻しコマンドを含める必要があります**wMBaddress**読み取られる、マクロ ブロックのマクロ ブロック コントロール コマンドのメンバー。 **WMBaddress**メンバーがラスター スキャンの順序で現在のマクロ ブロックのマクロ ブロックのアドレスを指定する 16 ビット値。 ラスター スキャン order (に基づいて、 **wPicWidthInMBminus1**と**wPicHeightInMBminus1**のメンバー、 [ **DXVA\_PictureParameters**](https://msdn.microsoft.com/library/windows/hardware/ff564012)構造) が次のように定義されています。

-   0 は、左のマクロ ブロックのアドレスです。

-   **wPicWidthInMBminus1**右マクロ ブロックのアドレスです。

-   **wPicHeightInMBminus1** x (**wPicWidthInMBminus1**+1)、左下のマクロ ブロックのアドレスです。

-   (**wPicHeightInMBminus1**+1) x (**wPicWidthInMBminus1**+1)-1、右下のマクロ ブロックのアドレスになります。

場合*BPP*で指定されている、 **bBPPminus1**のメンバー、 [ **DXVA\_PictureParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff564012)構造体は、8、8 ビット符号なしの値の形式でマクロ ブロックのデータが返されます (したがって、黒、名目上 Y = 16, Cb Cr を = = 128 であり、白い名目上 Y = 235、Cb Cr を = = 128)。 場合*BPP*が 8 よりも大きい 16 ビット符号なしの値の形式でデータが返されます。

マクロ ブロックのデータは、埋め込み、続けて [次へ] の 32 バイト アラインメントの境界を読み戻しコマンド バッファー自体のコピーの形式でホストするアクセラレータから返されます。 次に、輝度とクロミナンスのデータのマクロ ブロックのデータ値は、各マクロ ブロック内の各ブロックのブロックあたり 64 のサンプルのフォームでの読み戻しコマンド バッファーに送信された順序で返されます。

マクロ ブロック内の残存違いブロックが指定の mpeg-2 図 6 ~ 10、11、6 と 6 ~ 12 の順序で返されます (ラスター スキャン順序 Y マクロ ブロック、ブロックの後に、4:2:0 ブロックの後に、4、Cb: Cr のブロックを 2:0。場合は、4:2:2 または 4: 4、4:4 サンプリング操作: 2:0 ブロックの後、4 では: Cb、後に、4 のブロックを 2:2: Cr の 2:2 ブロックします。4 の場合: 4、4:4 サンプリング操作: 2:2 ブロックの後、4 では: Cb、後に、4 のブロックを 4:4: Cr のブロックを 4:4)。

 

 





