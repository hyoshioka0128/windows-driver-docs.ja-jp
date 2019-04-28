---
title: エラー コードをフィルター処理するマクロ例
description: エラー コードをフィルター処理するマクロ例
ms.assetid: 68aa0a75-82c7-4dd9-8f8f-eca5de6ea102
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f2f6ccd212cfcefbfb4c36956a4b51ac8a9a167
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373915"
---
# <a name="macro-example-to-filter-error-codes"></a>エラー コードをフィルター処理するマクロ例

> [!IMPORTANT]  
> WSD 見据えて機能は非推奨とされているし、WSD の挑戦者に関連するすべてのドキュメントは、2018 年に削除されます。

次のマクロの例では、通信障害エラー コードがフィルター処理します。

```cpp
//
// Example of a macro to filter device communication errors
//
#define WSD_COMMUNICATION_ERROR(hr) \
    ((HRESULT_FROM_WIN32(ERROR_WINHTTP_CANNOT_CONNECT)) == hr) || \
    ((HRESULT_FROM_WIN32(ERROR_WINHTTP_CONNECTION_ERROR)) == hr) || \
    ((HRESULT_FROM_WIN32(ERROR_WINHTTP_TIMEOUT)) == hr) || \
    ((HRESULT_FROM_WIN32(ERROR_TIMEOUT)) == hr) || \
    ((HRESULT_FROM_WIN32(ERROR_WINHTTP_NAME_NOT_RESOLVED)) == hr))
```

 




