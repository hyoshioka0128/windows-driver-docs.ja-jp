---
title: ComputerHardwareIds の出力
description: ComputerHardwareIds の出力
ms.assetid: 38a08dda-92db-4389-9c2c-91fe17a88051
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3cadc25f122b2e3da31b3a1b30ce5c4553305011
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343105"
---
# <a name="computerhardwareids-output"></a>ComputerHardwareIds の出力


ComputerHardwareIds ツールによって生成される出力の例を次に示します。

```
Using the BIOS to gather information

## Computer Information

BIOS Vendor: Contoso Inc.
BIOS Version string: A16
System BIOS Major Version: 6
System BIOS Minor Version: 0

System Manufacturer: Contoso Inc.
System Family: (null)
System ProductName: Contoso SYS01

Enclosure Type: Portable


Hardware IDs
------------
{346511cf-ccee-5c6d-8ee9-3c70fc7aae83}    <- Manufacturer + Family + ProductName + BIOS Vendor + BIOS Version + Major Version + Minor Version
{d7be59e5-29b5-589a-b49d-de7265ef6a7b}    <- Manufacturer + Family + ProductName
```

この例では、仕入先 (Contoso inc.) は通常使用して、2 つ目のハードウェア ID (d7be59e5-29b5-589a-b49d-de7265ef6a7b) の値を[ **HardwareID** ](https://msdn.microsoft.com/library/windows/hardware/ff546114)内の要素、 [PackageInfo の XML ドキュメント](https://msdn.microsoft.com/library/windows/hardware/ff549602)仕入先のデバイス メタデータ パッケージの。

 

 





