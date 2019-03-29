---
title: ローカライズされた文字列を [文字列] セクションの変更
description: この INF 要件により、作業をビルドする擬似ローカライズします。 文字列の範囲内で、ローカライズできない文字列とローカライズ可能なを記述することが要件
ms.assetid: F0A0C309-9FA3-4941-AF35-15CD63DB25E3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c078dcd265f3e728b502c7f3d5b9c307abdee65
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579946"
---
# <a name="string-section-changes-for-localized-strings"></a>\[文字列\]セクションのローカライズされた文字列の変更


この INF 要件により、作業をビルドする擬似ローカライズします。 要件を区切る文字列セクション内で、ローカライズできない文字列とローカライズ可能なです。

次の例にありません。 何がローカライズの先頭がありません。これを使用しない必要があります。

``` syntax
[Strings]

REG_MULTI_SZ   = 0x00010000
REG_DWORD      = 0x00010001

MSFT = "Microsoft"
IHV  = "Contoso, Ltd"
```

次の例は、代わりに使用する必要があります。新しい行に注意してください。

``` syntax
[Strings]

;Localizable
MSFT = "Microsoft"
IHV  = "Contoso, Ltd"


;Non-Localizable
REG_MULTI_SZ   = 0x00010000
REG_DWORD      = 0x00010001
```

 

 





