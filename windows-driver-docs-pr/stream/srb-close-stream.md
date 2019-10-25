---
title: SRB\_CLOSE\_ストリーム
description: SRB\_CLOSE\_ストリーム
ms.assetid: e118ddd7-fe0e-4834-9ae6-19eef0348b2c
keywords:
- SRB_CLOSE_STREAM ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- SRB_CLOSE_STREAM
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 697cab677d0554c5730047e8b165f3d7cc904643
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843306"
---
# <a name="srb_close_stream"></a>SRB\_CLOSE\_ストリーム


## <span id="ddk_srb_close_stream_ks"></span><span id="DDK_SRB_CLOSE_STREAM_KS"></span>


クラスドライバーは、この要求を送信してストリームを閉じます。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

ミニドライバーは、SRB の状態として次のいずれかを設定する必要があります。

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状態\_成功  
コマンドが正常に完了したことを示します。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状態\_\_実装されていません  
関数がミニドライバーによってサポートされていないことを示します。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>状態\_IO\_デバイス\_エラー  
ハードウェア障害が発生したことを示します。

### <a name="comments"></a>コメント

クラスドライバーは、 *pSrb*-&gt;**Streamobject**-&gt;streamobject を使用して、 *pSrb*-&gt;**streamobject** [ **\_オブジェクトバッファーに HW\_ストリーム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_object)を提供します。は、閉じられるストリームの番号に設定されます。 *PSrb*ポインターは、 [ **\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)構造体を指す HW\_ストリームを指します。 **Streamnumber**は、 [**SRB\_GET\_stream\_INFO**](srb-get-stream-info.md)要求に応答してミニドライバーが提供する、 [**HW\_ストリーム\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_descriptor)構造内のストリームのオフセットに対応します。

ミニドライバーがストリームを正常に閉じた場合、ミニドライバーは STATUS\_SUCCESS を返します。 それ以外の場合は、適切なエラー状態を返します。

**SRB\_CLOSE\_STREAM コマンドがミニドライバーによって受信されると、応答するミニドライバールーチンは次のようになります。**

1.  ストリームを開いたときにミニドライバーによって割り当てられたすべてのリソースを解放します。

2.  クロックがストリームに使用された場合は、クロックの参照を停止します。

3.  ストリームの状態をリセットして停止します。

ストリームは、関連付けられたユーザーモードアプリケーションがクラッシュした場合に、ストリーミング中に任意で閉じられる可能性があることに注意してください。 そのため、ストリームのすべての未処理リソースを解放し、ストリームの保留中のすべての SRBs を完了して、ストリームを休止状態に戻す必要があります。

 

 





