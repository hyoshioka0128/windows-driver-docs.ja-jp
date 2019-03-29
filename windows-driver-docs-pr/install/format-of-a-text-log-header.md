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
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571631"
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

 

 





