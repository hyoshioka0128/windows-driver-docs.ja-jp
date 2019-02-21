---
title: デバッグ\_要求\_ターゲット\_例外\_コンテキスト
description: デバッグ\_要求\_ターゲット\_例外\_コンテキスト
ms.assetid: e599a3f7-110b-46fc-8266-3a00ea1efe03
keywords:
- デバッグ DEBUG_REQUEST_TARGET_EXCEPTION_CONTEXT Windows
topic_type:
- apiref
api_name:
- DEBUG_REQUEST_TARGET_EXCEPTION_CONTEXT
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e85b67bfb58caa4d2715150a92d8ff9dabd5877
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551280"
---
# <a name="debugrequesttargetexceptioncontext"></a>デバッグ\_要求\_ターゲット\_例外\_コンテキスト


デバッグ\_要求\_ターゲット\_例外\_コンテキスト[**要求**](request.md)操作は戻り、[スレッド コンテキスト](https://msdn.microsoft.com/library/windows/hardware/ff554702#thread-context)ユーザー モードのミニダンプ ファイル ストアド イベント。

**パラメーター**

<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
使用されません。

<span id="OutBuffer"></span><span id="outbuffer"></span><span id="OUTBUFFER"></span>*OutBuffer*  
ストアドのイベントのスレッド コンテキスト。 スレッド コンテキストの種類は、イベントの時点で、ターゲットの有効なプロセッサのコンテキスト構造です。 *OutBuffer*この構造体を保持するために十分な大きさである必要があります。

<a name="remarks"></a>注釈
-------

この情報にも返されます、*コンテキスト*パラメーターによって、 [ **GetStoredEventInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff548431)メソッド。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**要求**](request.md)

[**GetStoredEventInformation**](https://msdn.microsoft.com/library/windows/hardware/ff548431)

 

 






