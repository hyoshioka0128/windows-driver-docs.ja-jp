---
title: SRB\_開いている\_ストリーム
description: SRB\_開いている\_ストリーム
ms.assetid: 53732add-e304-4128-9235-525ff073d777
keywords:
- SRB_OPEN_STREAM ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- SRB_OPEN_STREAM
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c5731cd17a738868667a0bd25e9c2906eda6556
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843289"
---
# <a name="srb_open_stream"></a>SRB\_開いている\_ストリーム


## <span id="ddk_srb_open_stream_ks"></span><span id="DDK_SRB_OPEN_STREAM_KS"></span>


クラスドライバーは、この要求を送信してストリームを開きます。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

ミニドライバーは、SRB の状態として次のいずれかを設定する必要があります。

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状態\_成功  
コマンドが正常に完了したことを示します。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状態\_\_実装されていません  
関数がミニドライバーによってサポートされていないことを示します。

<span id="STATUS_TOO_MANY_NODES"></span><span id="status_too_many_nodes"></span>ステータス\_多くの\_ノード\_すぎます  
このストリームを開くためのリソースが不足していることを示します。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>状態\_IO\_デバイス\_エラー  
ハードウェア障害が発生したことを示します。

### <a name="comments"></a>コメント

クラスドライバーは、 *pSrb*-&gt;**Streamobject**-&gt;streamobject を使用して、 *pSrb*-&gt;**streamobject** [ **\_オブジェクトバッファーに HW\_ストリーム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_object)を提供します。を開くストリームの番号をに設定します。 *PSrb*ポインターは、 [ **\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)構造体を指す HW\_ストリームを指します。 **Streamnumber**は、 [**SRB\_GET\_stream\_INFO**](srb-get-stream-info.md)要求に応答してミニドライバーが提供する、 [**HW\_ストリーム\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_descriptor)構造内のストリームのオフセットに対応します。 クラスドライバーは、開いているストリームが*pSrb*-&gt;**commanddata**-&gt;**openformat**で提供する必要があるデータ形式を指定します。

ミニドライバーは、この要求を受信すると、指定されたストリームをこの時点で開くことができるかどうかを判断する必要があります。 また、ミニドライバーは、渡された[**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)形式も検証する必要があります。 SRB の OpenFormat フィールド。 ストリームを開くことができる場合、ミニドライバーは、HW\_ストリーム\_オブジェクト構造を更新し、STATUS\_SUCCESS を返します。 ストリームインスタンスの最大数が既に開いている場合、またはこのストリームを開くために必要なハードウェアリソースが使用できない場合、ミニドライバーは適切なエラー状態を返します。

**SRB\_OPEN\_STREAM コマンドがミニドライバーによって受信されると、ミニドライバーは次のことを行う必要があります。**

1.  ストリームインスタンスの最大数が超過していないこと、およびストリームインデックスの値が有効であることを確認してください。

2.  要求されたデータ形式がこのストリームに対して有効であることを確認してください。

3.  ストリームの形式を設定します。

4.  任意のストリームから Irp を取り消すことができるように、デバイス拡張機能のすべてのストリーム拡張構造の配列を保持します。

5.  ストリームオブジェクトのポインターをストリームデータハンドラーとコントロールハンドラーに指定します。

6.  **ReceiveDataPacket**ルーチンに渡されたデータバッファーアドレスに対してデバイスが dma を直接実行する場合は、ストリームオブジェクトの dma フラグを設定します。 論理アドレス指定を使用して渡されたデータバッファーにドライバーがアクセスする場合は、ストリームオブジェクトで PIO フラグも設定します。

7.  ストリームでクロックサポートを利用できる場合は、ストリームオブジェクトの**HwClockObject**メンバーを通じてこれを示します。

 

 





