---
title: MIP マップ サーフェス作成の更新
description: MIP マップ サーフェス作成の更新
ms.assetid: a89a11ed-d450-43bb-b0cd-75132d19dbc3
keywords:
- MIP マップ サーフェス WDK Direct3D
- D3DRENDERSTATE_MIPMAPLODBIAS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd7bf824c217ba44d18926f327f941b0c9b8a432
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358416"
---
# <a name="mip-map-surface-creation-update"></a>MIP マップ サーフェス作成の更新


## <span id="ddk_mip_map_surface_creation_update_gg"></span><span id="DDK_MIP_MAP_SURFACE_CREATION_UPDATE_GG"></span>


DirectX 7.0 では、前に添付ファイル チェーンの MIP マップは、通常その MIP マップのサブレベルのみを行いました。 立方体環境マップの登場によって、これは、不要になった場合。 自体の立方体の環境の各面が MIP マップをする可能性があり、キューブ マップの他の面へのリンクと同様、MIP マップの下位レベルへのリンクの立方体環境マップの 1 つの面を形成のサーフェスの添付ファイルのチェーンがそのためで構成できます。

新しい機能のビットがされているように、添付ファイルのチェーンの MIP マップの画面は、サーフェスを低いレベル MIP マップだけ以外へのリンクを含めるようになりましたことができます、導入された、DDSCAPS2\_MIPMAPSUBLEVEL (を参照してください、 [ **DDSCAPS2**](https://msdn.microsoft.com/library/windows/hardware/ff550292)ここと、次のフラグの構造)。 このビットは、MIP マップ チェーンの最上位レベルの画面がすべて設定されます。 つまり、DDSCAPS2 した画面を探して、最上位のサーフェイスの添付ファイル リストを走査して、MIP マップ チェーンの次の最低レベルを表す、サーフェイスを見つけることができます、MIP マップ チェーンの最上位レベルの画面を与え\_MIPMAPSUBLEVEL機能ビットが設定されます。

機能は、サーフェイスがサーフェイスでのチェック、立方体環境マップの面であるかどうかを DDSCAPS2 をビット\_キューブ マップします。 場合、DDSCAPS\_MIPMAP 機能ビットが設定されていない、この画面の添付ファイルの一覧が作成されているキューブ マップの他の面から成る (確認機能ビット DDSCAPS2\_キューブ マップ\_POSITIVEX、DDSCAPS2\_CUBEMAP\_NEGATIVEX、DDSCAPS2\_CUBEMAP\_POSITIVEY、DDSCAPS2\_CUBEMAP\_NEGATIVEY、DDSCAPS2\_CUBEMAP\_POSITIVEZ、DDSCAPS2\_CUBEMAP\_NEGATIVEZ)。

場合、DDSCAPS\_MIPMAP 機能ビットを設定し、キューブ マップの画面の表面添付のリストは、キューブ マップには、上記の他の面およびこの面の MIP マップの次のレベルへのリンクで構成されます。 MIP マップのサブレベル、DDSCAPS2 によって識別される\_上記で説明した MIPMAPSUBLEVEL ビット。

### <a name="span-idd3drenderstatemipmaplodbiasspanspan-idd3drenderstatemipmaplodbiasspand3drenderstatemipmaplodbias"></a><span id="d3drenderstate_mipmaplodbias"></span><span id="D3DRENDERSTATE_MIPMAPLODBIAS"></span>D3DRENDERSTATE\_MIPMAPLODBIAS

その機能はテクスチャ ステージの状態、つまり、D3DRENDERSTATE に移動されましたこのレンダリング状態は廃止されていますが、\_MIPMAPLODBIAS は D3DTSS、まったく同じです\_MIPMAPLODBIAS の列挙子で、テクスチャのステージ 0 の D3DTEXTURESTAGESTATETYPE 列挙型。 受信する、D3DRENDERSTATE\_MIPMAPLODBIAS レガシー インターフェイスを介しての状態を表示するには、ドライバーする必要があります単にこれをマップ D3DTSS を処理するのと同じコード\_のテクスチャ MIPMAPLODBIAS ステージ 0。

MIP マップ LOD バイアスは、詳細 (LOD) の差のレベルを変更するために使用する浮動小数点値です。 この値は、トリリニア テクスチャで計算された、MIP マップ レベルの値をオフセットします。 通常、範囲の場合は-1.0 1.0;既定値は、0.0 です。 現在/DCT WHQL テストには、MIP マップ LOD バイアス 3.0-3.0 範囲で動作する必要があります。

(1.0) +/-各単位バイアスはバイアス MIP マップ レベルの 1 つだけを選択します。 負の値、バイアスとをシャープがエイリアス化されたイメージの詳細について、その結果より大きなの MIP マップ レベルの使用です。 正のバイアスは、日ごとのイメージに小さい MIP マップ レベルの使用とします。 少量のテクスチャ データは、一部のシステムのパフォーマンスを向上させることができますを参照することも負の値、バイアスを適用する結果します。

**注**   DirectX 9.0 と以降のアプリケーションは、D3DSAMP を使用できる\_MIPMAPLODBIAS mipmap のバイアスの詳細のレベルを制御する D3DSAMPLERSTATETYPE 列挙値。 ランタイムは、ユーザー モード サンプラーの状態をマップ (D3DSAMP\_*Xxx*) には、カーネル モード D3DTSS\_*Xxx*値ドライバーがユーザー モード サンプラーの状態を処理する必要はありません。 ドライバーは引き続き、D3DTSS を処理する必要があります\_MIPMAPLODBIAS 値。 D3DSAMPLERSTATETYPE の詳細については、DirectX SDK の最新のドキュメントを参照してください。

 

 

 





