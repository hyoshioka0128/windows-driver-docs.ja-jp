---
title: IPrinterBidiSchemaElement Value メソッド
description: Value メソッドは、Bidi スキーマ要素の値を返します。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: F989AFEF-795D-4C1A-880D-58CBC2D2B021
keywords:
- 印刷デバイス メソッドを値します。
- 印刷デバイス、IPrinterBidiSchemaElement インターフェイスのメソッドを値します。
- IPrinterBidiSchemaElement インターフェイス印刷デバイス、Value メソッド
topic_type:
- apiref
api_name:
- IPrinterBidiSchemaElement.Value
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 093e89237a40fe25e9428848e8f0db8995161e56
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357212"
---
# <a name="iprinterbidischemaelementvalue-method"></a>IPrinterBidiSchemaElement::Value メソッド

Value メソッドは、Bidi スキーマ要素の値を返します。

<a name="syntax"></a>構文
------

```cpp
HRESULT Value(
  [out, retval] VARIANT *pValue
);
```

<a name="parameters"></a>パラメーター
----------

*pValue* \[out, retval\]  
返される要素の値。

<a name="return-value"></a>戻り値
------------

このメソッドが戻る、 **HRESULT**値。

## <a name="see-also"></a>関連項目

[**IPrinterBidiSchemaElement**](iprinterbidischemaelement-interface.md)
