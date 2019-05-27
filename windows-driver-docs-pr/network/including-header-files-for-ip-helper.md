---
title: IP ヘルパーのヘッダー ファイルを含める
description: IP ヘルパーのヘッダー ファイルを含める
ms.assetid: f4642717-223c-425a-8389-cbbc75567ae3
keywords:
- IP ヘルパー WDK ネットワー キング、ヘッダー ファイルを含む
- ヘッダー ファイルの WDK IP ヘルパー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96e9427cf63f510262c5704092267661f34edc0a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327778"
---
# <a name="including-header-files-for-ip-helper"></a>IP ヘルパーのヘッダー ファイルを含める


ドライバー コード IP ヘルパー関数のカーネル モード、MIB 構造体、および Netioapi.h で宣言されている列挙型を使用する必要があります **\#含める**次の一連のステートメント。

```C++
#include <ntddk.h>
#include <netioapi.h>
```

**注**  ドライバー コードに Iphlpapi.h を含めないでください。 ユーザー モード アプリケーションに対してのみ使用されます。

 

Netioapi.h はカーネル モード ドライバーで使用する場合は、既に Winsock Kernel、ネットワーク インターフェイスの情報、ネットワーク層、および Network Driver Interface Specification (NDIS) 型を定義するヘッダー ファイルをネットワーク含まれます。

そのため、次のヘッダー ファイルは、ドライバーのコードでは含めないようにしています。

- Ifdef.h
- Nldef.h
- Ws2def.h
- Ws2ipdef.h

IP ヘルパー関数と構造体の MIB のユーザー モードのバージョンについては、Windows SDK のドキュメントを参照してください。

 

 





