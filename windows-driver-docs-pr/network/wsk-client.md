---
title: WSK_CLIENT
description: このトピックでは、WSK アプリケーションの WSK_CLIENT データ型について説明します。
ms.assetid: 7958dbd6-eaa6-4be8-a3a0-b3433ced924b
keywords:
- WSK_CLIENT、WDK WSK_CLIENT ネットワークドライバー
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ec0e8ed2a558fe03437a27b67906aff42ffd79c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844357"
---
# <a name="wsk_client"></a>WSK_CLIENT

WSK_CLIENT データ型は、wsk アプリケーションへのアタッチの WSK サブシステムのバインドコンテキストを定義します。

```c++
typedef PVOID PWSK_CLIENT;
```

**PWSK_CLIENT**  
**WSK_CLIENT**構造体の内容は wsk アプリケーションに対して非透過的です。

## <a name="remarks"></a>注釈

WSK アプリケーションが[WskCaptureProviderNPI](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskcaptureprovidernpi)関数を呼び出すと、wsk サブシステムは、 *WskProviderNpi*パラメーターを使って WSK アプリケーションへの WSK_CLIENT 構造体へのポインターを返します。 WSK サブシステムは、この構造体を使用して、WSK アプリケーションと WSK サブシステムの間のバインディングの状態を追跡します。 WSK アプリケーションは、このポインターをパラメーターとして[WSK_PROVIDER_DISPATCH](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_dispatch)のすべての関数 ([wskcontrolclient](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_client)、 [Wsksocket](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket)、および[wskcontrolclient](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket_connect)) に渡します。

詳細については、「 [Winsock カーネルアプリケーションの登録](registering-a-winsock-kernel-application.md)」を参照してください。

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| バージョン | Windows Vista 以降のバージョンの Windows オペレーティングシステムで使用できます。 |
| Header | Wsk .h (Wsk .h を含む) |

## <a name="see-also"></a>関連項目

[WskCaptureProviderNPI](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskcaptureprovidernpi)  
[WskControlClient](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_client)  
[WskSocket](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket)  
[WskSocketConnect](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket_connect)  
[WSK_PROVIDER_DISPATCH](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_dispatch)

