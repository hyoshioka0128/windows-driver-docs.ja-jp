---
title: DSM\_バージョン WMI クラス
description: DSM\_バージョン WMI クラス
ms.assetid: 79239921-169d-496d-a52b-f4b6b0cb0c80
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 974bfede7fe9b9476c7b94dc0fed6dc3e99e69fe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844561"
---
# <a name="dsm_version-wmi-class"></a>DSM\_バージョン WMI クラス


MPIO ドライバーは、DSM\_バージョンの WMI クラスを使用して、構成された DSM のバージョンを識別します。

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

このクラス定義が WMI ツールスイートによってコンパイルされると、 [**DSM\_バージョン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiowmi/ns-mpiowmi-_dsm_version)のデータ構造が生成されます。 この WMI クラスに関連付けられているメソッドはありません。

 

 





