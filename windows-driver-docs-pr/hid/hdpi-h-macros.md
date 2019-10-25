---
title: Hdpi.h マクロ
description: Hdpi .h ヘッダーに含まれるマクロ。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3181026688e74ab47a1fb479712b84fde16c99d3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824814"
---
# <a name="hdpih-macros"></a>Hdpi.h マクロ

Hdpi .h ヘッダーファイルには、いくつかのマクロが含まれています。 このトピックでは、次のマクロについて説明します。

* [**HidP\_GetButtons**](#hidp_getbuttons)
* [**HidP\_GetButtonsEx**](#hidp_getbuttonsex)
* [**HidP\_SetButtons**](#hidp_setbuttons)
* [**HidP\_UnsetButtons**](#hidp_unsetbuttons)


##  <a name="hidp_getbuttons"></a>HidP\_GetButtons


**Hidp\_GetButtons**マクロは、 [**Hidp\_getbuttons**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusages)ルーチンのニーモニックエイリアスです。

```cpp
#define HidP_GetButtons(Rty, UPa, LCo, ULi, ULe, Ppd, Rep, RLe) \
        HidP_GetUsages(Rty, UPa, LCo, ULi, ULe, Ppd, Rep, RLe)
```

##  <a name="hidp_getbuttonsex"></a>HidP\_GetButtonsEx


**Hidp\_GetButtonsEx**マクロは、 [**Hidp\_get使用性別**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagesex)ルーチンのニーモニックエイリアスです。

```cpp
#define HidP_GetButtonsEx(Rty, LCo, BLi, ULe, Ppd, Rep, RLe)  \
         HidP_GetUsagesEx(Rty, LCo, BLi, ULe, Ppd, Rep, RLe)
```


##  <a name="hidp_setbuttons"></a>HidP\_SetButtons


**Hidp\_SetButtons**マクロは、 [**Hidp\_setbuttons**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusages)ルーチンのニーモニックエイリアスです。

```cpp
#define HidP_SetButtons(Rty, Up, Lco, ULi, ULe, Ppd, Rep, Rle) \
        HidP_SetUsages(Rty, Up, Lco, ULi, ULe, Ppd, Rep, Rle)
```

##  <a name="hidp_unsetbuttons"></a>HidP\_UnsetButtons


**Hidp\_UnsetButtons**マクロは、 [**Hidp\_unsetbuttons**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_unsetusages)ルーチンのニーモニックエイリアスです。

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
<td>Hidpi. h (Hidpi を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目

[**HidP\_GetUsages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusages)

[**HidP\_Getの性別**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagesex)

[**HidP\_SetUsages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusages)

[**HidP\_UnsetUsages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_unsetusages)






