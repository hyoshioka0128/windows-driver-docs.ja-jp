---
title: DXVA 2.0 での暗号化セッションを使用してデコーダー
description: DirectX ビデオ アクセラレータ 2.0 デコーダーでの暗号化セッションの使用
ms.assetid: 2a3577f5-bc44-4e0d-a5fa-217dc6c6f5f3
keywords:
- DXVA 2.0 デコーダー WDK Windows 7 の表示
- DXVA 2.0 デコーダー WDK Windows Server 2008 R2 の表示
- 暗号化セッションを関連付ける DXVA 2.0 デコーダー WDK Windows 7 の表示
- 暗号化セッションを関連付ける DXVA 2.0 デコーダー WDK Windows Server 2008 R2 の表示
- DirectX ビデオ アクセラレータ 2.0 デコーダー WDK Windows 7 の表示
- DirectX ビデオ アクセラレータ 2.0 デコーダー WDK Windows Server 2008 R2 の表示
- 暗号化セッションを関連付ける DirectX ビデオ アクセラレータ 2.0 デコーダー WDK Windows 7 の表示
- 暗号化セッションを関連付ける DirectX ビデオ アクセラレータ 2.0 デコーダー WDK Windows Server 2008 R2 の表示
- 暗号化セッション WDK Windows 7 の表示
- 暗号化セッション WDK Windows Server 2008 R2 の表示
- 暗号化セッション DXVA 2.0 デコーダーとの関連付けの WDK Windows 7 の表示
- 暗号化セッション DXVA 2.0 デコーダーとの関連付け、WDK の Windows Server 2008 R2 の表示
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: b48df8ff7b8fb12ce20c23b6ac929c0e2837c8bc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389084"
---
# <a name="using-crypto-session-with-directx-video-accelerator-20-decoder"></a>DirectX ビデオ アクセラレータ 2.0 デコーダーでの暗号化セッションの使用


このセクションでは、Windows 7 以降および Windows Server 2008 R2 以降のバージョンの Windows オペレーティング システムにのみ適用されます。

