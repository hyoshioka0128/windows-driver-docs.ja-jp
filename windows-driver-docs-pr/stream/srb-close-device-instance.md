---
title: SRB\_閉じる\_デバイス\_インスタンス
description: SRB\_閉じる\_デバイス\_インスタンス
ms.assetid: 55a72f4f-45b3-427d-80b7-620aac870a8a
keywords:
- SRB_CLOSE_DEVICE_INSTANCE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- SRB_CLOSE_DEVICE_INSTANCE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7908f944c2963d06457925f344c4f3456f2bb3ed
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552672"
---
# <a name="srbclosedeviceinstance"></a>SRB\_閉じる\_デバイス\_インスタンス


## <span id="ddk_srb_close_device_instance_ks"></span><span id="DDK_SRB_CLOSE_DEVICE_INSTANCE_KS"></span>


クラスのドライバーでは、以前に開かれて、アダプターのインスタンスを閉じるには、この要求を送信します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

ミニドライバーは、SRB の状態として、次のいずれかを設定する必要があります。

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>ステータス\_成功  
コマンドが正常に完了を示します。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>ステータス\_いない\_実装されていません  
関数が、ミニドライバーでサポートされていないことを示します。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>ステータス\_IO\_デバイス\_エラー  
ハードウェア障害が発生したことを示します。

### <a name="comments"></a>コメント

ほとんどのアダプターが複数のインスタンスをサポートしてそのような場合は、 **FilterInstanceExtensionSize**フィールドに、 [ **HW\_初期化\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff559682)構造が 0 に設定する必要があり、このコマンドを受信しない必要があります。

 

 





