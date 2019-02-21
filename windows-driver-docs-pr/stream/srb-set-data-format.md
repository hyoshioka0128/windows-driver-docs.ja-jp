---
title: SRB\_設定\_データ\_形式
description: SRB\_設定\_データ\_形式
ms.assetid: a111ab92-a0a0-464e-ac13-f5be33ecd064
keywords:
- SRB_SET_DATA_FORMAT ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- SRB_SET_DATA_FORMAT
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75b6d550981ce1d1717984ebb3ded4ed6fe2a57a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536446"
---
# <a name="srbsetdataformat"></a>SRB\_設定\_データ\_形式


## <span id="ddk_srb_set_data_format_ks"></span><span id="DDK_SRB_SET_DATA_FORMAT_KS"></span>


クラスのドライバーでは、ストリームのデータ形式を設定するには、この要求を発行します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>ステータス\_成功  
コマンドが正常に完了を示します。

<span id="STATUS_NOT_SUPPORTED"></span><span id="status_not_supported"></span>ステータス\_いない\_サポートされています。  
ようにミニドライバーに要求されたデータの形式がサポートされていないことを示します。

### <a name="comments"></a>コメント

クラスのドライバーで新しいデータ形式を渡す、 **CommandData**.**OpenFormat**のメンバー、 *pSrb*ポインター。 (このポインターが指す、 [ **HW\_ストリーム\_要求\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff559702)構造です)。

データ形式の詳細については、次を参照してください。、 [Stream クラス ミニドライバー設計ガイド](https://msdn.microsoft.com/library/windows/hardware/ff568277)します。 参照してください[AVStream のデータ範囲の交差部分](https://msdn.microsoft.com/library/windows/hardware/ff558680)します。

 

 





