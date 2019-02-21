---
title: SRB\_ページング\_アウト\_ドライバー
description: SRB\_ページング\_アウト\_ドライバー
ms.assetid: 9bcb9f07-6fea-427b-9ae8-afdc6aec540f
keywords:
- SRB_PAGING_OUT_DRIVER ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- SRB_PAGING_OUT_DRIVER
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1282416ab7aeab03e4e8bf2fe1ab44a906cc8110
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532397"
---
# <a name="srbpagingoutdriver"></a>SRB\_ページング\_アウト\_ドライバー


## <span id="ddk_srb_paging_out_driver_ks"></span><span id="DDK_SRB_PAGING_OUT_DRIVER_KS"></span>


クラス ドライバーの詳細についてはそれを通知するには、この要求の送信、ミニドライバーをページにします。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

ミニドライバーは、SRB の状態として、次のいずれかを設定する必要があります。

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>ステータス\_成功  
コマンドが正常に完了を示します。

### <a name="comments"></a>コメント

クラス ドライバーは、のみが存在しない場合、開いているストリームまたはデバイスは、ページ、ミニドライバー アウトしようとします。 保留中のコールバックがこの状態で、ミニドライバーが必要がある可能性がある、ミニドライバーは、この SRB の受信時に、未処理のコールバックを取り消す必要があります。 ミニドライバーはアダプターの割り込みを無効にして状態を返します\_成功します。

ミニドライバーは、この機能を有効にする場合にのみ、ミニドライバーをクラス ドライバー ページ。 ミニドライバーは、デバイスの INF ファイルで、レジストリ変数 PageOutWhenUnopened を 1 に設定してこの機能を有効します。 詳細については、ミニドライバーの Inf のストリーミングのサンプルを参照してください。

 

 





