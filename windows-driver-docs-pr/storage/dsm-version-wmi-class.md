---
title: DSM\_バージョンの WMI クラス
description: DSM\_バージョンの WMI クラス
ms.assetid: 79239921-169d-496d-a52b-f4b6b0cb0c80
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 51db53f70e3bd6d6e60a68c32b7c81ce0cc23ff1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579796"
---
# <a name="dsmversion-wmi-class"></a>DSM\_バージョンの WMI クラス


MPIO ドライバーは DSM を使用して\_構成 DSM のバージョンを識別するためにバージョンの WMI クラスです。

```cpp
class DSM_VERSION
{
    //
    // Version: Major, Minor, Product, Qfe
    //
    [WmiDataId(1)] uint32 MajorVersion;
    [WmiDataId(2)] uint32 MinorVersion;
    [WmiDataId(3)] uint32 ProductBuild;
    [WmiDataId(4)] uint32 QfeNumber;

};
```

このクラスの定義が WMI ツール スイートによってコンパイルされると、生成、 [ **DSM\_バージョン**](https://msdn.microsoft.com/library/windows/hardware/ff552750)データ構造体。 この WMI クラスに関連付けられているメソッドはありません。

 

 




