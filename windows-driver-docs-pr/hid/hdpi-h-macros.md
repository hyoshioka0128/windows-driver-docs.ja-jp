---
title: Hdpi.h マクロ
description: Hdpi .h ヘッダーに含まれるマクロ。
ms.localizationpriority: medium
ms.date: 02/25/2020
ms.openlocfilehash: 1ebc9dfad8c16a77bddfd3d2043bf2ca06e81050
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968217"
---
# <a name="hdpih-macros"></a>Hdpi.h マクロ

[Hdpi .h](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/)ヘッダーファイルには、次のマクロが含まれています。

- [HidP \_ getbuttons](#hidp_getbuttons)
- [HidP \_ getbuttonsex](#hidp_getbuttonsex)
- [HidP \_ setbuttons](#hidp_setbuttons)
- [HidP \_ unsetbuttons](#hidp_unsetbuttons)

## <a name="hidp_getbuttons"></a>HidP \_ getbuttons

**Hidp \_ getbuttons**マクロは、 [**hidp \_ getbuttons**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusages)ルーチンのニーモニックエイリアスです。

```cpp
#define HidP_GetButtons(Rty, UPa, LCo, ULi, ULe, Ppd, Rep, RLe) \
        HidP_GetUsages(Rty, UPa, LCo, ULi, ULe, Ppd, Rep, RLe)
```

## <a name="hidp_getbuttonsex"></a>HidP \_ getbuttonsex

**Hidp \_ getbuttonsex**マクロは、 [**hidp \_ get使用性別**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagesex)ルーチンのニーモニックエイリアスです。

```cpp
#define HidP_GetButtonsEx(Rty, LCo, BLi, ULe, Ppd, Rep, RLe)  \
         HidP_GetUsagesEx(Rty, LCo, BLi, ULe, Ppd, Rep, RLe)
```

## <a name="hidp_setbuttons"></a>HidP \_ setbuttons

**Hidp \_ setbuttons**マクロは、 [**hidp \_ setbuttons**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusages)ルーチンのニーモニックエイリアスです。

```cpp
#define HidP_SetButtons(Rty, Up, Lco, ULi, ULe, Ppd, Rep, Rle) \
        HidP_SetUsages(Rty, Up, Lco, ULi, ULe, Ppd, Rep, Rle)
```

## <a name="hidp_unsetbuttons"></a>HidP \_ unsetbuttons

**Hidp \_ unsetbuttons**マクロは、 [**hidp \_ unsetbuttons**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_unsetusages)ルーチンのニーモニックエイリアスです。

```cpp
#define HidP_UnsetButtons(Rty, Up, Lco, ULi, ULe, Ppd, Rep, Rle) \
        HidP_UnsetUsages(Rty, Up, Lco, ULi, ULe, Ppd, Rep, Rle)
```

### <a name="requirements"></a>要件

**ヘッダー**: [hidpi. h](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/) (hidpi を含む)


## <a name="see-also"></a>関連項目

[hidpi. h](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/)

[HidP \_ getusages](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusages)

[HidP \_ getの性別](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagesex)

[HidP \_ setusages](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusages)

[HidP \_ unsetusages](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_unsetusages)
