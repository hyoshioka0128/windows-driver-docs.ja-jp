---
title: 1 対 1 の ID のマッピング
description: 1 対 1 の ID のマッピング
ms.assetid: fd9a98a4-5796-4d39-a83b-427b320b32da
keywords:
- マッピングのネットワーク コンポーネント Id
- ID マッピングの WDK netmap.inf ファイル
- マッピング ID の一対一の WDK ネットワー キング
- アップグレード前の Id の WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57c0b24ca1112cbd06866e56caa01c96d015f02c
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716822"
---
# <a name="one-to-one-id-mapping"></a>1 対 1 の ID のマッピング





**注**  Microsoft Windows XP では、ベンダーから提供されたネットワークのアップグレードはサポートされていない (SP1 以降)、Microsoft Windows Server 2003、および以降のオペレーティング システム。

 

内のエントリを**Oem<em>Xxx</em>**  ID の一対一のマッピングを指定する netmap.inf ファイルのファイルのセクションは、次の形式。

*preupgrade ID* = *postupgrade ID*

例:

```cpp
netservice=netservice_2000
```

ネットワーク プロトコル、サービス、およびクライアントの一対一の ID マッピングを使用する必要があります。 ID マッピングの一対一または一対多の ID のマッピングは、ネットワーク アダプターを使用できます。

 

 





