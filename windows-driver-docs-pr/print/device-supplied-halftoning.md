---
title: デバイスで指定されるハーフトーン
description: デバイスで指定されるハーフトーン
ms.assetid: d1d7963e-c23e-4cb5-a33f-43fec5dc74d2
keywords:
- デバイスから提供されるハーフトーン WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a539326bb9879a6c56baba893e5f4daa16e14ef0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387271"
---
# <a name="device-supplied-halftoning"></a>デバイスで指定されるハーフトーン





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

 

 




