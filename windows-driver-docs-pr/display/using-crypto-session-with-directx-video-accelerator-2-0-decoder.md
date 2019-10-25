---
title: DXVA 2.0 デコーダーでの Crypto Session の使用
description: DirectX ビデオ アクセラレータ 2.0 デコーダーでの暗号化セッションの使用
ms.assetid: 2a3577f5-bc44-4e0d-a5fa-217dc6c6f5f3
keywords:
- DXVA 2.0 デコーダー WDK Windows 7 ディスプレイ
- DXVA 2.0 デコーダー WDK Windows Server 2008 R2 ディスプレイ
- DXVA 2.0 デコーダー WDK Windows 7 display、crypto session との関連付け
- DXVA 2.0 デコーダー WDK Windows Server 2008 R2 の表示、暗号化セッションとの関連付け
- DirectX Video Accelerator 2.0 デコーダー WDK Windows 7 ディスプレイ
- DirectX Video Accelerator 2.0 デコーダー WDK Windows Server 2008 R2 ディスプレイ
- DirectX Video Accelerator 2.0 デコーダー WDK Windows 7 display、crypto session との関連付け
- DirectX Video Accelerator 2.0 デコーダー WDK Windows Server 2008 R2 表示、暗号化セッションに関連付けられる
- crypto session WDK Windows 7 display
- 暗号化セッション WDK Windows Server 2008 R2 ディスプレイ
- crypto session WDK Windows 7 display, DXVA 2.0 デコーダーとの関連付け
- crypto session WDK Windows Server 2008 R2 display, DXVA 2.0 デコーダーとの関連付け
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: da1d0b85f66f22fa247d4520a6b453ed750c4400
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825392"
---
# <a name="using-crypto-session-with-directx-video-accelerator-20-decoder"></a>DirectX ビデオ アクセラレータ 2.0 デコーダーでの暗号化セッションの使用


このセクションは、windows 7 以降、および windows Server 2008 R2 以降のバージョンの Windows オペレーティングシステムにのみ適用されます。

ユーザーモード表示ドライバーでは、暗号化セッションを DirectX ビデオアクセラレータ (VA) 2.0 デコードデバイスに関連付けることができます。これにより、DirectX VA 2.0 デコードデバイスで暗号化セッションのセッションキーが使用されるようになります。 ランタイムが暗号化を作成するためにドライバーの[**CREATECRYPTOSESSION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createcryptosession)関数を呼び出したときに、Direct3D ランタイムが[**D3DDDIARG\_CREATECRYPTOSESSION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_createcryptosession)構造体の**DecodeProfile**メンバーに有効なデコード GUID を指定する場合セッションでは、ランタイムは D3DAUTHETICATEDCONFIGURE\_CRYPTOSESSION set を使用してドライバーの[**ConfigureAuthenticatedChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_configureauthenicatedchannel)関数を呼び出し、DirectX VA 2.0 デコードデバイスとの暗号化セッションを構成することができます。 DirectX VA 2.0 デコードデバイスで暗号化セッションを構成する前に、ランタイムはドライバーの[**DecodeExtensionExecute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_decodeextensionexecute)関数を呼び出して、directx va 2.0 デコードデバイスのドライバーハンドルを取得する必要があります。 ランタイムは、 [**D3DDDIARG\_DECODEEXTENSIONEXECUTE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_decodeextensionexecute)構造体のメンバーを次の値に設定して、DirectX VA 2.0 デコードデバイスのドライバーハンドルを取得します。

```cpp
#define DXVA2_DECODE_GET_DRIVER_HANDLE    0x725
D3DDDIARG_DECODEEXTENSIONEXECUTE.Function = DXVA2_DECODE_GET_DRIVER_HANDLE;
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateInput->pData = NULL;
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateInput->DataSize = 0;
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateOutput->pData = HANDLE*;
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateOutput->DataSize = sizeof(HANDLE);
```

ランタイムが、DirectX VA 2.0 デコードデバイスを作成するためにドライバーの[**CreateDecodeDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createdecodedevice)関数を呼び出すと、 [**DXVADDI\_configピクチャデコード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_configpicturedecode)構造内のデコード暗号化 guid に0が指定されます。

ランタイムは、 [**D3DDDIARG\_CreateCryptoSession**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_createcryptosession)構造体の**cryptotype**メンバーを使用してドライバーの[**CreateCryptoSession**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createcryptosession)関数を呼び出した後、\_に設定されている AES128\_CTR を使用して暗号を作成します。session: [**D3DDDIARG\_DECODEBEGINFRAME**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_decodebeginframe)構造体の**Ppvpsetkey**メンバーの設定は、ドライバーの[**DECODEBEGINFRAME**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_decodebeginframe)関数を呼び出してフレームをデコードするときに、次の意味を示します。

-   **Ppvpsetkey**が**NULL**に設定されている場合、フレームのバッファーに暗号化されたデータが含まれていないため、復号化は必要ありません。

-   **Ppvpsetkey**が NULL\_GUID (すべてゼロ) を指している場合、フレームのバッファーはセッションキーで暗号化されます。

-   **Ppvpsetkey**がコンテンツキーを指している場合は、アプリケーションがコンテンツキーを暗号化するためにセッションキーを使用したことを示します。 ドライバーは、このコンテンツキーを使用して、このフレームに関連付けられているすべての暗号化されたバッファーの暗号化を解除する必要があります。

暗号化された各バッファーの初期化ベクターは、ドライバーの[**DecodeExecute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_decodeexecute)関数の呼び出しで、 [**DXVADDI\_DECODEBUFFERDESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_decodebufferdesc)構造体の**pCipherCounter**メンバーに表示されます。 初期化ベクターが以前に同じコンテンツキー (コンテンツキーが使用されていない場合はセッションキー) に対して使用されていると判断した場合、ドライバーは*DecodeExecute*関数への呼び出しに失敗する必要があります。 アプリケーションは、アプリケーションが暗号化する各バッファーの[**DXVADDI\_PVP\_HW\_iv**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_pvp_hw_iv)の**iv**メンバーをインクリメントする必要があります。 そのため、 **iv**メンバーが*DecodeExecute*に渡された前の**iv**値以下の場合、ドライバーの*DecodeExecute*関数は失敗する可能性があります。

ランタイムがバッファーを部分的に暗号化する必要がある場合は、ドライバーの[**DecodeExtensionExecute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_decodeextensionexecute)関数を呼び出し、 [**D3DDDIARG\_DecodeExtensionExecute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_decodeextensionexecute)構造体のメンバーを次の値に設定して、のブロックを指定します。ドライバーは次を暗号化する必要があります。

```cpp
#define DXVA2_DECODE_SPECIFY_ENCRYPTED_BLOCKS    0x724
D3DDDIARG_DECODEEXTENSIONEXECUTE.Function = DXVA2_DECODE_SPECIFY_ENCRYPTED_BLOCKS;
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateInput->pData = D3DENCRYPTED_BLOCK_INFO*;
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateInput->DataSize = sizeof(D3DENCRYPTED_BLOCK_INFO);
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateOutput->pData = NULL;
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateOutput->DataSize = 0;
```

 

 





