---
title: デバッグ\_要求\_ターゲット\_できます\_デタッチ
description: デバッグ\_要求\_ターゲット\_できます\_デタッチ
ms.assetid: 1e36715e-3414-4cd2-95f3-2b97878a3989
keywords:
- デバッグ DEBUG_REQUEST_TARGET_CAN_DETACH Windows
topic_type:
- apiref
api_name:
- DEBUG_REQUEST_TARGET_CAN_DETACH
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5bfc79d7b0e607a14a6500adfc84608e9ae0990
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349042"
---
# <a name="debugrequesttargetcandetach"></a>デバッグ\_要求\_ターゲット\_できます\_デタッチ


デバッグ\_要求\_ターゲット\_できます\_デタッチ[**要求**](request.md)デバッガー エンジンからデタッチ可能かどうかを操作のチェック現在のプロセス (実行中のプロセスを離れることが不要になったデバッグ対象)。

**Parameters**

<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
使用されていません。

<span id="OutBuffer"></span><span id="outbuffer"></span><span id="OUTBUFFER"></span>*OutBuffer*  
使用されていません。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

<span id="S_OK"></span><span id="s_ok"></span>S\_OK  
現在のプロセスからデバッガーをデタッチすることになります。

<span id="S_FALSE"></span><span id="s_false"></span>S\_FALSE  
現在のプロセスからデバッガーをデタッチすることはできません。

<a name="remarks"></a>注釈
-------

Microsoft Windows XP または Windows の以降のバージョンで実行されているターゲットのみをサポート プロセスからデバッガーをデタッチします。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**要求**](request.md)

 

 






