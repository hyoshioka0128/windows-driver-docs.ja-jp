---
title: 圧縮バッファーおよびデコード レンダー ターゲットの作成
description: 圧縮バッファーおよびデコード レンダー ターゲットの作成
ms.assetid: 4d386b72-24d9-424b-8d48-7eaf75aab76c
keywords:
- WDK の DirectX va なので、レンダー ターゲットをデコードするビデオ
- ビデオの WDK DirectX VA をデコードするには、レンダー ターゲット
- ビデオのデコード WDK DirectX va なので、圧縮されたバッファー
- ビデオの WDK DirectX VA をデコードするには、圧縮バッファー
- 圧縮されたバッファー WDK DirectX VA
- WDK DirectX VA をバッファー処理します。
- レンダー ターゲット WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b274e4a483834275bdc8b4030ec1e8224fff5f8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370202"
---
# <a name="creating-compressed-buffers-and-decode-render-targets"></a>圧縮バッファーおよびデコード レンダー ターゲットの作成


マイクロソフトの Direct3D ランタイムが呼び出すユーザー モードのディスプレイ ドライバーの[ **CreateResource** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)を圧縮されたバッファーを作成し、レンダー ターゲットをデコードします。

各種の圧縮されたバッファーは、ランタイムを作成する画面では、高速のビデオをデコードするために、圧縮されたバッファー情報が含まれることを示す特別なフラグと同様に、独自のサーフェイスの形式があります。 圧縮されたバッファーを作成する場合に、ユーザー モードのディスプレイ ドライバーを決定します、 **DecodeCompressedBuffer**でフラグをビット フィールド、**フラグ**のメンバー、 [ **D3DDDIARG\_CREATERESOURCE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)構造体、 *pResource*パラメーターの[ **CreateResource** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)へのポインターを設定します。 ユーザー モードのディスプレイ ドライバーの形式の値で作成するための圧縮のバッファーの種類を決定する、**形式**D3DDDIARG のメンバー\_CREATERESOURCE します。 次の形式が定義されています。

```cpp
D3DDDIFMT_PICTUREPARAMSDATA       = 150
D3DDDIFMT_MACROBLOCKDATA          = 151
D3DDDIFMT_RESIDUALDIFFERENCEDATA  = 152
D3DDDIFMT_DEBLOCKINGDATA          = 153
D3DDDIFMT_INVERSEQUANTIZATIONDATA = 154
D3DDDIFMT_SLICECONTROLDATA        = 155
D3DDDIFMT_BITSTREAMDATA           = 156
```

Direct3D ランタイムを作成しない各デコード レンダー ターゲット個別に、ユーザー モードのディスプレイ ドライバーの呼び出しで[ **CreateResource** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)関数。 各ターゲットは、1 つのリソースの subresource インデックスとして参照されます。 デコードのレンダー ターゲットを作成する場合に、ユーザー モードのディスプレイ ドライバーを決定します、 **DecodeRenderTarget**でフラグをビット フィールド、**フラグ**D3DDDIARG のメンバー\_CREATERESOURCE を設定します。

 

 





