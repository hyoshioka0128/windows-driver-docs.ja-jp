---
title: ビデオのデコード
description: ビデオのデコード
ms.assetid: d434469f-1279-47c4-b824-61daeb25b214
keywords:
- ビデオデコード WDK DirectX VA、ビデオのデコードについて
- ビデオのデコードに関するビデオ WDK DirectX VA、ビデオのデコード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 499a7929ba429ef464bf8dc8a411563270d10f40
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839017"
---
# <a name="decoding-video"></a>ビデオのデコード


Microsoft Direct3D ランタイムは、ユーザーモードのディスプレイドライバーの[**DecodeBeginFrame**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_decodebeginframe)関数と[**DecodeEndFrame**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_decodeendframe)関数を呼び出して、ユーザーモードディスプレイドライバーがビデオをデコードできるこれらの関数呼び出しの間の期間を示します。 ユーザーモード表示ドライバーがビデオデコード操作を実行できるようにするには、Microsoft Direct3D ランタイムがユーザーモードの表示ドライバーの[**SetDecodeRenderTarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_setdecoderendertarget)関数を呼び出して、これらのデコード操作のレンダーターゲットサーフェイスを設定する必要があります。 ただし、 **SetDecodeRenderTarget**の呼び出しは、開始フレームと終了フレームの間にのみ発生します。

保護モードで[**DecodeBeginFrame**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_decodebeginframe)を呼び出すと、Direct3D ランタイムは、 [**D3DDDIARG\_DecodeBeginFrame**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_decodebeginframe)構造体の**ppvpsetkey**メンバーが指す変数内の DirectX VA コンテンツキーを設定または変更します。 デコードデバイスは、このキーを使用して、このと後続のフレームの圧縮された DirectX VA バッファーの転送に使用します。

  、Direct3D ランタイムは、キーを変更または設定するためだけに**Ppvpsetkey**ポインターを設定する**ことに注意**してください。 以前に設定したキーを使用したままにするために、ランタイムはポインターを**NULL**に設定して、同じキーの再読み込みに時間がかかる可能性を回避します。 ドライバーでは、冗長設定は削除されません。 デコーダーアプリケーションでは、重複する設定を避ける必要があります。

 

デコード操作のレンダーターゲットサーフェイスが設定されると、ユーザーモードの表示ドライバーは、 [**DecodeExecute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_decodeexecute)関数の呼び出しを受信して、開始フレームと終了期間の間にビデオデコード操作を実行できます。

[**DecodeExecute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_decodeexecute)の呼び出しでは、PCOMPRESSEDBUFFERS [ **\_D3DDDIARG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_decodeexecute)構造体の**DECODEEXECUTE 配列の** [**DXVADDI\_DECODEBUFFERDESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_decodebufferdesc)構造体に指定されているすべてのバッファーの種類**は、D3DDDIARG**\_DecodeExecute の**hdecode**メンバーが指定するデコード GUID ごとに使用されます。 たとえば、スライスコントロール (D3DDDIFMT\_SLICECONTROLDATA)、逆量子化 (D3DDDIFMT\_INVERSEQUANTIZATIONDATA)、およびビットストリーム (D3DDDIFMT\_BITSTREAMDATA) バッファーは、可変長デコード (VLD) 処理にのみ必要であり、deblocking コントロールバッファー (D3DDDIFMT\_DEBLOCKINGDATA) は MPEG 2 では使用されません。

保護モードでは、コンテンツキーを持つ保護された転送のために暗号化されたバッファーには、バッファー記述子内の初期カウンター値へのポインターが含まれます (つまり、 [**DXVADDI\_DECODEBUFFERDESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_decodebufferdesc)構造体の**pCipherCounter**メンバーが指す変数)。 ユーザーモード表示ドライバーの[**DecodeExecute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_decodeexecute)関数を呼び出すたびに、 **DecodeExecute**がデコード操作でバッファーのデータを使用する前に、そのようなバッファーをローカルビデオメモリに転送する必要があります。 ただし、残留差 (D3DDDIFMT\_RESIDUALDIFFERENCEDATA) とビットストリーム (D3DDDIFMT\_BITSTREAMDATA) 型以外の型の DirectX VA 圧縮バッファーを暗号化するためのプランは存在しません。

 

 





