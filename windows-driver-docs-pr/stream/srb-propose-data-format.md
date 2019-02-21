---
title: SRB\_提案\_データ\_形式
description: SRB\_提案\_データ\_形式
ms.assetid: a15ec7cc-7351-4a63-ad35-e59610205913
keywords:
- SRB_PROPOSE_DATA_FORMAT ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- SRB_PROPOSE_DATA_FORMAT
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 325f5403ad585813e81b06c3b8eb505c1a9cd5d0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560151"
---
# <a name="srbproposedataformat"></a>SRB\_提案\_データ\_形式


## <span id="ddk_srb_propose_data_format_ks"></span><span id="DDK_SRB_PROPOSE_DATA_FORMAT_KS"></span>


クラスのドライバーでは、ストリームが指定されたデータ形式をサポートするかどうかを判断するには、この要求を発行します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

ミニドライバーは、SRB の状態として、次のいずれかを設定する必要があります。

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>ステータス\_成功  
コマンドが正常に完了を示します。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>ステータス\_いない\_実装されていません  
関数が、ミニドライバーでサポートされていないことを示します。

<span id="STATUS_NOT_SUPPORTED"></span><span id="status_not_supported"></span>ステータス\_いない\_サポートされています。  
提案された形式が、ミニドライバーでサポートされていないことを示します。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>ステータス\_IO\_デバイス\_エラー  
ハードウェア障害が発生したことを示します。

### <a name="comments"></a>コメント

クラス ドライバーが受信すると、 [ **KSPROPERTY\_接続\_PROPOSEDATAFORMAT** ](ksproperty-connection-proposedataformat.md)要求、提案された形式がサポートされているかどうかを判断するこの SRB コードを使用します。 クラスのドライバーで提案されたデータ形式を通過する、 **CommandData**.**OpenFormat**によって示されるメンバー *pSrb*します。 *PSrb*ポインターが指す、 [ **HW\_ストリーム\_要求\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff559702)構造体。

ミニドライバーは、データ形式をサポートしていない場合は設定*pSrb*-&gt;**状態**ステータス\_いない\_サポートされています。 このフィールドは、状態を設定が、ミニドライバーは、ストリームを指定した形式に切り替えることが場合、\_成功します。

ミニドライバーは、新しい形式を受け入れることは場合、クラス ドライバーが後で送信できます、ミニドライバーで示される形式の変更、 **OptionsFlags**内のメンバー、 [ **KSSTREAM\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff567138)構造体。

## <a name="see-also"></a>関連項目


[**SRB\_設定\_データ\_形式**](srb-set-data-format.md)

[SRB\_取得\_データ\_形式](srb-get-data-format.md)

 

 






