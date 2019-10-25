---
title: DXVA\_DeinterlaceBobDeviceClass DeinterlaceBlt メソッド
description: Sample DeinterlaceBlt 関数は、出力をターゲットサーフェスに書き込むことによって、インターレース解除またはフレームレート変換を実行します。
ms.assetid: 0aa68d0c-8c2b-41fe-9e46-a41b157fbd98
keywords:
- DeinterlaceBlt メソッドの表示デバイス
- DeinterlaceBlt メソッドの表示デバイス, DXVA_DeinterlaceBobDeviceClass インターフェイス
- DXVA_DeinterlaceBobDeviceClass インターフェイス表示デバイス, DeinterlaceBlt メソッド
topic_type:
- apiref
api_name:
- DXVA_DeinterlaceBobDeviceClass.DeinterlaceBlt
api_type:
- COM
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: bbb0e3837f341ffc6e5c02b8708a771beb401547
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839719"
---
# <a name="dxva_deinterlacebobdeviceclassdeinterlaceblt-method"></a>DXVA\_DeinterlaceBobDeviceClass::D einterlaceBlt メソッド


Sample *DeinterlaceBlt*関数は、出力をターゲットサーフェスに書き込むことによって、インターレース解除またはフレームレート変換を実行します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
HRESULT DeinterlaceBlt(
  [in] REFERENCE_TIME     rtTargetFrame,
  [in] LPRECT             lprcDstRect,
  [in] LPDDSURFACE        lpDDSDstSurface,
  [in] LPRECT             lprcSrcRect,
  [in] LPDXVA_VideoSample lpDDSrcSurfaces,
  [in] DWORD              dwNumSurfaces,
  [in] FLOAT              fAlpha
);
```

<a name="parameters"></a>パラメーター
----------

\] の*Rttargetframe* \[は、入力フレームのシーケンス内の出力フレームの位置を識別します。 ノンインターレースのみを実行する場合は、 [**DXVA\_videosample**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videosample)構造体で定義されているように、ターゲット時間が参照サンプルの開始時の表示時間と同じであるか、開始時の表示時間と終了位置の間の中間点である必要があります。表示時間。 詳細については、「 [**DXVA\_DeinterlaceBlt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlaceblt)構造体」を参照してください。

フレームレート変換が要求された場合、 **Rttarget** time は、参照サンプルの**rttarget**時間とは異なる場合があります。

\] の*lprcDstRect* \[は、ターゲットサーフェイス上の四角形の左上および右下の点を記述する[**RECT**](https://docs.microsoft.com/windows/desktop/api/windef/ns-windef-tagrect)構造体へのポインターを提供します。 これらのポイントは、ビットブロック転送が発生する領域と、ターゲットサーフェイス上の位置を定義します。

\] の*lpDDSDstSurface* \[は、ターゲットサーフェイスへのポインターを提供します。 ターゲットサーフェイスは、D3D レンダーターゲット、D3D テクスチャ、またはレンダーターゲットでもある D3D テクスチャにすることができます。 ターゲットサーフェスは、常にローカルのビデオメモリに割り当てられます。

ターゲットサーフェスのピクセル形式は、 [**DXVA\_DeinterlaceCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacecaps)構造体に示されているものです。ただし、ノンインターレースの手順の一部として、YUV から RGB へのカラー空間変換が実行されている場合は除きます。 この場合、コピー先のサーフェス形式は RGB 形式で、各色コンポーネントに対して8ビット以上の精度が設定されています。

\] の*lprcSrcRect* \[は、ソースサーフェイス上の四角形の左上および右下の点を記述する RECT 構造体へのポインターを提供します。 これらのポイントは、ビットブロック転送のソースデータの領域とソースサーフェイス上の位置を定義します。

\] の*lpDDSrcSurfaces* \[は、ビデオソースのサンプルの配列へのポインターを提供します。

*Dwnumsurfaces* \[\] では、 **lpDDSrcSurfaces**配列内のサーフェイスの数を示します。

\] の*fAlpha* \[は、サーフェイスのアルファ値を示します。 値 0.0 F は透明なサーフェイスを示します。 値 1.0 F は不透明なサーフェイスを示します。

<a name="return-value"></a>戻り値
------------

成功した場合は 0 (S\_OK または DD\_OK) を返します。それ以外の場合は、エラーコードを返します。 エラーコードの完全な一覧については、 *ddraw*を参照してください。

<a name="remarks"></a>注釈
-------

*DeinterlaceBlt*関数は、 [**DD\_MOTIONCOMPコールバック**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)構造の**rendermocomp**メンバーへの呼び出しに直接マップされます。 **Rendermocomp**メンバーは、 [**DD\_RENDERMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)構造体を参照するディスプレイドライバーが提供する関数を指します。 DD\_RENDERMOCOMPDATA 構造体は、次のように入力されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">メンバー</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>dwNumBuffers</strong></p></td>
<td align="left"><p><strong>Lpbufferinfo</strong>が指す配列内のエントリの数を示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpBufferInfo</strong></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_ddmocompbufferinfo" data-raw-source="[&lt;strong&gt;DDMOCOMPBUFFERINFO&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_ddmocompbufferinfo)"><strong>Ddmocompbufferinfo</strong></a>構造体の配列を指します。入力参照サンプルごとに1つ、ターゲットサンプル用に1つです。 コピー先のサンプルは、配列の最初の要素です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dwFunction</strong></p></td>
<td align="left"><p><em>DXVA</em>で定義されている<strong>DXVA_DeinterlaceBltFnCode</strong>定数を示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpInputData</strong></p></td>
<td align="left"><p>塗りつぶされた<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlaceblt" data-raw-source="[&lt;strong&gt;DXVA_DeinterlaceBlt&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlaceblt)"><strong>DXVA_DeinterlaceBlt</strong></a>構造体を指します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>lpOutputData</strong></p></td>
<td align="left"><p>現在使用されていない<strong>NULL</strong>に設定します。</p></td>
</tr>
</tbody>
</table>

 

インターレース解除に使用する DirectX VA デバイスでは、 **Rendermocomp**によってポイントされたドライバーから提供されるコールバックは、ディスプレイドライバーが提供する**beginmocompframe**または**endmocompframe**関数を呼び出さずに呼び出されます。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**DD\_MOTIONCOMPCALLBACKS バック**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)

[**DD\_RENDERMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)

[**DXVA\_DeinterlaceBlt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlaceblt)

[**DXVA\_DeinterlaceCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacecaps)

[**DXVA\_VideoSample**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videosample)

 

 






