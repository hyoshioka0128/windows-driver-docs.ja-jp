---
title: デバイスから提供されるハーフトーン
description: デバイスから提供されるハーフトーン
ms.assetid: d1d7963e-c23e-4cb5-a33f-43fec5dc74d2
keywords:
- デバイスから提供されるハーフトーン WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a539326bb9879a6c56baba893e5f4daa16e14ef0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560077"
---
# <a name="device-supplied-halftoning"></a>デバイスから提供されるハーフトーン





プリンターでは、内部的にハーフトーン機能を提供する場合、ミニドライバーは Unidrv がこれらの機能をアクティブ化するプリンターに送信するコマンドを指定する必要があります。 各ハーフトーン オプションはプリンターでサポートされている GPD ファイルのハーフトーン\*機能エントリを含める必要があります\*各ハーフトーンのデバイスから提供されるオプションのエントリを次のようにコマンドします。

```cpp
*Feature: Halftone
{
    *Option: CustomHalftoneMethod1
    {
        *Name: "Custom Halftone Method 1"
        *Command: CmdSelect: "<printer command string>"
    }
    *Option: CustomHalftoneMethod2
    {
        *Name: "Custom Halftone Method 2"
        *Command: CmdSelect: "<printer command string>"
    }
}
```

返さ機能のエントリも指定する必要があり、含める必要があります\*DevBPP と\*DevNumOfPlanes エントリをプリンターで想定されている入力形式を記述します。

 

 




