---
title: ユーザーの値
description: ユーザーの値
ms.assetid: 42b57fc2-fda0-464a-83dc-3e63ef693e9f
keywords:
- ユーザーのレジストリ設定 WDK ジョイスティック
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6638a4e2950b19977b335563180713a70aa0e92b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577934"
---
# <a name="user-values"></a>ユーザーの値





REGSTR という名前の 1 つの値\_VAL\_JOYUSERVALUES が以下に示す構造を格納します。 この構造体の指定方法のデータが VJoyD によって操作されるアプリケーションは、データがスケールされることを要求したときに中央揃え、またはに定義されているデッド ゾーンを指定します。

```cpp
struct {
    /* value at which to time-out internal joystick polling */
    DWORD   dwTimeOut;
 
    /* range of values app wants returned for axes */
    struct { 
        /* minimums for each axis */
        struct {
            DWORD    dwX;
            DWORD    dwY;
            DWORD    dwZ;
            DWORD    dwR;
            DWORD    dwU;
            DWORD    dwV;
        } jpMin;
        /* maximums for each axis */
        struct {
            DWORD    dwX;
            DWORD    dwY;
            DWORD    dwZ;
            DWORD    dwR;
            DWORD    dwU;
            DWORD    dwV;
        } jpMax;
        /* center positions for each axis */
        struct {
            DWORD    dwX;
            DWORD    dwY;
            DWORD    dwZ;
            DWORD    dwR;
            DWORD    dwU;
            DWORD    dwV;
        } jpCenter;
    } jrvRanges;
 
    /* area around center to be considered as "dead". specified as */
    /* a percentage (0-100). Only X & Y handled by system driver */
    struct {
        DWORD    dwX;
        DWORD    dwY;
        DWORD    dwZ;
        DWORD    dwR;
        DWORD    dwU;
        DWORD    dwV;
    } jpDeadZone;
}
```

 

 




