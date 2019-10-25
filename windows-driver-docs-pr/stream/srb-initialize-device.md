---
title: SRB\_\_デバイスの初期化
description: SRB\_\_デバイスの初期化
ms.assetid: a4e35253-43d8-4d11-8a5b-72a9863f6677
keywords:
- SRB_INITIALIZE_DEVICE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- SRB_INITIALIZE_DEVICE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ea313ca253460e7843b20d8c21f624091d06185
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843295"
---
# <a name="srb_initialize_device"></a>SRB\_\_デバイスの初期化


## <span id="ddk_srb_initialize_device_ks"></span><span id="DDK_SRB_INITIALIZE_DEVICE_KS"></span>


クラスドライバーは、ミニドライバーのハードウェアの初期化を開始するときにこの要求を送信します。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

ミニドライバーは、SRB の状態として次のいずれかを設定する必要があります。

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状態\_成功  
ホストアダプターが見つかり、構成情報が正常に決定されたことを示します。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>状態\_IO\_デバイス\_エラー  
ホストアダプターが見つかったが、構成情報の取得中にエラーが発生したことを示します。 可能であれば、エラーをログに記録する必要があります。

<span id="STATUS_NO_SUCH_DEVICE"></span><span id="status_no_such_device"></span>\_デバイスの状態\_\_いいえ  
指定された構成情報が無効であることを示します。

### <a name="comments"></a>コメント

クラスドライバーは、 *pSrb*-&gt;**Commanddata. CONFIGINFO**のポート\_構成\_情報構造体へのポインターを渡します。 *PSrb*ポインターは、 [ **\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)構造体を指す HW\_ストリームを指します。 クラスドライバーは、 *pSrb*-&gt;**Commanddata. configinfo**のほとんどのフィールドに、オペレーティングシステムからデバイスについて取得した情報を入力します。 ほとんどの場合、ミニドライバーでは、 **Configinfo**の**streamdescriptor size**メンバーに、 [**HW\_ストリームの\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_descriptor)構造のサイズを設定する必要があります。

 

 





