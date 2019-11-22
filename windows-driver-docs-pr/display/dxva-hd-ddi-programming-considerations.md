---
title: DXVA-HD DDI のプログラミングに関する考慮事項
description: DXVA-HD DDI のプログラミングに関する考慮事項
ms.assetid: 84576a8d-67e1-480a-9323-ef34b0900d22
keywords:
- DXVA-HD DDI WDK Windows 7 の表示、プログラミングに関する考慮事項
- DXVA-HD DDI WDK Server 2008 R2 の表示、プログラミングに関する考慮事項
- 高解像度ビデオ WDK Windows 7 display、DXVA-HD DDI、プログラミングに関する考慮事項
- 高解像度ビデオ WDK Server 2008 R2 display、DXVA-HD DDI、プログラミングに関する考慮事項
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f5e809c16a2f71e470a497ea16263b5ee2402f9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839717"
---
# <a name="dxva-hd-ddi-programming-considerations"></a>DXVA-HD DDI のプログラミングに関する考慮事項


このセクションは、windows 7 以降、および windows Server 2008 R2 以降のバージョンの Windows オペレーティングシステムにのみ適用されます。

ユーザーモード表示ドライバーで[DXVA の DDI](dxva-hd-ddi.md)を実装する場合は、次のプログラミングのヒントを考慮する必要があります。

-   ドライバーは、 [D3DCAPS9](https://go.microsoft.com/fwlink/p/?linkid=122122)構造体の**CAPS3**メンバーで D3DCAPS3\_DXVAHD (0x00000400l) ビットを設定して DXVA をサポートしていることを示す必要があります。そうしないと、Direct3D ランタイムは[**createvideoprocessor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_createvideoprocessor)を呼び出すことができません。DXVA デバイスを作成する関数。 D3DCAPS9 構造体については、DirectX 9.0 SDK のドキュメントを参照してください。 この*ドライバーは、GETD3D9CAPS パラメーターが*指す[**D3DDDIARG\_getcaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)構造体の**型**メンバーで D3DDDICAPS\_値が設定されている[**getcaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)関数の呼び出しに応答して、D3DCAPS3\_DXVAHD ビットを設定します。

-   DXVAHD\_SURFACE\_TYPE\_VIDEO\_入力\_、アプリケーションレベルの DXVAHD\_SURFACE\_型列挙型のプライベート値に対応する DDI 値がありません。 アプリケーションでは、CPU またはシェーダーベースのビデオプロセッサプラグインに対して異なる形式で割り当てられているスクリーン以外のプレーンサーフェスに対して、ビデオ\_入力の種類\_VIDEO INPUT\_DXVAHD\_SURFACE\_設定します。

-   DXVAHD\_SURFACE\_TYPE\_VIDEO\_アプリケーションレベルの DXVAHD\_SURFACE の出力値は、D3DDDI の**VideoProcessRenderTarget**ビットフィールドフラグに対応し\_[ **_ RESOURCEFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_resourceflags)構造体。\_ Direct3D ランタイムは、ビデオ処理を作成するために、ランタイムがドライバーの[**createresource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)関数を呼び出したときに、 [**D3DDDIARG\_createresource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)構造体の**Flags**メンバーに**VideoProcessRenderTarget**を設定します。レンダーターゲット。

-   Direct3D ランタイムは、ビットブロック転送 (bitblt) とストリーム状態の両方を保持します。 ランタイムは、ランタイムに対してクエリを実行すると、アプリケーションに戻ります。

-   アプリケーションレベルの**IDXVAHD\_VideoProcessor:: GetVideoProcessBltState**メソッドに対応する DDI 関数がありません。 ただし、アプリケーションが**IDXVAHD\_videoprocessor:: GetVideoProcessBltState**を呼び出してビデオプロセッサのプライベート bitblt 状態データを取得する場合、Direct3D ランタイムはドライバーの[**Getvideoprocessbltstateprivate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_getvideoprocessbltstateprivate)を呼び出します。プロシージャ.

-   アプリケーションレベルの**IDXVAHD\_VideoProcessor:: GetVideoProcessStreamState**メソッドに対応する DDI 関数がありません。 ただし、アプリケーションが**IDXVAHD\_videoprocessor:: GetVideoProcessBltState**を呼び出してビデオプロセッサのプライベートストリームの状態データを取得する場合、Direct3D ランタイムはドライバーの[**Getvideoprocessstreamstateprivate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_getvideoprocessstreamstateprivate)を呼び出します。プロシージャ.

-   アプリケーションレベルの DXVAHD\_ストリーム\_状態列挙の DXVAHD\_STREAM\_STATE\_D3DFORMAT 値には、 [**DXVAHDDDI\_STREAM\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_dxvahdddi_stream_state)列挙に対応する DDI 値がありません。 ビデオプロセッサプラグインでは、DXVAHD\_SURFACE で割り当てられたサーフェイスに対して、DXVAHD\_STREAM\_STATE\_D3DFORMAT 値を使用して\_ビデオ\_入力\_アプリケーションレベルの DXVAHD\_SURFACE\_型の列挙体。\_

-   DXVAHD\_デバイス\_TYPE 列挙に対応する DDI 列挙がありません (たとえば、DXVAHDDDI\_デバイス\_種類はありません)。 [**DXVAHDDDI\_VPDEVCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_vpdevcaps)構造体の最初のメンバーは予約されていますが、アプリケーションレベルの DXVAHD\_vpdevcaps 構造体の最初のメンバーは、 **(devicetype**で DXVAHD\_デバイス\_型の値に設定されています。レプリカ. **(Devicetype**メンバーは、ランタイムまたはビデオプロセッサプラグインによって設定されます。このプラグインは、常にドライバーを DXVAHD\_デバイス\_種類\_ハードウェアとして報告します。

-   [**DXVAHDDDI\_FILTER\_RANGE\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_filter_range_data)構造体の**乗数**メンバーは、浮動小数点値です。 ドライバーは、底2の分数として正確に表すことができる値を使用する必要があります。 たとえば、0.25 はベース2の端数として正確に表すことができますが、0.1 はできません。

-   [DXVA-HD DDI](dxva-hd-ddi.md)関数は、S\_OK、e\_invalidarg、または e\_OUTOFMEMORY を返す必要があります。

 

 





