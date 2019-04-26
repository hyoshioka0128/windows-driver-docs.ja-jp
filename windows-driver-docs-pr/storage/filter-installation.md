---
title: フィルターのインストール
description: フィルターのインストール
ms.assetid: 118d9fd9-c499-4371-9084-a4368a78f5e0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40fedbe775c3c9534646ecc45c71d85f2ef19cf7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355880"
---
# <a name="filter-installation"></a>フィルターのインストール


クラッシュ ダンプのフィルター ドライバーは、次のコード例に示すように、レジストリ キー、サービス名を追加することで、クラッシュ ダンプのスタックでインストールできます。 クラッシュ ダンプまたは休止状態が初期化されると、ダンプのドライバーが読み込まれます。 この時点では、レジストリ キーに記載されているフィルター ドライバーが読み込まれます。

```cpp
HKLM\SYSTEM\CurrentControlSet\Control\CrashControl

DumpFilters REG_MULTI_SZ DriverName

e.g. dumpfltr.sys
```

 

 




