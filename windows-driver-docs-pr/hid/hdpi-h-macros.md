---
title: Hdpi.h マクロ
description: Hdpi .h ヘッダーに含まれるマクロ。
ms.localizationpriority: medium
ms.date: 02/25/2020
ms.openlocfilehash: a781f092f31abf5be80d82c6a77557aeed0acb46
ms.sourcegitcommit: f1f641bd759b7bf6e45626ffcc090ffd28337c30
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/28/2020
ms.locfileid: "78166684"
---
# <a name="hdpih-macros"></a>Hdpi.h マクロ

[Hdpi .h](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/)ヘッダーファイルには、次のマクロが含まれています。

- [HidP\_GetButtons](#hidp_getbuttons)
- [HidP\_GetButtonsEx](#hidp_getbuttonsex)
- [HidP\_SetButtons](#hidp_setbuttons)
- [HidP\_UnsetButtons](#hidp_unsetbuttons)

## <a name="hidp_getbuttons"></a>HidP\_GetButtons

**Hidp\_GetButtons**マクロは、 [**Hidp\_getbuttons**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusages)ルーチンのニーモニックエイリアスです。

```cpp
#define HidP_GetButtons(Rty, UPa, LCo, ULi, ULe, Ppd, Rep, RLe) \
        HidP_GetUsages(Rty, UPa, LCo, ULi, ULe, Ppd, Rep, RLe)
```

## <a name="hidp_getbuttonsex"></a>HidP\_GetButtonsEx

**Hidp\_GetButtonsEx**マクロは、 [**Hidp\_get使用性別**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagesex)ルーチンのニーモニックエイリアスです。

```cpp
#define HidP_GetButtonsEx(Rty, LCo, BLi, ULe, Ppd, Rep, RLe)  \
         HidP_GetUsagesEx(Rty, LCo, BLi, ULe, Ppd, Rep, RLe)
```

## <a name="hidp_setbuttons"></a>HidP\_SetButtons

**Hidp\_SetButtons**マクロは、 [**Hidp\_setbuttons**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusages)ルーチンのニーモニックエイリアスです。

```cpp
#define HidP_SetButtons(Rty, Up, Lco, ULi, ULe, Ppd, Rep, Rle) \
        HidP_SetUsages(Rty, Up, Lco, ULi, ULe, Ppd, Rep, Rle)
```

## <a name="hidp_unsetbuttons"></a>HidP\_UnsetButtons

**Hidp\_UnsetButtons**マクロは、 [**Hidp\_unsetbuttons**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_unsetusages)ルーチンのニーモニックエイリアスです。

```cpp
#define HidP_UnsetButtons(Rty, Up, Lco, ULi, ULe, Ppd, Rep, Rle) \
        HidP_UnsetUsages(Rty, Up, Lco, ULi, ULe, Ppd, Rep, Rle)
```

### <a name="requirements"></a>要件

| | |
| --- | --- |
| ヘッダー | [hidpi. h](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/) (hidpi を含む) |

## <a name="see-also"></a>参照

[hidpi. h](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/)

[HidP\_GetUsages](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusages)

[HidP\_Getの性別](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagesex)

[HidP\_SetUsages](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusages)

[HidP\_UnsetUsages](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_unsetusages)
