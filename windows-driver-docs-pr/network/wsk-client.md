---
title: WSK_CLIENT
description: このトピックでは、WSK アプリケーション WSK_CLIENT データ型について説明します。
ms.assetid: 7958dbd6-eaa6-4be8-a3a0-b3433ced924b
keywords:
- WSK_CLIENT、WDK WSK_CLIENT ネットワーク ドライバー
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66f179ebd5bb092ff30a0d83b0588607fca157dc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538025"
---
# <a name="wskclient"></a>WSK_CLIENT

WSK_CLIENT のデータ型は、WSK アプリケーションにその添付ファイルの WSK サブシステムのバインド コンテキストを定義します。

```c++
typedef PVOID PWSK_CLIENT;
```

**PWSK_CLIENT**  
内容、 **WSK_CLIENT**構造は WSK アプリケーションに対して非透過的です。

## <a name="remarks"></a>注釈

WSK アプリケーションを呼び出すと、 [WskCaptureProviderNPI](https://msdn.microsoft.com/library/windows/hardware/ff571122)関数で WSK サブシステムで、WSK_CLIENT 構造体の WSK アプリケーションへのポインターが返されます、 *WskProviderNpi*パラメーター。 WSK サブシステムは、WSK アプリケーションと WSK サブシステム間のバインドの状態を追跡するために、この構造体を使用します。 WSK アプリケーションは、内のすべての関数をパラメーターとしてこのポインターを渡して[WSK_PROVIDER_DISPATCH](https://msdn.microsoft.com/library/windows/hardware/ff571175) ([WskControlClient](https://msdn.microsoft.com/library/windows/hardware/ff571126)、 [WskSocket](https://msdn.microsoft.com/library/windows/hardware/ff571149)、および[WskSocketConnect](https://msdn.microsoft.com/library/windows/hardware/ff571150))。

詳細については、次を参照してください。 [Winsock カーネル アプリケーションを登録する](registering-a-winsock-kernel-application.md)します。

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| バージョン | Windows Vista および Windows オペレーティング システムの以降のバージョンで使用できます。 |
| Header | Wsk.h (Wsk.h を含む) |

## <a name="see-also"></a>関連項目

[WskCaptureProviderNPI](https://msdn.microsoft.com/library/windows/hardware/ff571122)  
[WskControlClient](https://msdn.microsoft.com/library/windows/hardware/ff571126)  
[WskSocket](https://msdn.microsoft.com/library/windows/hardware/ff571149)  
[WskSocketConnect](https://msdn.microsoft.com/library/windows/hardware/ff571150)  
[WSK_PROVIDER_DISPATCH](https://msdn.microsoft.com/library/windows/hardware/ff571175)

