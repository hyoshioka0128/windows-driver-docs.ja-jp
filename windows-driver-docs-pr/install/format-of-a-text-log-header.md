---
title: テキスト ログ ヘッダーの書式
description: テキスト ログ ヘッダーの書式
ms.assetid: d4a50905-215f-4156-b5cf-f160c757bb90
keywords:
- ヘッダーの WDK SetupAPI ログ記録
- WDK SetupAPI ログ出力を書式設定します。
- テキスト ログの WDK SetupAPI、ヘッダー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d25176111815715564f42650e9d74eb0cb485468
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377079"
---
# <a name="format-of-a-text-log-header"></a>テキスト ログ ヘッダーの書式


A*テキスト ログ ヘッダー* SetupAPI テキスト ログの最初のほとんどログ エントリから構成されません。 テキスト ログのヘッダーには、オペレーティング システムとシステム アーキテクチャに関する情報が含まれています。 テキスト ログのヘッダーの例を次に示します。

```cpp
[Device Install Log]
     OS Version = 6.0.5033
     Service Pack = 0.0
     Suite = 0x0100
     ProductType = 1
     Architecture = x86

[BeginLog]
```

テキスト ログのヘッダーの情報への呼び出しによって返される情報のサブセットは、 [GetVersionEx](https://go.microsoft.com/fwlink/p/?linkid=179601)で、 [OVSERVERSIONINFOEX](https://go.microsoft.com/fwlink/p/?linkid=179602)構造体。 詳細については、Microsoft Windows SDK を参照してください。

 

 





