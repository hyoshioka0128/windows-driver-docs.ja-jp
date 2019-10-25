---
title: Direct3D バージョン 11 DDI との通信の初期化
description: Direct3D バージョン 11 DDI との通信の初期化
ms.assetid: 3b383f78-da88-4979-b55f-8e234f230df7
keywords:
- Direct3D バージョン 11 WDK Windows 7 display、DDI 通信の初期化
- Direct3D バージョン 11 WDK Windows Server 2008 R2 の表示、DDI 通信の初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a08d666739d8daee6028b5055d1f21edda80c10
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840372"
---
# <a name="initializing-communication-with-the-direct3d-version-11-ddi"></a>Direct3D バージョン 11 DDI との通信の初期化


このセクションは、windows 7 以降、および windows Server 2008 R2 以降のバージョンの Windows オペレーティングシステムにのみ適用されます。

ユーザーモードの display driver DLL のバージョン 11 DDI との通信を初期化するために、DLL がまだ読み込まれていない場合は、Direct3D version 11 runtime によって最初に DLL が読み込まれます。 次に、Direct3D ランタイムは、DLL の export テーブルを介してユーザーモード表示ドライバーの[**OpenAdapter10\_2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)関数を呼び出し、グラフィックスアダプターのインスタンスを開きます。 **OpenAdapter10\_2**関数は、DLL の唯一のエクスポート関数です。

[**OpenAdapter10\_2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)関数は、 [**OpenAdapter10**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)関数と同じです **。ただし、** **OpenAdapter10\_2**では、**ドライバーのアダプター固有の関数のテーブルを  ** [**D3D10DDIARG\_openadapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_openadapter)構造体の padapterfuncs\_2 のメンバー。 D3D10DDIARG の padapterfuncs メンバーにあるドライバーのアダプター固有の関数のテーブル**を返し\_** OPENADAPTER。 **Padapterfuncs 2**は、 [**D3D10\_2DDI\_adapterの**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10_2ddi_adapterfuncs)構造体を指します。**Padapterfuncs 関数**は、 [**D3D10DDI\_adapterの**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddi_adapterfuncs)構造体を指します。\_

 

[**OpenAdapter10\_2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)は、初期化ドライバーをより効率的にするように設計されています。 Direct3D バージョン11のドライバーには、 **OpenAdapter10\_2**を実装する必要があります。 また、これらのドライバーの初期化効率を向上させるために、Direct3D バージョン10.1 ドライバーで**OpenAdapter10\_2** ( [**OpenAdapter10**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)に加えて、またはその両方) を実装することもできます。 Direct3D バージョン10.1 ドライバーでの**OpenAdapter10\_2**の実装の詳細については、「[バージョン探索のサポート](version-discovery-support.md)」を参照してください。 **OpenAdapter10\_2**は、ランタイムとドライバー間のバージョン管理とその他の情報の交換を処理します。

### <a name="span-idversioningspanspan-idversioningspanversioning"></a><span id="versioning"></span><span id="VERSIONING"></span>版

[**OpenAdapter10\_2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)とドライバーのアダプター固有の関数によって、direct3d API と direct3d DDI 間のバージョン管理が direct3d 10 のバージョン管理の方法で処理されるようになります (direct3d 10 の処理方法の詳細については、「」を参照してください)。バージョン管理、「 [Direct3D バージョン 10 DDI との通信の初期化](initializing-communication-with-the-direct3d-version-10-ddi.md)」を参照してください。 特定のバージョンがサポートされていないことを示すために ( **OpenAdapter10\_2**と同様に)、ドライバーの**OpenAdapter10\_2**関数の失敗に依存している Direct3D API の代わりに、ドライバーでは、DDI のバージョンを明示的に一覧表示する必要があります。対応. Direct3D ランタイムは、ユーザーモードのディスプレイドライバーの[**Getsupportedversions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10_2ddi_getsupportedversions)関数 (ドライバーのアダプター固有の関数の1つ) を呼び出して、ドライバーがサポートする DDI のバージョンを照会します。

Direct3D 11 DDI functions には、少なくとも2つの新しい DDI バージョンがあります。 各 DDI バージョンは、DDI が Windows Vista または Windows 7 で実行されているかどうかを識別します。 ただし、Direct3D 11 DDI のサポートは、必ずしも D3D\_機能\_レベル\_11 に関連付けられているハードウェア機能の完全なサポートを示しているわけではありません。 ドライバーは、(テセレーションなどの) Direct3D 11 DDI によって公開されている他の機能をサポートしていない、Direct3D 11 DDI の新しいスレッド機能をサポートできます。 次のコードは、各 DDI バージョンがどのように区別されるかを示しています。

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

