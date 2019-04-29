---
title: PRINTERBIDISCHEMAELEMENTTYPE 列挙型
description: 双方向の操作で転送されるデータの有効な値を指定します。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 18F2325D-DA22-4D73-8560-62FDEF1E04A8
keywords:
- PRINTERBIDISCHEMAELEMENTTYPE 列挙印刷デバイス
topic_type:
- apiref
api_name:
- PRINTERBIDISCHEMAELEMENTTYPE
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6958248a166aa14b697c6db663230cef1385207
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390273"
---
# <a name="printerbidischemaelementtype-enumeration"></a>PRINTERBIDISCHEMAELEMENTTYPE 列挙型

双方向の操作で転送されるデータの有効な値を指定します

<a name="syntax"></a>構文
------

```cpp
typedef enum _PRINTERBIDISCHEMAELEMENTTYPE { 
  PrinterBidiSchemaElementType_Null    = 0,
  PrinterBidiSchemaElementType_Int     = 1,
  PrinterBidiSchemaElementType_Float   = 2,
  PrinterBidiSchemaElementType_Bool    = 3,
  PrinterBidiSchemaElementType_String  = 4,
  PrinterBidiSchemaElementType_Text    = 5,
  PrinterBidiSchemaElementType_Enum    = 6,
  PrinterBidiSchemaElementType_Blob    = 7
} PRINTERBIDISCHEMAELEMENTTYPE;
```

<a name="constants"></a>定数
---------

**PrinterBidiSchemaElementType\_Null**  
データがありません。

**PrinterBidiSchemaElementType\_Int**  
データは、整数です。

**PrinterBidiSchemaElementType\_Float**  
データは、浮動小数点数です。

**PrinterBidiSchemaElementType\_Bool**  
データは、ブール値です。

**PrinterBidiSchemaElementType\_文字列**  
データは、Unicode 文字の文字列です。

**PrinterBidiSchemaElementType\_Text**  
データは、ローカライズできない Unicode 文字列です。

**PrinterBidiSchemaElementType\_列挙型**  
データは、Unicode 文字列です。

**PrinterBidiSchemaElementType\_Blob**  
データはバイナリ データです。

## <a name="see-also"></a>関連項目

[**BidiType**](iprinterbidischemaelement-biditype.md)
