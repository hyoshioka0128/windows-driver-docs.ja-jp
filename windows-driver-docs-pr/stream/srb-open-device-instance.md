---
title: SRB\_オープン\_デバイス\_インスタンス
description: SRB\_オープン\_デバイス\_インスタンス
ms.assetid: 71f57abd-7875-4c7a-bbb3-c5c45c9a83ab
keywords:
- SRB_OPEN_DEVICE_INSTANCE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- SRB_OPEN_DEVICE_INSTANCE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba54fe8fde7331c633373de02acc54b41aa6af6d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387105"
---
# <a name="srbopendeviceinstance"></a>SRB\_オープン\_デバイス\_インスタンス


## <span id="ddk_srb_open_device_instance_ks"></span><span id="DDK_SRB_OPEN_DEVICE_INSTANCE_KS"></span>


クラスのドライバーでは、アダプターのインスタンスを開くには、この要求を送信します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

ミニドライバーは、SRB の状態として、次のいずれかを設定する必要があります。

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>ステータス\_成功  
コマンドが正常に完了を示します。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>ステータス\_いない\_実装されていません  
関数が、ミニドライバーでサポートされていないことを示します。

<span id="STATUS_TOO_MANY_NODES"></span><span id="status_too_many_nodes"></span>ステータス\_すぎます\_多く\_ノード  
このストリームを開くには、十分なリソースがないことを示します。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>ステータス\_IO\_デバイス\_エラー  
ハードウェア障害が発生したことを示します。

### <a name="comments"></a>コメント

ミニドライバーは、デバイスの複数のインスタンスをサポートする場合、このコマンドは、アダプターの新しいインスタンスを開くたびに、クラス ドライバーによって送信されます。 たとえば、DSP デコーダーを割り当てることができますを検討してください。 *n*指定されたストリームのインスタンスの数。 **HwInstanceExtension**クラス ドライバーによってミニドライバーのインスタンスごとのワークスペースに、SRB のフィールドが設定し、必要があります。

ほとんどのアダプターが複数のインスタンスをサポートしてそのような場合は、 **FilterInstanceExtensionSize**フィールドに、 **HW\_初期化\_データ**に構造体を設定する必要があります0 し、このコマンドを受信しない必要があります。

## <a name="see-also"></a>関連項目


[**SRB\_閉じる\_デバイス\_インスタンス**](srb-close-device-instance.md)

 

 






