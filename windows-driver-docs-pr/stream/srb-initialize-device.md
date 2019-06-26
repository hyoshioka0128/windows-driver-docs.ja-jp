---
title: SRB\_初期化\_デバイス
description: SRB\_初期化\_デバイス
ms.assetid: a4e35253-43d8-4d11-8a5b-72a9863f6677
keywords:
- SRB_INITIALIZE_DEVICE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- SRB_INITIALIZE_DEVICE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30d7fc354725bde72905d99432b4a107142d161c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377905"
---
# <a name="srbinitializedevice"></a>SRB\_初期化\_デバイス


## <span id="ddk_srb_initialize_device_ks"></span><span id="DDK_SRB_INITIALIZE_DEVICE_KS"></span>


クラス ドライバーは、ミニドライバーのハードウェアの初期化を開始するときに、この要求を送信します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

ミニドライバーは、SRB の状態として、次のいずれかを設定する必要があります。

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>ステータス\_成功  
構成情報が正常に判別、ホスト アダプターが見つかったことを示します。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>ステータス\_IO\_デバイス\_エラー  
ホスト アダプターが検出されましたが、構成情報の取得中にエラーが発生したことを示します。 可能であれば、エラーをログに記録する必要があります。

<span id="STATUS_NO_SUCH_DEVICE"></span><span id="status_no_such_device"></span>ステータス\_いいえ\_かかる\_デバイス  
指定された構成情報が有効でなかったことを示します。

### <a name="comments"></a>コメント

クラスのドライバーが、ポートへのポインターを渡します\_構成\_情報の構造体で*pSrb*-&gt;**CommandData.ConfigInfo**します。 *PSrb*ポインターが指す、 [ **HW\_ストリーム\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_request_block)構造体。 ほとんどのフィールドに記入クラス ドライバー *pSrb*-&gt;**CommandData.ConfigInfo**オペレーティング システムからデバイスに関する情報を取得します。 ほとんどの状況では、ミニドライバーだけを埋めるために、 **StreamDescriptorSize**のメンバー **ConfigInfo**のサイズとその[ **HW\_ストリーム\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_descriptor)構造体。

 

 





