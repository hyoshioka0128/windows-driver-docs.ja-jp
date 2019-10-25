---
title: 圧縮バッファーおよびデコード レンダー ターゲットの作成
description: 圧縮バッファーおよびデコード レンダー ターゲットの作成
ms.assetid: 4d386b72-24d9-424b-8d48-7eaf75aab76c
keywords:
- ビデオデコード WDK DirectX VA、レンダーターゲット
- ビデオのデコード (WDK DirectX VA、レンダーターゲット)
- ビデオデコード WDK DirectX VA、圧縮バッファー
- ビデオをデコードする WDK DirectX VA、圧縮バッファー
- 圧縮バッファー WDK DirectX VA
- バッファー WDK DirectX VA
- レンダーターゲット WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96eb384b7141acc06919e41252d596eff5156a36
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839021"
---
# <a name="creating-compressed-buffers-and-decode-render-targets"></a>圧縮バッファーおよびデコード レンダー ターゲットの作成


Microsoft Direct3D ランタイムは、ユーザーモードの display driver の[**Createresource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)関数を呼び出して、圧縮されたバッファーを作成し、デコードするターゲットをレンダリングします。

圧縮されたバッファーの各型には、独自の表面形式と、ランタイムによって作成されるサーフェイスに高速ビデオデコード用の圧縮されたバッファー情報が含まれていることを示す特殊なフラグがあります。 ユーザーモードの表示ドライバーは、 [**D3DDDIARG\_CREATERESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)構造体の**Flags**メンバーの**DecodeCompressedBuffer**ビットフィールドフラグが、 *presource*パラメーターに指定されている場合、圧縮されたバッファーを作成することを決定します。[**Createresource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)ポイントがに設定されています。 ユーザーモードの表示ドライバーは、D3DDDIARG\_CREATERESOURCE の**形式**のメンバーの形式値によって作成される圧縮バッファーの種類を決定します。 次の形式が定義されています。

```cpp
D3DDDIFMT_PICTUREPARAMSDATA       = 150
D3DDDIFMT_MACROBLOCKDATA          = 151
D3DDDIFMT_RESIDUALDIFFERENCEDATA  = 152
D3DDDIFMT_DEBLOCKINGDATA          = 153
D3DDDIFMT_INVERSEQUANTIZATIONDATA = 154
D3DDDIFMT_SLICECONTROLDATA        = 155
D3DDDIFMT_BITSTREAMDATA           = 156
```

Direct3D ランタイムは、ユーザーモードの表示ドライバーの[**Createresource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)関数の呼び出しで、各デコードレンダーターゲットを個別に作成します。 各ターゲットは、1つのリソースのサブリソースインデックスとして参照されます。 D3DDDIARG\_CREATERESOURCE の**Flags**メンバーの**DecodeRenderTarget**ビットフィールドフラグが設定されている場合、ユーザーモード表示ドライバーはデコードレンダーターゲットを作成することを決定します。

 

 





