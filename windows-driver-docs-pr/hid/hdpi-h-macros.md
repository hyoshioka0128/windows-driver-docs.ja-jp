---
title: Hdpi.h マクロ
description: マクロは Hdpi.h ヘッダーに含まれます。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5559dff7a571e2e5b857a3a6f7f29e1ee06c4aef
ms.sourcegitcommit: 0504cc497918ebb7b41a205f352046a66c0e26a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2019
ms.locfileid: "65405100"
---
# <a name="hdpih-macros"></a>Hdpi.h マクロ

Hdpi.h ヘッダー ファイルには、いくつかのマクロが含まれています。 このトピックでは、次のマクロをドキュメントします。

* [**HidP\_GetButtons**](#hidp_getbuttons)
* [**HidP\_GetButtonsEx**](#hidp_getbuttonsex)
* [**HidP\_SetButtons**](#hidp_setbuttons)
* [**HidP\_UnsetButtons**](#hidp_unsetbuttons)


##  <a name="hidpgetbuttons"></a>HidP\_GetButtons


**HidP\_GetButtons**マクロのニーモニック エイリアスとは、 [ **HidP\_GetUsages** ](https://msdn.microsoft.com/library/windows/hardware/ff539742)ルーチン。

```cpp
#define HidP_GetButtons(Rty, UPa, LCo, ULi, ULe, Ppd, Rep, RLe) \
        HidP_GetUsages(Rty, UPa, LCo, ULi, ULe, Ppd, Rep, RLe)
```

##  <a name="hidpgetbuttonsex"></a>HidP\_GetButtonsEx


**HidP\_GetButtonsEx**マクロは、ニーモニックのエイリアス、 [ **HidP\_GetUsagesEx** ](https://msdn.microsoft.com/library/windows/hardware/ff539745)ルーチン。

```cpp
#define HidP_GetButtonsEx(Rty, LCo, BLi, ULe, Ppd, Rep, RLe)  \
         HidP_GetUsagesEx(Rty, LCo, BLi, ULe, Ppd, Rep, RLe)
```


##  <a name="hidpsetbuttons"></a>HidP\_SetButtons


**HidP\_SetButtons**マクロのニーモニック エイリアスとは、 [ **HidP\_SetUsages** ](https://msdn.microsoft.com/library/windows/hardware/ff539792)ルーチン。

```cpp
#define HidP_SetButtons(Rty, Up, Lco, ULi, ULe, Ppd, Rep, Rle) \
        HidP_SetUsages(Rty, Up, Lco, ULi, ULe, Ppd, Rep, Rle)
```

##  <a name="hidpunsetbuttons"></a>HidP\_UnsetButtons


**HidP\_UnsetButtons**マクロのニーモニック エイリアスとは、 [ **HidP\_UnsetUsages** ](https://msdn.microsoft.com/library/windows/hardware/ff539819)ルーチン。

```cpp
#define HidP_UnsetButtons(Rty, Up, Lco, ULi, ULe, Ppd, Rep, Rle) \
        HidP_UnsetUsages(Rty, Up, Lco, ULi, ULe, Ppd, Rep, Rle)
```

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Hidpi.h (include Hidpi.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目

[**HidP\_GetUsages**](https://msdn.microsoft.com/library/windows/hardware/ff539742)

[**HidP\_GetUsagesEx**](https://msdn.microsoft.com/library/windows/hardware/ff539745)

[**HidP\_SetUsages**](https://msdn.microsoft.com/library/windows/hardware/ff539792)

[**HidP\_UnsetUsages**](https://msdn.microsoft.com/library/windows/hardware/ff539819)