### <a name="span-idinformation_exchangespanspan-idinformation_exchangespaninformation-exchange"></a><span id="information_exchange"></span><span id="INFORMATION_EXCHANGE"></span>情報交換

ドライバーの[**OpenAdapter10\_2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)関数は、バージョン情報を指定するだけでなく、ランタイムとドライバー間のその他の情報も交換します。

ドライバーの[**OpenAdapter10\_2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)関数の呼び出しでは、ランタイムが[**D3D10DDIARG\_Openadapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_openadapter)の**Padaptercallbacks**メンバーに[**pfnQueryAdapterInfoCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_queryadapterinfocb) adapter コールバック関数を渡します。データ. ユーザーモードのディスプレイドライバーは、 **pfnQueryAdapterInfoCb** adapter コールバック関数を呼び出して、ディスプレイミニポートドライバーからグラフィックスハードウェア機能を照会する必要があります。

ランタイムは、(ドライバーのアダプター固有の関数の1つである) ユーザーモードの表示ドライバーの[**CreateDevice (D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)関数を呼び出して、レンダリング状態のコレクションを処理し、初期化を完了するためのディスプレイデバイスを作成します。 初期化が完了すると、Direct3D バージョン11ランタイムは、ディスプレイドライバーによって提供される[direct3d バージョン11の関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を呼び出すことができます。また、ユーザーモードの表示ドライバーは、[ランタイムが提供する関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を呼び出すことができます。

ユーザーモードの表示ドライバーの CreateDevice (D3D10) 関数は、ユーザーモードの表示ドライバーのバージョン 11 DDI を初期化するために、次のようにメンバーが設定されている[**D3D10DDIARG\_CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice)構造体を使用して呼び出されます。

-   ランタイムは、ユーザーモードの表示ドライバーからランタイムが必要とするインターフェイスのバージョンに**インターフェイス**を設定します。

-   ランタイムは、ランタイムがいつビルドされるかを識別するためにドライバーが使用できる数値に**バージョン**を設定します。 たとえば、ドライバーはバージョン番号を使用して、Windows Vista と共にリリースされたランタイムと、後続の Service Pack と共にリリースされたランタイムを区別できます。この場合、ドライバーに必要な修正が含まれている可能性があります。

-   ランタイムは、ドライバーがランタイムにコールバックするときにドライバーが使用するハンドルを指定するために、 **Hrtdevice**を設定します。

-   ランタイムは、 **hDrvDevice**を設定して、後続のドライバー呼び出しでランタイムが使用するハンドルを指定します。

-   ランタイムは、 **pKTCallbacks**が指す[**D3DDDI\_DEVICECALLBACKS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_devicecallbacks)構造体に、デバイス固有のコールバック関数のテーブルを提供します。 ユーザーモード表示ドライバーは、ランタイム提供のコールバック関数を呼び出して、ディスプレイミニポートドライバーのカーネルモードサービスにアクセスします。

-   ユーザーモード表示ドライバーは、 **p11DeviceFuncs**が指す[**D3D11DDI\_devicefuncs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddi_devicefuncs)構造体に、デバイス固有の関数のテーブルを返します。

-   ランタイムは、 **Dxgibaseddi**がポイントする[**DXGI\_DDI\_BASE\_ARGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_args)構造体を提供します。 ランタイムとユーザーモードの表示ドライバーは、この構造に対する[DirectX グラフィックスインフラストラクチャ DDI](directx-graphics-infrastructure-ddi.md)を提供します。

-   ランタイムは、ドライバーがランタイムにコールバックしてコア Direct3D 10 機能 (つまり、 **p11UMCallbacks**メンバーが指定する関数の呼び出し) にアクセスするときに、ドライバーが使用するハンドルを指定するように**hRTCoreLayer**を設定します。

-   ランタイムは、 [**D3D11DDI\_CORELAYER\_DEVICECALLBACKS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddi_corelayer_devicecallbacks)構造体に、 **p11UMCallbacks**がポイントするコアコールバック関数のテーブルを提供します。 ユーザーモード表示ドライバーは、ランタイムによって提供されるコアコールバック関数を呼び出して、状態を更新します。

 

 





