---
title: ソース ディスクおよびファイルの識別
description: ソース ディスクおよびファイルの識別
ms.assetid: 0eb8fe7f-1e44-4f3d-8567-31a2cd659805
keywords:
- ソース ディスクまたはファイルを識別する INF ファイルの WDK 表示
- ソース ディスクの WDK の表示
- ソース ファイルの WDK の表示
- 表示のソース ディスクまたはファイルを識別します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6815050947045be29ca067fc90f20949bd047e7f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380178"
---
# <a name="identifying-source-disks-and-files"></a>ソース ディスクおよびファイルの識別


すべてのボックスでディスプレイ ドライバーを指定する必要があります、 **SourceDisksNames**と**SourceDisksFiles**セクション。 次の例では、CD-ROM のディスクとディスクに格納されているソース ファイルの名前を識別する方法を示します。 ソース ファイルは、インストール中に、ターゲット コンピューターに転送されます。

```inf
[SourceDisksNames]
3426=windows cd

[SourceDisksFiles]
DisplayMiniportDriverName.sys  = 3426
UserModeDriverName1.dll  = 3426
UserModeDriverName2.dll  = 3426
```

詳細については、 **SourceDisksNames**と**SourceDisksFiles**のセクションを参照してください[ **INF SourceDisksNames セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksnames-section)と[ **INF SourceDisksFiles セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksfiles-section)します。

 

 





