---
title: ソース ディスクとファイルを識別します。
description: ソース ディスクとファイルを識別します。
ms.assetid: 0eb8fe7f-1e44-4f3d-8567-31a2cd659805
keywords:
- ソース ディスクまたはファイルを識別する INF ファイルの WDK 表示
- ソース ディスクの WDK の表示
- ソース ファイルの WDK の表示
- 表示のソース ディスクまたはファイルを識別します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 344cb2f80d2402a6bb881605ecfafc36b0463726
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529209"
---
# <a name="identifying-source-disks-and-files"></a>ソース ディスクとファイルを識別します。


すべてのボックスでディスプレイ ドライバーを指定する必要があります、 **SourceDisksNames**と**SourceDisksFiles**セクション。 次の例では、CD-ROM のディスクとディスクに格納されているソース ファイルの名前を識別する方法を示します。 ソース ファイルは、インストール中に、ターゲット コンピューターに転送されます。

```inf
[SourceDisksNames]
3426=windows cd

[SourceDisksFiles]
DisplayMiniportDriverName.sys  = 3426
UserModeDriverName1.dll  = 3426
UserModeDriverName2.dll  = 3426
```

詳細については、 **SourceDisksNames**と**SourceDisksFiles**のセクションを参照してください[ **INF SourceDisksNames セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547478)と[ **INF SourceDisksFiles セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547472)します。

 

 





