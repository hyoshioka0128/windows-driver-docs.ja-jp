---
title: デバッグ\_要求\_設定\_追加\_作成\_オプション
description: デバッグ\_要求\_設定\_追加\_作成\_オプション
ms.assetid: e80f8575-b7f9-466a-8087-b3cb103503f7
keywords:
- デバッグ DEBUG_REQUEST_SET_ADDITIONAL_CREATE_OPTIONS Windows
topic_type:
- apiref
api_name:
- DEBUG_REQUEST_SET_ADDITIONAL_CREATE_OPTIONS
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a443041865d023db1669747a1b03a4bd9696bc1c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349044"
---
# <a name="debugrequestsetadditionalcreateoptions"></a>デバッグ\_要求\_設定\_追加\_作成\_オプション


デバッグ\_要求\_設定\_追加\_作成\_オプション[**要求**](request.md)操作は、既定のプロセスの作成を設定します。オプション。

**Parameters**

<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
新しい既定のプロセスの作成オプション。 プロセスの作成オプションの種類は[**デバッグ\_作成\_プロセス\_オプション**](https://msdn.microsoft.com/library/windows/hardware/ff541464)します。

<span id="OutBuffer"></span><span id="outbuffer"></span><span id="OUTBUFFER"></span>*OutBuffer*  
使用されていません。

<a name="remarks"></a>注釈
-------

既定のプロセス作成のオプションがメソッドで使用される[ **CreateProcess** ](https://msdn.microsoft.com/library/windows/hardware/ff539321)と[ **CreateProcessAndAttach** ](https://msdn.microsoft.com/library/windows/hardware/ff540048) とは異なり、この[**CreateProcess2** ](https://msdn.microsoft.com/library/windows/hardware/ff539323)と[ **CreateProcessAndAttach2**](https://msdn.microsoft.com/library/windows/hardware/ff540055)、プロセス作成オプションの完全な範囲を指定しません。

**CreateFlags**のフィールド、 [**デバッグ\_作成\_プロセス\_オプション**](https://msdn.microsoft.com/library/windows/hardware/ff541464)ために、構造体は、既定値として使用されませんすべてプロセス作成操作では、この情報を提供します。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**要求**](request.md)

[**デバッグ\_要求\_取得\_追加\_作成\_オプション**](debug-request-get-additional-create-options.md)

[**デバッグ\_作成\_プロセス\_オプション**](https://msdn.microsoft.com/library/windows/hardware/ff541464)

[**CreateProcess**](https://msdn.microsoft.com/library/windows/hardware/ff539321)

[**CreateProcessAndAttach**](https://msdn.microsoft.com/library/windows/hardware/ff540048)

 

 






