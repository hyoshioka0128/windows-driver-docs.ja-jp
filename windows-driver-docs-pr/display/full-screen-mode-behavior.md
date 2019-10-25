---
title: 全画面表示モードの動作
description: 全画面表示モードの動作
ms.assetid: 43e7fec0-4e4d-401c-80c7-3e0710313214
keywords:
- 全画面回転の WDK 表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2853d61a753e1b6811ed46cf1cdca9643c8160e5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839690"
---
# <a name="full-screen-mode-behavior"></a>全画面表示モードの動作


ユーザーモードの表示ドライバーでは、レンダリングデバイスが全画面表示モードであることを確認できます。

-   **全画面**のビットフィールドフラグが、ドライバーの[**openresource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_openresource)関数の呼び出し*で、* [**D3DDDIARG\_openresource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_openresource)構造体の**Flags**メンバーに設定されている場合。

-   **プライマリ**ビットフィールドフラグが、ドライバーの[**createresource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)関数への呼び出しで、 [**D3DDDIARG\_Createresource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)構造体の**Flags**メンバーに設定されている場合は、 *presource*パラメーターが指すようになります。

Microsoft DirectX 9.0 以前用に開発されたアプリケーションでは、Microsoft Direct3D ランタイムが*Openresource*を呼び出して共有プライマリサーフェイスを開き、*その後、* 追加のバックバッファーを作成します。 Microsoft DirectX 9L アプリケーションでは、Direct3D ランタイムは、( *Openresource*を呼び出さずに) *createresource*を呼び出して、すべてのスワップチェーンバッファーを作成します。 Direct3D ランタイムは、 *Presource*パラメーターが指す[**D3DDDIARG\_Openresource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_openresource)および[**D3DDDIARG\_Createresource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)構造体の**回転**メンバーの主な表面向きを指定します。[**Openresource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_openresource)関数と[**createresource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)関数の両方を呼び出します。

全画面表示のデバイスでは、ユーザーモードの表示ドライバーは、回転されたリソースをロックし、回転したリソースにレンダリングし、回転されたリソースからビットブロック転送 (bitblt) を実行する必要があります。 通常、ユーザーモード表示ドライバーは、中間のレンダーターゲットを回転方向に作成し (すべてのロック、bitblts、およびレンダリングは、これらの中間レンダーターゲットに送られます)、横方向のプライマリ割り当て (つまり、digital to アナログコンバーター \[DAC\] を使用したスキャン)。 ユーザーモードの表示ドライバーを呼び出してデータを反転すると、中間のレンダーターゲットからランドスケープバッファーへの回転が実行されてから、フリップコマンドを発行するために[**Pfnを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_presentcb)呼び出すことができます。

ユーザーモードの表示ドライバーで、回転されたリソースと回転されていないリソースを含む bitblt を実行する必要がある場合、Direct3D ランタイムでは、 [**D3DDDIARG\_BLT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_blt)の**Flags**メンバーの**回転**ビットフィールドフラグが指定されます。bitblt に対して適切な回転が行われる必要があることをドライバーに示すために、ドライバーの[**Blt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_blt)関数の呼び出しの構造体。

DirectX 9L アプリケーションは、ローテーション対応であることができます。つまり、すべてが適切な向きでレンダリングされ、回転されたバッファーへのロックが適切に処理されます。 Direct3D ランタイムが回転対応アプリケーションのスワップチェーンを作成すると、ランタイムは常に、 [**D3DDDIARG\_CREATERESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)の**ローテーション**メンバーの D3DDDI\_ローテーション\_id として回転を指定します。ユーザーモードの表示ドライバーは、ローテーション対応アプリケーションを動作させるために特別な操作を実行する必要がないため、構造体です。

 

 





