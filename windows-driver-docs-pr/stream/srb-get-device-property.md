---
title: SRB\_取得\_デバイス\_プロパティ
description: SRB\_取得\_デバイス\_プロパティ
ms.assetid: 2a0a3b8a-7252-4ba5-a1a5-ffef0f0f5715
keywords:
- SRB_GET_DEVICE_PROPERTY ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- SRB_GET_DEVICE_PROPERTY
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb6c684c785322aa18c7950b4d26f3b8f5e27bd9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390875"
---
# <a name="srbgetdeviceproperty"></a>SRB\_取得\_デバイス\_プロパティ


## <span id="ddk_srb_get_device_property_ks"></span><span id="DDK_SRB_GET_DEVICE_PROPERTY_KS"></span>


クラスのドライバーでは、ミニドライバー定義のプロパティのプロパティの get 要求を完了するために必要なデータのミニドライバーを照会するには、この要求を送信します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

ミニドライバーは、SRB の状態として、次のいずれかを設定する必要があります。

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>ステータス\_成功  
コマンドが正常に完了を示します。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>ステータス\_いない\_実装されていません  
関数が、ミニドライバーでサポートされていないことを示します。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>ステータス\_IO\_デバイス\_エラー  
ハードウェア障害が発生したことを示します。

### <a name="comments"></a>コメント

クラス ドライバーは、操作のパラメーターを渡す、 *pSrb*-&gt;**CommandData.PropertyInfo**バッファー、フォームの構造[ **ストリーム\_プロパティ\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff568442)します。 *PSrb*ポインターが指す、 [ **HW\_ストリーム\_要求\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff559702)構造体。 **プロパティ**ストリームのメンバー\_プロパティ\_記述子には、問題の中にプロパティがについて説明します、 **PropertyInfo**メンバー プロパティのデータをコピーするバッファーを指定します。します。 バッファーが小さすぎる場合、ミニドライバーを設定する必要があります、**状態**のメンバー *pSrb*ステータス\_バッファー\_オーバーフローが発生します。

プロパティ セットの詳細については、次を参照してください。 [KS プロパティ](https://msdn.microsoft.com/library/windows/hardware/ff567671)します。

## <a name="see-also"></a>関連項目


[**ストリーム\_プロパティ\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff568442)

 

 






