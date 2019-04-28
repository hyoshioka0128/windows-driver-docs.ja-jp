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
ms.openlocfilehash: e91cfb940c45135048c58fb346701b223b3051de
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379865"
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

詳細については、**バージョン**セクションと関連付けられているディレクティブ**バージョン**を参照してください[ **INF バージョン セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547502)します。

 

 





