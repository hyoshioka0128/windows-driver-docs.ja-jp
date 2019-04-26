---
title: Hello World' Definition File
description: Hello World' Definition File
ms.assetid: 50c38eea-7826-44bb-9048-ce8e07ce3478
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d0e5b40bbfd32d4f8f469ff249e3078c33bc967
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358428"
---
# <a name="hello-world-definition-file"></a>'Hello World' の定義ファイル

定義ファイルは、エントリ ポイント関数のエクスポートに使用されます。 *Hellowld.def*ファイルは、次の 2 つの COM エクスポートを含める必要があります**DllGetClassObject**と**DllCanUnloadNow**、Microsoft Windows SDK で説明されます。ドキュメントです。

```make
LIBRARY HELLOWLD

EXPORTS
     DllGetClassObject   PRIVATE
     DllCanUnloadNow     PRIVATE
```
