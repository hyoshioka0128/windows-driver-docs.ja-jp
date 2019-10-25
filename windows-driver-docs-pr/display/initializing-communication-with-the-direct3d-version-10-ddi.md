---
title: Direct3D バージョン 10 DDI との通信の初期化
description: Direct3D バージョン 10 DDI との通信の初期化
ms.assetid: dc3cc26f-7295-46d6-9bd7-aae7027ea92c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dff83a93cff3b5668825e23c9ce569f19bfe49c2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840375"
---
# <a name="initializing-communication-with-the-direct3d-version-10-ddi"></a>Direct3D バージョン 10 DDI との通信の初期化


ユーザーモードの display driver DLL のバージョン 10 DDI との通信を初期化するために、DLL がまだ読み込まれていない場合は、まず、Direct3D version 10 runtime によって DLL が読み込まれます。 次に、Direct3D ランタイムは、DLL の export テーブルを介してユーザーモードの表示ドライバーの[**OpenAdapter10**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)関数を呼び出し、グラフィックスアダプターのインスタンスを開きます。 *OpenAdapter10*関数は、DLL の唯一のエクスポートされた Direct3D version 10 関数です。

ドライバーの*OpenAdapter10*関数の呼び出しでは、ランタイムは、 [**D3D10DDIARG\_openadapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_openadapter)構造体の**Padaptercallbacks**メンバーに[**pfnQueryAdapterInfoCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_queryadapterinfocb) adapter コールバック関数を提供します。 また、ランタイムは、D3D10DDIARG\_OPENADAPTER の**インターフェイス**および**バージョン**メンバーでもそのバージョンを提供します。 ユーザーモードの表示ドライバーでは、このバージョンのランタイムを使用できることを確認する必要があります。 新しいバージョンのランタイムでは以前のバージョンの DDI を使用できるため、以前のバージョンの DDI を実装するドライバーと正しく通信できるため、ユーザーモードの表示ドライバーは、新しいバージョンのランタイムを失敗させないようにする必要があります。 ユーザーモードの表示ドライバーは、D3D10DDIARG\_OPENADAPTER の**Padapterfuncs**メンバーで、アダプター固有の関数のテーブルを返します。

ユーザーモードのディスプレイドライバーは、 [**pfnQueryAdapterInfoCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_queryadapterinfocb) adapter コールバック関数を呼び出して、ディスプレイミニポートドライバーからグラフィックスハードウェア機能を照会する必要があります。

ランタイムは、(ドライバーのアダプター固有の関数の1つである) ユーザーモードの表示ドライバーの[**CreateDevice (D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)関数を呼び出して、レンダリング状態のコレクションを処理し、初期化を完了するためのディスプレイデバイスを作成します。 初期化が完了すると、Direct3D バージョン10ランタイムは、ディスプレイドライバーによって提供される[direct3d バージョン10の関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を呼び出すことができます。また、ユーザーモードの表示ドライバーは、[ランタイムが提供する関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を呼び出すことができます。

ユーザーモードの表示ドライバーの*CreateDevice (D3D10)* 関数は、ユーザーモードの表示ドライバーのバージョン 10 DDI を初期化するために次のようにメンバーが設定されている[**D3D10DDIARG\_CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice)構造体を使用して呼び出されます。

-   ランタイムは、ユーザーモードの表示ドライバーからランタイムが必要とするインターフェイスのバージョンに**インターフェイス**を設定します。

-   ランタイムは、ランタイムがビルドされた日時を識別するためにドライバーが使用できる数値に**バージョン**を設定します。 たとえば、ドライバーはバージョン番号を使用して、Windows Vista と共にリリースされたランタイムと、後続の Service Pack と共にリリースされたランタイムを区別できます。この場合、ドライバーに必要な修正が含まれている可能性があります。

-   ランタイムは、ドライバーがランタイムにコールバックするときにドライバーが使用するハンドルを指定するために、 **Hrtdevice**を設定します。

-   ランタイムは、 **hDrvDevice**を設定して、後続のドライバー呼び出しでランタイムが使用するハンドルを指定します。

-   ランタイムは、 **pKTCallbacks**が指す[**D3DDDI\_DEVICECALLBACKS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_devicecallbacks)構造体に、デバイス固有のコールバック関数のテーブルを提供します。 ユーザーモード表示ドライバーは、ランタイム提供のコールバック関数を呼び出して、ディスプレイミニポートドライバーのカーネルモードサービスにアクセスします。

-   ユーザーモード表示ドライバーは、 **Pdevicefuncs**が指す[**D3D10DDI\_devicefuncs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddi_devicefuncs)構造体に、デバイス固有の関数のテーブルを返します。

-   ランタイムは、 **Dxgibaseddi**がポイントする[**DXGI\_DDI\_BASE\_ARGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_args)構造体を提供します。 ランタイムとユーザーモードの表示ドライバーは、この構造に対する[DirectX グラフィックスインフラストラクチャ DDI](directx-graphics-infrastructure-ddi.md)を提供します。

-   ランタイムは、ドライバーがランタイムにコールバックしてコア Direct3D 10 機能 (つまり、 **pUMCallbacks**メンバーが指定する関数の呼び出し) にアクセスするときに、ドライバーが使用するハンドルを指定するように**hRTCoreLayer**を設定します。

-   ランタイムは、 [**D3D10DDI\_CORELAYER\_DEVICECALLBACKS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddi_corelayer_devicecallbacks)構造体に、 **pUMCallbacks**がポイントするコアコールバック関数のテーブルを提供します。 ユーザーモード表示ドライバーは、ランタイムによって提供されるコアコールバック関数を呼び出して、状態を更新します。

同時に存在できるディスプレイデバイス (グラフィックスコンテキスト) の数は、使用可能なシステムメモリによってのみ制限されます   に**注意**してください。

 

 

 





