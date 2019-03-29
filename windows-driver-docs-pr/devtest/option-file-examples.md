---
title: オプション ファイルの例
description: オプション ファイルの例
ms.assetid: 632c37a8-a1cc-419a-917f-94e9308c4993
keywords:
- ファイル WDK Static Driver Verifier のオプション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c17133f8c4d4e6b88fb858314e915faf970e79f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580345"
---
# <a name="option-file-examples"></a>オプション ファイルの例


**例 1:タイムアウト値を変更します。**

次の例の Sdv default.xml ファイル、タイムアウトは 2 時間 (つまり、7,200 秒) に増加します。

```XML
<?xml version="1.0" encoding="utf-8"?>
<SlamConfig xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 <SDV_SlamConfig_Timeout xmlns="http://www.microsoft.com/SDV">7200</SDV_SlamConfig_Timeout>
  <SDV_SlamConfig_Spaceout xmlns="http://www.microsoft.com/SDV">2500</SDV_SlamConfig_Spaceout>
  <SDV_SlamConfig_NumberOfThreads xmlns="http://www.microsoft.com/SDV">0</SDV_SlamConfig_NumberOfThreads></SlamConfig>
```

**例 2:Spaceout 値を変更します。**

次の例の Sdv default.xml ファイル SDV の使用可能な仮想メモリは 3500 MB (3.5 GB) に増加します。

```XML
<?xml version="1.0" encoding="utf-8"?>
<SlamConfig xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <SDV_SlamConfig_Timeout xmlns="http://www.microsoft.com/SDV">3000</SDV_SlamConfig_Timeout>
  <SDV_SlamConfig_Spaceout xmlns="http://www.microsoft.com/SDV">3500</SDV_SlamConfig_Spaceout>
  <SDV_SlamConfig_NumberOfThreads xmlns="http://www.microsoft.com/SDV">0</SDV_SlamConfig_NumberOfThreads>
</SlamConfig>
```

**例 3:NumberOfThreads 値を変更します。**

次の例の Sdv default.xml ファイルでは、SDV を利用できるスレッドの数は 2 に制限されます。

```XML
<?xml version="1.0" encoding="utf-8" ?> 
- <SlamConfig xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <SDV_SlamConfig_Timeout xmlns="http://www.microsoft.com/SDV">3000</SDV_SlamConfig_Timeout> 
  <SDV_SlamConfig_Spaceout xmlns="http://www.microsoft.com/SDV">2500</SDV_SlamConfig_Spaceout> 
  <SDV_SlamConfig_NumberOfThreads xmlns="http://www.microsoft.com/SDV">2</SDV_SlamConfig_NumberOfThreads> 
  </SlamConfig>
```

 

 





