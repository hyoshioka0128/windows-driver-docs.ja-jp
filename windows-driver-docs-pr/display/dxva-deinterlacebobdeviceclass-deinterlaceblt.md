---
title: DXVA\_DeinterlaceBobDeviceClass DeinterlaceBlt メソッド
description: サンプル関数を実行する DeinterlaceBlt インター レースを解除または変換先の画面に出力を記述することでフレーム レート変換します。
ms.assetid: 0aa68d0c-8c2b-41fe-9e46-a41b157fbd98
keywords:
- ディスプレイ デバイスの DeinterlaceBlt メソッド
- DeinterlaceBlt メソッド ディスプレイ デバイス、DXVA_DeinterlaceBobDeviceClass インターフェイス
- DXVA_DeinterlaceBobDeviceClass は、DeinterlaceBlt メソッドのディスプレイ デバイスをインターフェイスします。
topic_type:
- apiref
api_name:
- DXVA_DeinterlaceBobDeviceClass.DeinterlaceBlt
api_type:
- COM
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: ba69f86e410be7b0358903eb8408a1e5d6441f5d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375850"
---
# <a name="dxvadeinterlacebobdeviceclassdeinterlaceblt-method"></a>DXVA\_DeinterlaceBobDeviceClass::DeinterlaceBlt メソッド


サンプル*DeinterlaceBlt*の動作にインター レースを解除または変換先の画面に出力を記述することでフレーム レート変換します。

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

*rtTargetFrame* \[で\]入力フレームのシーケンス内で [出力] フレームの場所を識別します。 デインター レースが実行されるだけの場合、ターゲットの時間に一致させてくださいいずれか、表示の開始時刻の参照の例で定義されている、 [ **DXVA\_VideoSample** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videosample)構造体、または開始の表示時刻と終了の表示時間の中間点。 詳細については、次を参照してください。、 [ **DXVA\_DeinterlaceBlt** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlaceblt)構造体。

フレーム レートの変換が要求された場合、 **rtTarget**時間のいずれかとは異なる場合、 **rtStart**参照サンプルの時間。

*lprcDstRect* \[で\]へのポインターを提供する[ **RECT** ](https://docs.microsoft.com/windows/desktop/api/windef/ns-windef-tagrect)左上隅を示し、先に四角形の適切なポイントを削減する構造体画面。 これらのポイントの領域を定義するビット ブロック転送を実行して、宛先表面上での位置。

*lpDDSDstSurface* \[で\]宛先表面へのポインターを提供します。 転送先のサーフェスは、D3D レンダリング ターゲットや D3D テクスチャでは、レンダー ターゲットになっている D3D テクスチャを指定できます。 宛先表面は常にローカルのビデオ メモリに割り当てられます。

転送先のサーフェイスのピクセル形式で示されているは、 [ **DXVA\_DeinterlaceCaps** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlacecaps)構造の一部として、YUV から RGB 色空間変換が実行される場合を除き、プロシージャ インター レースを解除します。 この場合、宛先表面形式は少なくとも 8 ビットの各色コンポーネントの有効桁数で RGB 形式です。

*lprcSrcRect* \[で\]左をについて説明し、ソース画面上の四角形の適切なポイントを削減する RECT 構造体へのポインターを提供します。 これらのポイントは、ビット ブロック転送およびソース画面上の位置のソース データの領域を定義します。

*lpDDSrcSurfaces* \[で\]ビデオ ソース サンプルの配列へのポインターを提供します。

*dwNumSurfaces* \[で\]における surface の数を示す、 **lpDDSrcSurfaces**配列。

*fAlpha* \[で\]サーフェスのアルファ値を示します。 値 0.0F は、透過的な画面を示します。 値 1.0F は、非透過の画面を示します。

<a name="return-value"></a>戻り値
------------

0 を返します (S\_[ok] または DD\_OK) 成功した場合、それ以外の場合、エラー コードを返します。 参照してください*ddraw.h*エラー コードの完全な一覧についてはします。

<a name="remarks"></a>注釈
-------

*DeinterlaceBlt*関数のマップへの呼び出しに直接、 **RenderMoComp**のメンバー、 [ **DD\_MOTIONCOMPCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)構造体。 **RenderMoComp**メンバーが参照するディスプレイ ドライバーによって提供される関数を指す、 [ **DD\_RENDERMOCOMPDATA** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)構造体。 DD\_RENDERMOCOMPDATA 構造は次のように入力されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Member</th>
<th align="left">値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>dwNumBuffers</strong></p></td>
<td align="left"><p>指す配列内のエントリの数を示す<strong>lpBufferInfo</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpBufferInfo</strong></p></td>
<td align="left"><p>配列を指す<a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_ddmocompbufferinfo" data-raw-source="[&lt;strong&gt;DDMOCOMPBUFFERINFO&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_ddmocompbufferinfo)"> <strong>DDMOCOMPBUFFERINFO</strong> </a>構造体のいずれかのサンプルを参照し、コピー先のサンプルの 1 つは、各入力します。 コピー先のサンプルは、配列の最初の要素です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dwFunction</strong></p></td>
<td align="left"><p>示す、 <strong>DXVA_DeinterlaceBltFnCode</strong>で定義された定数<em>dxva.h</em>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpInputData</strong></p></td>
<td align="left"><p>塗りつぶされたを指す<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlaceblt" data-raw-source="[&lt;strong&gt;DXVA_DeinterlaceBlt&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlaceblt)"> <strong>DXVA_DeinterlaceBlt</strong> </a>構造体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>lpOutputData</strong></p></td>
<td align="left"><p>設定<strong>NULL</strong>、現在使用されていません。</p></td>
</tr>
</tbody>
</table>

 

インター レースを解除するため、DirectX VA デバイスのドライバーが指定したコールバックが指す**RenderMoComp**はドライバーによって提供される表示を呼び出さずと呼ばれる**BeginMoCompFrame**または**EndMoCompFrame**関数。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**DD\_MOTIONCOMPCALLBACKS**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)

[**DD\_RENDERMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)

[**DXVA\_DeinterlaceBlt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlaceblt)

[**DXVA\_DeinterlaceCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlacecaps)

[**DXVA\_VideoSample**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videosample)

 

 






