---
title: MOF ファイルを含める
description: MOF ファイルを含める
ms.assetid: 87ef7156-d204-4797-b805-a50d9a4c509d
keywords:
- カスタムの Guid の WDK ネットワーク
- WMI の WDK にネットワーク接続、Guid
- Oid WDK ネットワー キング、WMI
- Guid の WDK ネットワーク
- Windows Management Instrumentation の WDK ネットワー キング、Guid
- MOF ファイルの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc8aee4f71cba538becde5971a8e0448d1e71bb6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571491"
---
# <a name="including-a-mof-file"></a>MOF ファイルを含める





管理オブジェクト フォーマット (MOF) ファイルにコンパイルされ、ミニポート ドライバーのリソースに含める必要があります、ミニポート ドライバーのカスタム Oid にマップするカスタム Guid のすべての説明を含める必要があります (\*.rc) ファイル。

MOF のソース ファイルでは、型 MOFDATA の必要があり、.mof の拡張機能があります。 バイナリ ファイルに貼り付けた MOF のソース ファイルをコンパイルする必要があります[Mofcomp.exe](https://msdn.microsoft.com/library/windows/hardware/ff542012)でこのファイルを確認する必要がありますと[Wmimofck.exe](https://msdn.microsoft.com/library/windows/hardware/ff565588)します。

ミニポート ドライバーのリソース ファイルで、次の行を挿入する必要があります (\*.rc) MOF バイナリを含める。

```Text
NdisMofResource MOFDATA filename.bmf
```

*ファイル名*MOF のソース ファイルのファイル名を表します。

 

 