ユーザー モードのディスプレイ ドライバー暗号化セッションを関連付けることができますと DirectX ビデオ アクセラレータ (VA) 2.0 は、デバイスをデバイスで使用する暗号化セッションのセッション キーをデコードする DirectX VA 2.0 の実行をデコードします。 Direct3D のランタイムを有効なデコードに GUID を指定している、 **DecodeProfile**のメンバー、 [ **D3DDDIARG\_CREATECRYPTOSESSION** ](https://msdn.microsoft.com/library/windows/hardware/ff542923)構造体ときに、ランタイムが呼び出す、ドライバーの[ **CreateCryptoSession** ](https://msdn.microsoft.com/library/windows/hardware/ff540609)暗号化セッションを作成する関数をランタイムは、ドライバーを呼び出すことができます、その後[ **ConfigureAuthenticatedChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff539572) D3DAUTHETICATEDCONFIGURE で関数を\_CRYPTOSESSION DirectX VA 2.0 を使用した暗号化セッションを構成する設定がデバイスをデコードします。 デバイスをデコード DirectX VA 2.0 を使用した暗号化セッションを構成する前に、ランタイムは、ドライバーを呼び出す必要があります[ **DecodeExtensionExecute** ](https://msdn.microsoft.com/library/windows/hardware/ff551811) DirectX VA 2.0 用ドライバーのハンドルを取得する関数デバイスをデコードします。 ランタイムのメンバーを設定する、 [ **D3DDDIARG\_DECODEEXTENSIONEXECUTE** ](https://msdn.microsoft.com/library/windows/hardware/ff543009)構造、DirectX VA 2.0 のドライバーのハンドルを取得する次の値には、デバイスをデコードします。

```cpp
#define DXVA2_DECODE_GET_DRIVER_HANDLE    0x725
D3DDDIARG_DECODEEXTENSIONEXECUTE.Function = DXVA2_DECODE_GET_DRIVER_HANDLE;
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateInput->pData = NULL;
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateInput->DataSize = 0;
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateOutput->pData = HANDLE*;
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateOutput->DataSize = sizeof(HANDLE);
```

共通言語ランタイムは、ドライバーの[ **CreateDecodeDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff540618) DirectX VA 2.0 デコード デバイスを作成する関数をランタイム内でデコード暗号化 Guid の場合は 0 を指定します、 [**DXVADDI\_CONFIGPICTUREDECODE** ](https://msdn.microsoft.com/library/windows/hardware/ff562894)構造体。

ランタイムが呼び出す、ドライバーの後に[ **CreateCryptoSession** ](https://msdn.microsoft.com/library/windows/hardware/ff540609)関数と、 **CryptoType**のメンバー、 [ **D3DDDIARG\_CREATECRYPTOSESSION** ](https://msdn.microsoft.com/library/windows/hardware/ff542923) D3DCRYPTOTYPE に設定\_AES128\_crypto のセッションの設定を作成する CTR、 **pPVPSetKey** のメンバー[**D3DDDIARG\_DECODEBEGINFRAME** ](https://msdn.microsoft.com/library/windows/hardware/ff542987)ドライバーの呼び出しで構造[ **DecodeBeginFrame** ](https://msdn.microsoft.com/library/windows/hardware/ff551802)をデコードする関数をフレームでは、次の意味を示します。

-   場合**pPVPSetKey**に設定されている**NULL**、暗号化されたデータが含まれていないフレーム バッファーとそのため、復号化は必要ありません。

-   場合**pPVPSetKey** 、NULL を指す\_GUID (すべてゼロ) のフレームのバッファーがセッション キーで暗号化されます。

-   場合**pPVPSetKey**コンテンツ キーへのポインター、アプリケーションがコンテンツ キーの暗号化にセッション キーを使用することを示します。 ドライバーは、このコンテンツ キーを使用して、このフレームに関連付けられているすべての暗号化されたバッファーを復号化する必要があります。

暗号化された各バッファーの初期化ベクターが表示されます、 **pCipherCounter**のメンバー、 [ **DXVADDI\_DECODEBUFFERDESC** ](https://msdn.microsoft.com/library/windows/hardware/ff562896)の呼び出しで構造体ドライバーの[ **DecodeExecute** ](https://msdn.microsoft.com/library/windows/hardware/ff551808)関数。 呼び出しが失敗するドライバー、 *DecodeExecute*同じコンテンツ キー (または、コンテンツ キーを使用しない場合、セッション キー) の初期化ベクターが使用されていたと判断した場合に機能します。 アプリケーションをインクリメントする必要があります、 **IV**のメンバー、 [ **DXVADDI\_PVP\_HW\_IV** ](https://msdn.microsoft.com/library/windows/hardware/ff562920)ごとにバッファーをアプリケーションが暗号化されます。 そのため、ドライバーの*DecodeExecute*関数が失敗する場合、 **IV**メンバーは、前に小さい**IV**に渡された値*DecodeExecute*します。

ドライバーの場合は、ランタイムは、バッファーを暗号化する必要が部分的に、呼び出す[ **DecodeExtensionExecute** ](https://msdn.microsoft.com/library/windows/hardware/ff551811)関数をセットのメンバー、 [ **D3DDDIARG\_DECODEEXTENSIONEXECUTE** ](https://msdn.microsoft.com/library/windows/hardware/ff543009)構造体をドライバーをブロックするを指定するには、次の値を暗号化する必要があります。

```cpp
#define DXVA2_DECODE_SPECIFY_ENCRYPTED_BLOCKS    0x724
D3DDDIARG_DECODEEXTENSIONEXECUTE.Function = DXVA2_DECODE_SPECIFY_ENCRYPTED_BLOCKS;
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateInput->pData = D3DENCRYPTED_BLOCK_INFO*;
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateInput->DataSize = sizeof(D3DENCRYPTED_BLOCK_INFO);
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateOutput->pData = NULL;
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateOutput->DataSize = 0;
```

 

 





