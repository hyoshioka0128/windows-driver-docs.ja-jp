---
title: Hello World' Definition File
description: Hello World' Definition File
ms.assetid: 50c38eea-7826-44bb-9048-ce8e07ce3478
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d0e5b40bbfd32d4f8f469ff249e3078c33bc967
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530783"
---
# <a name="hello-world-definition-file"></a>'Hello World' の定義ファイル

定義ファイルは、エントリ ポイント関数のエクスポートに使用されます。 *Hellowld.def*ファイルは、次の 2 つの COM エクスポートを含める必要があります**DllGetClassObject**と**DllCanUnloadNow**、Microsoft Windows SDK で説明されます。ドキュメントです。

```make
LIBRARY HELLOWLD

EXPORTS
     DllGetClassObject   PRIVATE
     DllCanUnloadNow     PRIVATE
```
