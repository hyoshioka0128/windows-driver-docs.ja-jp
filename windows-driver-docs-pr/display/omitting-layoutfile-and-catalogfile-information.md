---
title: LayoutFile および CatalogFile の情報の省略
description: LayoutFile および CatalogFile の情報の省略
ms.assetid: e34302b9-0fb4-462b-9fa6-5ae51e83cd8b
keywords:
- INF ファイル WDK の表示、LayoutFile ディレクティブ
- INF ファイル WDK の表示、CatalogFile ディレクティブ
- CatalogFile ディレクティブ WDK の表示
- LayoutFile ディレクティブ WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d635074fd5bcae4a3aba87b6e8db0801f7620225
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372770"
---
# <a name="omitting-layoutfile-and-catalogfile-information"></a>LayoutFile および CatalogFile の情報の省略


すべての情報を指定する必要があります、 **LayoutFile**と**CatalogFile**ディレクティブ、**バージョン**セクション。 次の例は、一般的な**バージョン**セクション。

```inf
[Version]
Signature="$Windows NT$"
Provider=%MSFT%
ClassGUID={4D36E968-E325-11CE-BFC1-08002BE10318}
Class=Display
DriverVer=11/22/2004, 6.14.10.7000
```

詳細については、**バージョン**セクションと関連付けられているディレクティブ**バージョン**を参照してください[ **INF バージョン セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)します。

 

 





