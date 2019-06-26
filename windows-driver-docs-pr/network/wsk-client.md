---
title: WSK_CLIENT
description: このトピックでは、WSK アプリケーション WSK_CLIENT データ型について説明します。
ms.assetid: 7958dbd6-eaa6-4be8-a3a0-b3433ced924b
keywords:
- WSK_CLIENT、WDK WSK_CLIENT ネットワーク ドライバー
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 808516d580816214b854fa43878d07d195ec750a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379372"
---
# <a name="wskclient"></a>WSK_CLIENT

WSK_CLIENT のデータ型は、WSK アプリケーションにその添付ファイルの WSK サブシステムのバインド コンテキストを定義します。

```c++
typedef PVOID PWSK_CLIENT;
```

**PWSK_CLIENT**  
内容、 **WSK_CLIENT**構造は WSK アプリケーションに対して非透過的です。

## <a name="remarks"></a>注釈

WSK アプリケーションを呼び出すと、 [WskCaptureProviderNPI](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nf-wsk-wskcaptureprovidernpi)関数で WSK サブシステムで、WSK_CLIENT 構造体の WSK アプリケーションへのポインターが返されます、 *WskProviderNpi*パラメーター。 WSK サブシステムは、WSK アプリケーションと WSK サブシステム間のバインドの状態を追跡するために、この構造体を使用します。 WSK アプリケーションは、内のすべての関数をパラメーターとしてこのポインターを渡して[WSK_PROVIDER_DISPATCH](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/ns-wsk-_wsk_provider_dispatch) ([WskControlClient](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_client)、 [WskSocket](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_socket)、および[WskSocketConnect](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_socket_connect))。

詳細については、次を参照してください。 [Winsock カーネル アプリケーションを登録する](registering-a-winsock-kernel-application.md)します。

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| バージョン | Windows Vista および Windows オペレーティング システムの以降のバージョンで使用できます。 |
| Header | Wsk.h (Wsk.h を含む) |

## <a name="see-also"></a>関連項目

[WskCaptureProviderNPI](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nf-wsk-wskcaptureprovidernpi)  
[WskControlClient](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_client)  
[WskSocket](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_socket)  
[WskSocketConnect](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_socket_connect)  
[WSK_PROVIDER_DISPATCH](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/ns-wsk-_wsk_provider_dispatch)

