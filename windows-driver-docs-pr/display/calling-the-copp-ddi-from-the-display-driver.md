---
title: ディスプレイ ドライバーからの COPP DDI の呼び出し
description: ディスプレイ ドライバーからの COPP DDI の呼び出し
ms.assetid: d91d8a62-f212-4ae7-be61-b973d6495880
keywords:
- COPP DDI WDK DirectX VA を呼び出す
- COPP WDK DirectX va なので、ディスプレイ ドライバーからの呼び出し
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81b3a94fef0d0b783318be91958e3ac854e9f248
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384609"
---
# <a name="calling-the-copp-ddi-from-the-display-driver"></a>ディスプレイ ドライバーからの COPP DDI の呼び出し


## <span id="ddk_calling_the_copp_ddi_from_the_display_driver_gg"></span><span id="DDK_CALLING_THE_COPP_DDI_FROM_THE_DISPLAY_DRIVER_GG"></span>


このセクションには、Windows Server 2003 SP1 にのみ以降が適用されますおよび Windows XP SP2 以降。

ディスプレイ ドライバー、ビデオのミニポート ドライバーへの呼び出しを開始する[COPP DDI](sample-functions-for-copp.md) COPP I/O を使用して制御 (IOCTL) を要求します。 ディスプレイ ドライバーの呼び出し、 [ **EngDeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeviceiocontrol) COPP IOCTL を使用して、ビデオのミニポート ドライバーを同期 COPP 要求を送信する関数。 グラフィックス デバイス インターフェイス (GDI) では、入力と出力の両方に 1 つのバッファーを使用して、I/O サブシステムに要求を渡します。 I/O サブシステムは、ビデオのポートは、ビデオのミニポート ドライバーを使用して、要求を処理する要求をルーティングします。

次のサンプル データの構造と Ioctl は、ディスプレイ ドライバーとビデオのミニポート ドライバー間 COPP 情報を転送に使用できます。 ドライバーはことができますデータ構造と Ioctl を使用するか、必要に応じて、新しいものを作成します。

```cpp
typedef struct {
    PVOID* ppThis;
    PVOID InputBuffer;
    HRESULT phr;
} COPP_IO_InputBuffer;

#define IOCTL_COPP_OpenDevice \
        CTL_CODE(FILE_DEVICE_VIDEO, 2190, METHOD_BUFFERED, FILE_ANY_ACCESS)
#define IOCTL_COPP_CloseDevice \
        CTL_CODE(FILE_DEVICE_VIDEO, 2191, METHOD_BUFFERED, FILE_ANY_ACCESS)
#define IOCTL_COPP_GetCertificateLength \
        CTL_CODE(FILE_DEVICE_VIDEO, 2192, METHOD_BUFFERED, FILE_ANY_ACCESS)
#define IOCTL_COPP_KeyExchange \
        CTL_CODE(FILE_DEVICE_VIDEO, 2193, METHOD_BUFFERED, FILE_ANY_ACCESS)
#define IOCTL_COPP_StartSequence \
        CTL_CODE(FILE_DEVICE_VIDEO, 2194, METHOD_BUFFERED, FILE_ANY_ACCESS)
#define IOCTL_COPP_Command \
        CTL_CODE(FILE_DEVICE_VIDEO, 2195, METHOD_BUFFERED, FILE_ANY_ACCESS)
#define IOCTL_COPP_Status \
        CTL_CODE(FILE_DEVICE_VIDEO, 2196, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

上記の Ioctl を使用しないかどうかは、」の説明に従って、書式設定する必要があります、独自のプライベート Ioctl を定義する[I/O 制御コードを定義する](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)します。

 

 





