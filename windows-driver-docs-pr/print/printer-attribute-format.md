---
title: プリンター属性形式
description: プリンター属性形式
ms.assetid: 676e9220-4990-4581-8f23-79083afc311c
keywords:
- プリンターは、WDK Unidrv、形式を属性します。
- WDK のプリンターの属性の形式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79c2d9dd6cae9cf39fd31f135b288ed2b6b452b8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380538"
---
# <a name="printer-attribute-format"></a>プリンター属性形式





GPD ファイルでプリンターの属性エントリを指定するには、次の形式を使用します。

\* *AttributeName* :*AttributeValue*

場所*AttributeName*のいずれかに属している事前定義された名前は、[属性型](attribute-types.md)と*AttributeValue*の 1 つ、 [GPD 値型](gpd-value-types.md).

たとえば、 \*ModelName 属性は、プリンターのハードウェアを説明するテキスト文字列を指定するために使用します。 にこの属性に値を割り当てるには、GPD ファイルで、次の行を配置する可能性があります。

```cpp
*ModelName: "Canon Bubble-Jet BJC-600"
```

すべての属性名は、あらかじめ定義されてし、Unidrv の GPD パーサーによって認識されます。

 

 




