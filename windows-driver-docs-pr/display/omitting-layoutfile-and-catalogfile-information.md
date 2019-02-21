---
title: LayoutFile と CatalogFile 情報を省略します。
description: LayoutFile と CatalogFile 情報を省略します。
ms.assetid: e34302b9-0fb4-462b-9fa6-5ae51e83cd8b
keywords:
- INF ファイル WDK の表示、LayoutFile ディレクティブ
- INF ファイル WDK の表示、CatalogFile ディレクティブ
- CatalogFile ディレクティブ WDK の表示
- LayoutFile ディレクティブ WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e91cfb940c45135048c58fb346701b223b3051de
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530714"
---
# <a name="omitting-layoutfile-and-catalogfile-information"></a>LayoutFile と CatalogFile 情報を省略します。


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

 

 





