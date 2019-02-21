---
title: フィルターのインストール
description: フィルターのインストール
ms.assetid: 118d9fd9-c499-4371-9084-a4368a78f5e0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40fedbe775c3c9534646ecc45c71d85f2ef19cf7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529670"
---
# <a name="filter-installation"></a>フィルターのインストール


クラッシュ ダンプのフィルター ドライバーは、次のコード例に示すように、レジストリ キー、サービス名を追加することで、クラッシュ ダンプのスタックでインストールできます。 クラッシュ ダンプまたは休止状態が初期化されると、ダンプのドライバーが読み込まれます。 この時点では、レジストリ キーに記載されているフィルター ドライバーが読み込まれます。

```cpp
HKLM\SYSTEM\CurrentControlSet\Control\CrashControl

DumpFilters REG_MULTI_SZ DriverName

e.g. dumpfltr.sys
```

 

 




