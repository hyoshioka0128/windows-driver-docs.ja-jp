---
title: DSM\_バージョンの WMI クラス
description: DSM\_バージョンの WMI クラス
ms.assetid: 79239921-169d-496d-a52b-f4b6b0cb0c80
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e4531e63b1cb50233987f6dc187acf7a988399ad
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384681"
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

このクラスの定義が WMI ツール スイートによってコンパイルされると、生成、 [ **DSM\_バージョン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mpiowmi/ns-mpiowmi-_dsm_version)データ構造体。 この WMI クラスに関連付けられているメソッドはありません。

 

 





