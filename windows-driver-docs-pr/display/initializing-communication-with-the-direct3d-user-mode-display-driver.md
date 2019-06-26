---
title: D3D ユーザー モードのディスプレイ ドライバーの通信を初期化しています
description: Direct3D のユーザー モード ディスプレイ ドライバーの通信の初期化
ms.assetid: 96e85df4-e340-4017-b348-7c24349ffe69
keywords:
- ユーザー モードのディスプレイ ドライバー WDK Windows Vista では、初期化しています
- Direct3D の WDK の表示
- ユーザー モード ドライバー WDK Windows Vista では、Direct3D の表示します。
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 8ee840f853b13ee5788c337dd90bafef21637309
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385191"
---
# <a name="initializing-communication-with-the-direct3d-user-mode-display-driver"></a>Direct3D のユーザー モード ディスプレイ ドライバーの通信の初期化

ダイナミック リンク ライブラリ (DLL) には、マイクロソフトの Direct3D ユーザー モード ディスプレイ ドライバーとの通信を初期化するために、Direct3D ランタイムは、まず、DLL を読み込みます。 Direct3D ランタイムが次に、ユーザー モードのディスプレイ ドライバーを呼び出す[ **OpenAdapter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_openadapter)グラフィックス アダプターのインスタンスを開く、DLL のエクスポート テーブルを使用して関数。 *OpenAdapter*関数は DLL の関数をエクスポートします。

ドライバーの呼び出しで*OpenAdapter*関数の場合、ランタイムは、提供、 [ **pfnQueryAdapterInfoCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_queryadapterinfocb)アダプターのコールバック関数で、 **pAdapterCallbacks**のメンバー、 [ **D3DDDIARG\_OPENADAPTER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_openadapter)構造体。 ランタイムでは、そのバージョンにも用意されて、**インターフェイス**と**バージョン**D3DDDIARG のメンバー\_OPENADAPTER します。 ユーザー モードのディスプレイ ドライバーは、このバージョンのランタイムを使用できることを確認する必要があります。 ユーザー モードのディスプレイ ドライバーがそのアダプターに固有の関数でのテーブルを返します、 **pAdapterFuncs** D3DDDIARG のメンバー\_OPENADAPTER します。

ユーザー モードのディスプレイ ドライバーを呼び出す必要があります、 [ **pfnQueryAdapterInfoCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_queryadapterinfocb)ディスプレイのミニポート ドライバーからのグラフィックス ハードウェア機能のクエリをアダプター コールバック関数。

共通言語ランタイムは、ユーザー モードのディスプレイ ドライバーの[ **CreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createdevice)とにレンダリング状態のコレクションを処理するためのディスプレイ デバイスを作成する機能 (ドライバーのアダプター固有の関数の 1 つ)初期化を完了します。 初期化が完了したら、Direct3D のランタイムが呼び出すことができます、[表示機能のドライバーによって提供される](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)、ユーザー モードのディスプレイ ドライバーが呼び出すことができます、[ランタイムが指定した関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

ユーザー モードのディスプレイ ドライバーの*CreateDevice*関数を呼び出すと、 [ **D3DDDIARG\_CREATEDEVICE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_createdevice)構造体のメンバーで設定しますユーザー モードのディスプレイ ドライバー インターフェイスを初期化するために次の方法:

-   ランタイム セット**インターフェイス**ユーザー モードのディスプレイ ドライバーからランタイムを必要とするインターフェイスのバージョンにします。

-   ランタイム セット**バージョン**ドライバーは、ランタイムのビルド時に識別するために使用できる数にします。 たとえば、ドライバーは、Windows Vista でリリースされたランタイムと、ランタイムが後続のサービス パック、ドライバーが必要な修正プログラムが含まれているリリースを区別するために、バージョン番号を使用できます。

-   ランタイム セット**hDevice**ランタイムを呼び出し、ドライバーとドライバーが使用するハンドルを指定します。 ドライバーは、一意のハンドルを生成し、内で実行時に戻して**hDevice**します。 ランタイムは、返されたを使用する必要があります**hDevice**ドライバーの後続の呼び出しで処理します。

-   ランタイムでは、そのデバイスに固有のコールバック関数のテーブルを提供する、 [ **D3DDDI\_DEVICECALLBACKS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddi_devicecallbacks)構造体**pCallbacks**ポイント。 ユーザー モードのディスプレイ ドライバーは、ディスプレイのミニポート ドライバーでのカーネル モードのサービスへのアクセスにランタイムが提供するコールバック関数を呼び出します。

-   ユーザー モードのディスプレイ ドライバーがそのデバイスに固有の関数でのテーブルを返します、 [ **D3DDDI\_DEVICEFUNCS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddi_devicefuncs)構造体**pDeviceFuncs**ポイント。

**注**  同時に存在可能な表示デバイス (グラフィックス コンテキスト) の数が使用可能なシステム メモリによってのみ制限されます。

 

 

 





