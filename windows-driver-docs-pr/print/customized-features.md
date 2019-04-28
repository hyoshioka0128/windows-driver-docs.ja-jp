---
title: カスタマイズされた機能
description: カスタマイズされた機能
ms.assetid: a7dfed02-3505-4ed6-86cf-efb273f76ad6
keywords:
- プリンターの WDK Unidrv、カスタマイズ機能します。
- カスタマイズされたプリンター機能 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9480f1b71049959ec1d6f5621292fdd7d2cfa76
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365549"
---
# <a name="customized-features"></a>カスタマイズされた機能





カスタマイズされた機能は、ハードウェアに固有のものです。 これらの機能の一意の名前を作成します。 、カスタマイズされた各機能のセットを指定する必要があります[オプションをカスタマイズ](customized-options.md)します。 たとえば、プリンター、経済性のモードの操作を提供します。 GPD 言語がこの機能を記述するための機能を提供しないために、カスタマイズされた機能とそのオプションを定義する必要があります。 機能の仕様を次に示します。

```cpp
*Feature: EconoMode
{
    *Name: "Economy Mode"
    *FeatureType: PRINTER_PROPERTY
    *DefaultOption: EconoModeOff
    *Option: EconoModeOff
    {
        *Name: "Off"
        *Command: CmdSelect
         {
             *Order: DOC_SETUP.5
             *Cmd: "@PJL SET ECONOMODE=OFF<0A>"
         }
    }
    *Option: EconoModeOn
    {
        *Name: "On"
        *Command: CmdSelect
        {
            *Order: DOC_SETUP.5
            *Cmd: "@PJL SET ECONOMODE=ON<0A>"
        }
    }
}
```

 

 




