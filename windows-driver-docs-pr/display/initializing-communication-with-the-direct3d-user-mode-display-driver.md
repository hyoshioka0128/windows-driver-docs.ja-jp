---
title: D3D ユーザーモードの表示ドライバー通信の初期化
description: Direct3D のユーザー モード ディスプレイ ドライバーの通信の初期化
ms.assetid: 96e85df4-e340-4017-b348-7c24349ffe69
keywords:
- ユーザーモード表示ドライバー WDK Windows Vista、初期化
- Direct3D WDK ディスプレイ
- ユーザーモードディスプレイドライバー WDK Windows Vista、Direct3D
ms.date: 09/17/2019
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: bf3e38c3bbdfe67c1aff2e57c0a57b0b069a5fb2
ms.sourcegitcommit: 3246a166d5454c68f77c15267f3f0b347359f505
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/19/2019
ms.locfileid: "71108098"
---
# <a name="initializing-communication-with-the-direct3d-user-mode-display-driver"></a>Direct3D のユーザー モード ディスプレイ ドライバーの通信の初期化

Microsoft Direct3D ユーザーモード表示ドライバー DLL のバージョン 11 DDI との通信を初期化するには、まず、Direct3D ランタイムが DLL を読み込みます。 次に、Direct3D ランタイムは、DLL の export テーブルを介してユーザーモードの表示ドライバーの[**openadapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_openadapter)関数を呼び出し、グラフィックスアダプターのインスタンスを開きます。 *Openadapter*関数は、DLL の唯一のエクスポート関数です。

ドライバーの*openadapter*関数の呼び出しでは、ランタイムは[**D3DDDIARG\_openadapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_openadapter)構造体の**padaptercallbacks**メンバーに[**pfnQueryAdapterInfoCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_queryadapterinfocb) adapter コールバック関数を提供します。 ランタイムは、D3DDDIARG\_openadapter の**インターフェイス**および**バージョン**メンバーでもそのバージョンを提供します。 ユーザーモードの表示ドライバーでは、このバージョンのランタイムを使用できることを確認する必要があります。 ユーザーモードの表示ドライバーは、D3DDDIARG_OPENADAPTER の**Padapterfuncs**メンバーのアダプター固有の関数のテーブルを返します。

ユーザーモードのディスプレイドライバーは、 [**pfnQueryAdapterInfoCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_queryadapterinfocb) adapter コールバック関数を呼び出して、ディスプレイミニポートドライバーからグラフィックスハードウェア機能を照会する必要があります。

ランタイムは、ユーザーモードの表示ドライバーの[**CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createdevice)関数 (ドライバーのアダプター固有の関数の1つ) を呼び出して、レンダリング状態のコレクションを処理し、初期化を完了するためのディスプレイデバイスを作成します。 初期化が完了すると、Direct3D ランタイムは[ディスプレイドライバー](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)によって提供される関数を呼び出すことができ、ユーザーモードの表示ドライバーは[ランタイムが提供する関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)を呼び出すことができます。

ユーザーモード表示ドライバーの*CreateDevice*関数は、ユーザーモードの display driver インターフェイスを初期化するために、次のようにメンバーが設定されている[**D3DDDIARG\_CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_createdevice)構造体を使用して呼び出されます。

- ランタイムは、ユーザーモードの表示ドライバーからランタイムが必要とするインターフェイスのバージョンに**インターフェイス**を設定します。

- ランタイムは、ランタイムがビルドされた日時を識別するためにドライバーが使用できる数値に**バージョン**を設定します。 たとえば、ドライバーはバージョン番号を使用して、Windows Vista と共にリリースされたランタイムと、後続の Service Pack と共にリリースされたランタイムを区別できます。この場合、ドライバーに必要な修正が含まれている可能性があります。

- ランタイムは、ドライバーがランタイムにコールバックするときにドライバーが使用するハンドルを指定するように**Hdevice**を設定します。 ドライバーは一意のハンドルを生成し、 **Hdevice**のランタイムに渡します。 ランタイムは、返された**Hdevice**ハンドルを後続のドライバー呼び出しで使用する必要があります。

- ランタイムは、 **pcallbacks**が指す[**D3DDDI_DEVICECALLBACKS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddi_devicecallbacks)構造体に、デバイス固有のコールバック関数のテーブルを提供します。 ユーザーモード表示ドライバーは、ランタイム提供のコールバック関数を呼び出して、ディスプレイミニポートドライバーのカーネルモードサービスにアクセスします。

- ユーザーモード表示ドライバーは、 **pdevicefuncs**が指す[ **\_D3DDDI devicefuncs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddi_devicefuncs)構造体に、デバイス固有の関数のテーブルを返します。

> [!NOTE]
> 同時に存在できるディスプレイデバイス (グラフィックスコンテキスト) の数は、使用可能なシステムメモリによってのみ制限されます。
