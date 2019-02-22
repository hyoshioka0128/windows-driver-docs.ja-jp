---
title: Direct3D のバージョン 11 DDI との通信を初期化しています
description: Direct3D のバージョン 11 DDI との通信を初期化しています
ms.assetid: 3b383f78-da88-4979-b55f-8e234f230df7
keywords:
- DDI 通信を初期化して、Direct3D バージョン 11 WDK Windows 7 表示
- DDI 通信を初期化して、Direct3D バージョン 11 WDK Windows Server 2008 R2 表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74d6c0c926b04793a2fc26f1fc28d0a914d72b06
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528695"
---
# <a name="initializing-communication-with-the-direct3d-version-11-ddi"></a>Direct3D のバージョン 11 DDI との通信を初期化しています


このセクションでは、Windows 7 以降および Windows Server 2008 R2 以降のバージョンの Windows オペレーティング システムにのみ適用されます。

ユーザー モードのディスプレイ ドライバー DLL のバージョン 11 との通信を初期化するために DDI、Direct3D のバージョン 11 ランタイムでは、DLL がまだ読み込まれていない場合、DLL が最初に読み込みます。 Direct3D ランタイムが次に、ユーザー モードのディスプレイ ドライバーを呼び出す[ **OpenAdapter10\_2** ](https://msdn.microsoft.com/library/windows/hardware/ff568603)グラフィックス アダプターのインスタンスを開く、DLL のエクスポート テーブルを使用して関数。 **OpenAdapter10\_2**関数は DLL の関数をエクスポートします。

**注**   、 [ **OpenAdapter10\_2** ](https://msdn.microsoft.com/library/windows/hardware/ff568603)関数のと同じですが、 [ **OpenAdapter10** ](https://msdn.microsoft.com/library/windows/hardware/ff568602)関数点を除いて**OpenAdapter10\_2**でドライバーのアダプター固有の関数のテーブルを返します、 **pAdapterFuncs\_2**のメンバー、[ **D3D10DDIARG\_OPENADAPTER** ](https://msdn.microsoft.com/library/windows/hardware/ff541724)構造、および**OpenAdapter10**でドライバーのアダプター固有の関数のテーブルを返します、D3D10DDIARG の pAdapterFuncs メンバー\_OPENADAPTER します。 **pAdapterFuncs\_2**を指す、 [ **D3D10\_2DDI\_ADAPTERFUNCS** ](https://msdn.microsoft.com/library/windows/hardware/ff541900)構造体。**pAdapterFuncs**を指す、 [ **D3D10DDI\_ADAPTERFUNCS** ](https://msdn.microsoft.com/library/windows/hardware/ff541811)構造体。

 

[**OpenAdapter10\_2** ](https://msdn.microsoft.com/library/windows/hardware/ff568603)ドライバーの初期化をより効率的に設計されました。 実装する必要があります**OpenAdapter10\_2** Direct3D のバージョン 11 ドライバー。 実装することも**OpenAdapter10\_2** (なくまたはに加えて[ **OpenAdapter10**](https://msdn.microsoft.com/library/windows/hardware/ff568602)) を増やす、Direct3D のバージョン 10.1 ドライバーで、これらのドライバーの効率を初期化します。 実装の詳細については**OpenAdapter10\_2** 、Direct3D バージョン 10.1 ドライバーには、次を参照してください。[バージョンの検出サポート](version-discovery-support.md)します。 **OpenAdapter10\_2**バージョン管理と、ランタイムとドライバーの間には、その他の情報の交換を処理します。

### <a name="span-idversioningspanspan-idversioningspanversioning"></a><span id="versioning"></span><span id="VERSIONING"></span>バージョン管理

[**OpenAdapter10\_2** ](https://msdn.microsoft.com/library/windows/hardware/ff568603)ドライバーのアダプター固有の関数、Direct3D API と Direct3D DDI のバージョンがその direct3d10 方法から処理される方法を変更する処理の詳細については、バージョン管理direct3d10 がバージョン管理が処理する方法の詳細についてを参照してください。 [Direct3D のバージョン 10 DDI との通信を初期化して](initializing-communication-with-the-direct3d-version-10-ddi.md))。 ドライバーの障害発生時に証明書利用者の Direct3D API ではなく**OpenAdapter10\_2**特定バージョンのサポートなしを指定する関数 (と同様**OpenAdapter10\_2**)、ドライバーがサポートしています DDI バージョンを一覧表示は明示的にする必要があります。 Direct3D ランタイムが呼び出すユーザー モードのディスプレイ ドライバーの[ **GetSupportedVersions** ](https://msdn.microsoft.com/library/windows/hardware/ff566807)関数 (ドライバーのアダプター固有の関数のいずれか)、ドライバーがサポートする DDI バージョンを照会します。

少なくとも 2 つの新しい DDI バージョンの Direct3D 11 DDI 関数があります。 各 DDI バージョンでは、DDI が Windows Vista または Windows 7 上で実行するかどうかを区別します。 ただし、Direct3D 11 DDI のサポートは必ずしも D3D に関連付けられているハードウェア機能の完全なサポート\_機能\_レベル\_11。 ドライバーは、Direct3D 11 DDI Direct3D 11 DDI のテセレーションをなどによって公開されているその他の機能をサポートしていないハードウェアでのスレッドの新機能をサポートできます。 次のコードは、各 DDI バージョンを識別する方法を示しています。

```cpp
// D3D11.0 on Vista
#define D3D11_DDI_MAJOR_VERSION 11
#define D3D11_0_DDI_MINOR_VERSION ...
#define D3D11_0_DDI_INTERFACE_VERSION \
    ((D3D11_DDI_MAJOR_VERSION << 16) | D3D11_0_DDI_MINOR_VERSION)
#define D3D11_0_DDI_BUILD_VERSION ...
#define D3D11_0_DDI_SUPPORTED \
    ((((UINT64)D3D11_0_DDI_INTERFACE_VERSION) << 32) | \
    (((UINT64)D3D11_0_DDI_BUILD_VERSION) << 16))

// D3D11.0 on Windows 7
#define D3D11_0_7_DDI_MINOR_VERSION ...
#define D3D11_0_7_DDI_INTERFACE_VERSION \
    ((D3D11_DDI_MAJOR_VERSION << 16) | D3D11_0_7_DDI_MINOR_VERSION)
#define D3D11_0_7_DDI_BUILD_VERSION ...
#define D3D11_0_7_DDI_SUPPORTED \
    ((((UINT64)D3D11_0_7_DDI_INTERFACE_VERSION) << 32) | \
    (((UINT64)D3D11_0_7_DDI_BUILD_VERSION) << 16))
 
#ifndef IS_D3D11_WIN7_INTERFACE_VERSION
#define IS_D3D11_WIN7_INTERFACE_VERSION( i ) (D3D11_0_7_DDI_INTERFACE_VERSION == i)
#endif 
```

### <a name="span-idinformationexchangespanspan-idinformationexchangespaninformation-exchange"></a><span id="information_exchange"></span><span id="INFORMATION_EXCHANGE"></span>情報交換

バージョンについては、ドライバーを指定するだけでなく[ **OpenAdapter10\_2** ](https://msdn.microsoft.com/library/windows/hardware/ff568603)関数も、ランタイムとドライバーの間には、その他の情報を交換します。

ドライバーの呼び出しで[ **OpenAdapter10\_2** ](https://msdn.microsoft.com/library/windows/hardware/ff568603)関数の場合、ランタイムは、提供、 [ **pfnQueryAdapterInfoCb** ](https://msdn.microsoft.com/library/windows/hardware/ff568920)アダプターのコールバック関数で、 **pAdapterCallbacks**のメンバー、 [ **D3D10DDIARG\_OPENADAPTER** ](https://msdn.microsoft.com/library/windows/hardware/ff541724)構造体。 ユーザー モードのディスプレイ ドライバーを呼び出す必要があります、 **pfnQueryAdapterInfoCb**ディスプレイのミニポート ドライバーからのグラフィックス ハードウェア機能のクエリをアダプター コールバック関数。

共通言語ランタイムは、ユーザー モードのディスプレイ ドライバーの[ **CreateDevice(D3D10)** ](https://msdn.microsoft.com/library/windows/hardware/ff540635)レンダリング状態のコレクションを処理するためのディスプレイ デバイスを作成する機能 (ドライバーのアダプター固有の関数の 1 つ)初期化を完了して。 初期化が完了したら、Direct3D のバージョン 11 ランタイムが呼び出すことができます、[表示 Direct3D バージョン 11 の機能のドライバーによって提供される](https://msdn.microsoft.com/library/windows/hardware/ff552924)、ユーザー モードのディスプレイ ドライバーが呼び出すことができます、[ランタイムが指定した関数](https://msdn.microsoft.com/library/windows/hardware/ff552862).

ユーザー モードのディスプレイ ドライバーの CreateDevice(D3D10) 関数を呼び出すと、 [ **D3D10DDIARG\_CREATEDEVICE** ](https://msdn.microsoft.com/library/windows/hardware/ff541664)構造体のメンバーが設定されて次のように初期化するために、ユーザー モードのディスプレイ ドライバーのバージョン 11 DDI:

-   ランタイム セット**インターフェイス**ユーザー モードのディスプレイ ドライバーからランタイムを必要とするインターフェイスのバージョンにします。

-   ランタイム セット**バージョン**ドライバーは、ランタイムのビルド時に識別するために使用できる数にします。 たとえば、ドライバーは、Windows Vista でリリースされたランタイムと、ランタイムが後続のサービス パック、ドライバーが必要な修正プログラムが含まれているリリースを区別するために、バージョン番号を使用できます。

-   ランタイム セット**hRTDevice**ランタイムを呼び出し、ドライバーとドライバーが使用するハンドルを指定します。

-   ランタイム セット**hDrvDevice**ドライバーの後続の呼び出しで、ランタイムを使用するハンドルを指定します。

-   ランタイムでは、そのデバイスに固有のコールバック関数のテーブルを提供する、 [ **D3DDDI\_DEVICECALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff544512)構造体**pKTCallbacks**ポイント. ユーザー モードのディスプレイ ドライバーは、ディスプレイのミニポート ドライバーでのカーネル モードのサービスへのアクセスにランタイムが提供するコールバック関数を呼び出します。

-   ユーザー モードのディスプレイ ドライバーがそのデバイスに固有の関数でのテーブルを返します、 [ **D3D11DDI\_DEVICEFUNCS** ](https://msdn.microsoft.com/library/windows/hardware/ff542141)構造体**p11DeviceFuncs**ポイント。

-   ランタイムを提供、 [ **DXGI\_DDI\_ベース\_ARGS** ](https://msdn.microsoft.com/library/windows/hardware/ff557485)構造体**DXGIBaseDDI**ポイント。 ランタイムとユーザー モード ドライバーの供給を表示、 [DirectX グラフィックス インフラストラクチャ DDI](directx-graphics-infrastructure-ddi.md)この構造にします。

-   ランタイム セット**hRTCoreLayer** direct3d10 のコア機能にアクセスするランタイムを呼び出し、ドライバーとドライバーが使用するハンドルを指定する (関数の呼び出しを**p11UMCallbacks**メンバーを指定します)。

-   ランタイムでその中核となるコールバック関数のテーブルを提供する、 [ **D3D11DDI\_CORELAYER\_DEVICECALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff542137)構造体**p11UMCallbacks**ポイント。 ユーザー モードのディスプレイ ドライバーは、ランタイムが指定した主要な状態を更新するコールバック関数を呼び出します。

 

 





