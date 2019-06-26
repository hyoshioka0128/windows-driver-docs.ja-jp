---
title: Direct3D バージョン 10 DDI との通信の初期化
description: Direct3D バージョン 10 DDI との通信の初期化
ms.assetid: dc3cc26f-7295-46d6-9bd7-aae7027ea92c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf86cbea15bd7e5e182a64a5b7da76195ec82694
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385187"
---
# <a name="initializing-communication-with-the-direct3d-version-10-ddi"></a>Direct3D バージョン 10 DDI との通信の初期化


ユーザー モードのディスプレイ ドライバー DLL のバージョンとの通信を初期化するために 10 DDI、Direct3D のバージョン 10 ランタイムでは、DLL がまだ読み込まれていない場合、DLL が最初に読み込みます。 Direct3D ランタイムが次に、ユーザー モードのディスプレイ ドライバーを呼び出す[ **OpenAdapter10** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)グラフィックス アダプターのインスタンスを開く、DLL のエクスポート テーブルを使用して関数。 *OpenAdapter10*関数は DLL の Direct3D のバージョン 10 関数をエクスポートします。

ドライバーの呼び出しで*OpenAdapter10*関数の場合、ランタイムは、提供、 [ **pfnQueryAdapterInfoCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_queryadapterinfocb)アダプターのコールバック関数で、 **pAdapterCallbacks**のメンバー、 [ **D3D10DDIARG\_OPENADAPTER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_openadapter)構造体。 ランタイムでは、そのバージョンにも用意されて、**インターフェイス**と**バージョン**D3D10DDIARG のメンバー\_OPENADAPTER します。 ユーザー モードのディスプレイ ドライバーは、このバージョンのランタイムを使用できることを確認する必要があります。 ユーザー モードのディスプレイ ドライバーでする必要がありますので、新しいランタイム バージョン DDI の以前のバージョンを使用することができ、そのため、これらの以前の DDI バージョンを実装するドライバーと通信できる正しくより新しいバージョンのランタイムは失敗しません。 ユーザー モードのディスプレイ ドライバーがそのアダプターに固有の関数でのテーブルを返します、 **pAdapterFuncs** D3D10DDIARG のメンバー\_OPENADAPTER します。

ユーザー モードのディスプレイ ドライバーを呼び出す必要があります、 [ **pfnQueryAdapterInfoCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_queryadapterinfocb)ディスプレイのミニポート ドライバーからのグラフィックス ハードウェア機能のクエリをアダプター コールバック関数。

共通言語ランタイムは、ユーザー モードのディスプレイ ドライバーの[ **CreateDevice(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)レンダリング状態のコレクションを処理するためのディスプレイ デバイスを作成する機能 (ドライバーのアダプター固有の関数の 1 つ)初期化を完了して。 初期化が完了したら、Direct3D のバージョン 10 ランタイムが呼び出すことができます、[表示 Direct3D バージョン 10 の機能のドライバーによって提供される](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)、ユーザー モードのディスプレイ ドライバーが呼び出すことができます、[ランタイムが指定した関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index).

ユーザー モードのディスプレイ ドライバーの*CreateDevice(D3D10)* 関数を呼び出すと、 [ **D3D10DDIARG\_CREATEDEVICE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice)構造体のメンバーを持つがで設定されます。ユーザー モードのディスプレイ ドライバーのバージョン 10 を初期化するために次のよう DDI:

-   ランタイム セット**インターフェイス**ユーザー モードのディスプレイ ドライバーからランタイムを必要とするインターフェイスのバージョンにします。

-   ランタイム セット**バージョン**ドライバーは、ランタイムのビルド時に識別するために使用できる数にします。 たとえば、ドライバーは、Windows Vista でリリースされたランタイムと、ランタイムが後続のサービス パック、ドライバーが必要な修正プログラムが含まれているリリースを区別するために、バージョン番号を使用できます。

-   ランタイム セット**hRTDevice**ランタイムを呼び出し、ドライバーとドライバーが使用するハンドルを指定します。

-   ランタイム セット**hDrvDevice**ドライバーの後続の呼び出しで、ランタイムを使用するハンドルを指定します。

-   ランタイムでは、そのデバイスに固有のコールバック関数のテーブルを提供する、 [ **D3DDDI\_DEVICECALLBACKS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddi_devicecallbacks)構造体**pKTCallbacks**ポイント. ユーザー モードのディスプレイ ドライバーは、ディスプレイのミニポート ドライバーでのカーネル モードのサービスへのアクセスにランタイムが提供するコールバック関数を呼び出します。

-   ユーザー モードのディスプレイ ドライバーがそのデバイスに固有の関数でのテーブルを返します、 [ **D3D10DDI\_DEVICEFUNCS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddi_devicefuncs)構造体**pDeviceFuncs**ポイント。

-   ランタイムを提供、 [ **DXGI\_DDI\_ベース\_ARGS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_base_args)構造体**DXGIBaseDDI**ポイント。 ランタイムとユーザー モード ドライバーの供給を表示、 [DirectX グラフィックス インフラストラクチャ DDI](directx-graphics-infrastructure-ddi.md)この構造にします。

-   ランタイム セット**hRTCoreLayer** direct3d10 のコア機能にアクセスするランタイムを呼び出し、ドライバーとドライバーが使用するハンドルを指定する (関数の呼び出しを**pUMCallbacks**メンバーを指定します)。

-   ランタイムでその中核となるコールバック関数のテーブルを提供する、 [ **D3D10DDI\_CORELAYER\_DEVICECALLBACKS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddi_corelayer_devicecallbacks)構造体**pUMCallbacks**ポイント。 ユーザー モードのディスプレイ ドライバーは、ランタイムが指定した主要な状態を更新するコールバック関数を呼び出します。

**注**  同時に存在できるディスプレイ デバイス (グラフィックス コンテキスト) の数が使用可能なシステム メモリによってのみ制限されます。

 

 

 





