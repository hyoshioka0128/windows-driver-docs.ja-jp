---
title: DXVA\_DeinterlaceBobDeviceClass DeinterlaceBltEx メソッド
description: サンプル関数を実行する DeinterlaceBltEx インター レースを解除またはフレーム レートの変換を組み合わせて、deinterlaced またはフレーム レート変換に指定されたビデオのビデオ、substreams し、宛先表面に、結合した出力を書き込みます。
ms.assetid: 12a0e467-54f8-4cca-8ec0-aa8d04480ab6
keywords:
- ディスプレイ デバイスの DeinterlaceBltEx メソッド
- DeinterlaceBltEx メソッド ディスプレイ デバイス、DXVA_DeinterlaceBobDeviceClass インターフェイス
- DXVA_DeinterlaceBobDeviceClass は、DeinterlaceBltEx メソッドのディスプレイ デバイスをインターフェイスします。
topic_type:
- apiref
api_name:
- DXVA_DeinterlaceBobDeviceClass.DeinterlaceBltEx
api_type:
- COM
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5cc83d33b73421403ec92590d94028a69ed4dd96
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375848"
---
# <a name="dxvadeinterlacebobdeviceclassdeinterlacebltex-method"></a>DXVA\_DeinterlaceBobDeviceClass::DeinterlaceBltEx メソッド


サンプル**DeinterlaceBltEx**関数実行フレーム レート変換に指定されたビデオのビデオのインター レースを解除またはフレーム レート変換の場合は、結合、deinterlaced substreams、および変換先に、結合した出力を書き込みます画面。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
HRESULT DeinterlaceBltEx(
  [in] REFERENCE_TIME      rtTargetFrame,
  [in] LPRECT              lprcTargetRect,
  [in] DXVA_AYUVsample2    BackgroundColor,
  [in] DWORD               dwDestinationFormat,
  [in] DWORD               dwDestinationFlags,
  [in] LPDDSURFACE         lpDDSDstSurface,
  [in] LPDXVA_VideoSample2 lpDDSrcSurfaces,
  [in] DWORD               dwNumSurfaces,
  [in] FLOAT               fAlpha
);
```

<a name="parameters"></a>パラメーター
----------

*rtTargetFrame* \[で\]入力フレームのシーケンス内で [出力] フレームの場所を提供します。 いずれかのターゲット時間が一致する必要があります、純粋なデインター レースを実行する場合、 **rtStart**回、中間の回 (つまり、(**rtStart**+**rtEnd**)/2) のサンプルについてで定義されている、 [ **DXVA\_VideoSample2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videosample2)構造体。

フレーム レート変換が要求された場合、 *rtTargetFrame*時間は、のいずれかに異なる可能性があります、 **rtStart**時間またはサンプルの中間時間。

*lprcTargetRect* \[で\]へのポインターを提供する[ **RECT** ](https://docs.microsoft.com/windows/desktop/api/windef/ns-windef-tagrect)どのに宛先表面内の場所を記述する構造体**DeinterlaceBltEx**記述する必要があります。 ドライバーを使用して*lprcTargetRect*を書き込むピクセルを判断します。 出力イメージがある四角形内のピクセルに制限されていることに注意してください。 *lprcTargetRect*します。 すべてのピクセルの四角形内では、 *lprcTargetRect* 、記述する必要がありますに四角形の外側のピクセル*lprcTargetRect*は変更しないでください。

*BackgroundColor* \[で\]装置、 [ **DXVA\_AYUVsample2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_ayuvsample2)背景の色と不透明度のレベルを識別する構造体なる、すべてのビデオ ストリームとサブストリームがで構成されます。 Microsoft Windows Server 2003 SP1 と Windows XP SP2 では、不透明度は使用されませんし、ドライバーによって無視する必要があります。

*dwDestinationFormat* \[で\]書式にあるポインターで指定されている宛先表面の情報を提供*lpDDSDstSurface*します。 Windows Server 2003 SP1 および Windows XP SP2 では、このパラメーターは 0 に設定します。

*dwDestinationFlags* \[で\]前の変換先の画面から現在の変換先の画面での変更を示すフラグのコレクションを提供します。 このパラメーターは内のフラグの 1 つ以上のビットごとの OR、 [ **DXVA\_DestinationFlags** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ne-dxva-_dxva_destinationflags)列挙型。 これらのフラグは、ドライバーのコードを最適化するために使用できます。 つまり、コードでは、前の変換先の画面から変更が発生していない場合は、現在の変換先の画面で操作を実行する必要はありません。

*lpDDSDstSurface* \[で\]宛先表面へのポインターを提供します。 転送先のサーフェイスは、ビデオ メモリ内にある、プレーン オフスクリーン サーフェイスです。 転送先のサーフェイスのピクセル形式がで指定された、 **d3dOutputFormat**のメンバー、 [ **DXVA\_DeinterlaceCaps** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlacecaps)構造体。 YUV の色空間のピクセル形式があります。

*lpDDSrcSurfaces* \[で\]DXVA の配列へのポインターを提供\_ビデオ ソースを記述する VideoSample2 構造体のサンプルを参照およびサブストリームのビット ブロック転送に必要なサンプル.

*dwNumSurfaces* \[で\]サンプルの数を提供、 *lpDDSrcSurfaces*配列。

*fAlpha* \[で\]出力の宛先表面イメージには、背景色、ビデオ ストリーム、およびビデオ サブストリームのコンポジットです、ドライバーが適用される平面透明度の値を提供します。 Windows Server 2003 SP1 および Windows XP SP2 では、この値は常に 1.0 f は、イメージ全体が不透明であると、全体的なイメージのアルファ ブレンドが不要であることを示します。

<a name="return-value"></a>戻り値
------------

0 を返します (S\_[ok] または DD\_OK) 成功した場合、それ以外の場合、エラー コードを返します。 参照してください*ddraw.h*エラー コードの完全な一覧についてはします。

<a name="remarks"></a>注釈
-------

**DeinterlaceBltEx**フレーム レートのビデオの変換または関数は、インターまたはフレーム レート変換操作を実行し、deinterlaced と指定されたビデオ サブストリームを同時に結合します。 **DeinterlaceBltEx**関数は、移行先の画面に出力に書き込みます。 なお**DeinterlaceBltEx**ノンインター レース化操作をする必要があります、ドライバーの場合に実行しない、プログレッシブ ビデオ サンプルを使用して呼び出すことができます。 ドライバーのビデオに指定されたビデオ サブストリームを組み合わせるし、で示されている各ストリームに変換する必要があります、 *lprcTargetRect*と*BackgroundColor*パラメーターおよび**rcSrc**と**rcDst**のメンバー、 [ **DXVA\_VideoSample2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videosample2)で渡される配列内の構造体、 *pDDSrcSurfaces*パラメーター。

プログレッシブ ビデオに複数の参照ストリームを必要とするインター モードを使用する場合、複数のフレームは、それらのフレームに出力を生成するために必要ない場合でもにドライバーにも送信します。 詳細については、例 5 を参照してください。[入力バッファー順序](https://docs.microsoft.com/windows-hardware/drivers/display/input-buffer-order)します。

渡される配列内の参照のビデオ サンプルについては、 *pDDSrcSurfaces*パラメーター、 **rtStart**と**rtEnd** 、DXVA のメンバー\_VideoSample2 の構造体のサンプルについては、サンプルの一時的な場所を示します。 配列で、各ビデオ サブストリーム サンプルについては、 **rtStart**と**rtEnd** 、DXVA のメンバー\_VideoSample2 構造の各サンプルは、0 にクリアされます。

ビデオ サブストリームのみ AI44、IA44、AYUV と*FOURCC*ドライバーするピクセル形式を指定することができます。 詳細については、次を参照してください。 [Supplying ビデオ サブストリームと宛先表面](https://docs.microsoft.com/windows-hardware/drivers/display/supplying-video-substream-and-destination-surfaces)します。

パレット ピクセル形式のビデオ サブストリーム、用、**パレット**のメンバー、 [ **DXVA\_VideoSample2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videosample2)構造に各ビデオ サブストリームが含まれています、ドライバーがときに使用する 16 のパレット エントリの配列合成サブストリーム サンプル。 Nonpalletized ピクセル形式の場合、パレット エントリは 0 がクリアされ、無視することができます。

**SampleFlags**のメンバー、 [ **DXVA\_VideoSample2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videosample2)構造に各入力のサンプルには、変更を示すフラグのコレクションが含まれています、前のサンプルから現在のサンプルです。 フラグには、パレット、色データ、元の四角形、およびサンプルのコピー先の四角形に変更が反映されます。 これらのフラグは、ドライバーのコードを最適化するために使用できます。 つまり、コードでは、前のサンプルのフレームからの変更が発生していない場合は、サンプルの現在のフレームの操作を実行する必要はありません。

*DwNumSurfaces*パラメーター内の要素の数を示す、 *lpDDSrcSurface*配列。 ビデオのリファレンス サンプルは、配列内の順に Z オーダーでビデオ サブストリームをします。 詳細については、次を参照してください。[入力バッファー順序](https://docs.microsoft.com/windows-hardware/drivers/display/input-buffer-order)します。 ドライバーを受信するビデオのサブストリームの数の範囲は 0 から 15 です。 ときに**DeinterlaceBltEx**が呼び出されると、ドライバーは通常受信ビデオ サブストリームを 0 または 1。 ただし、ドライバーは、複数のビデオ サブストリームを処理できるように実装する必要があります。

**DeinterlaceBltEx**関数のマップへの呼び出しに直接、 **RenderMoComp**のメンバー、 [ **DD\_MOTIONCOMPCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)構造体。 **RenderMoComp**メンバーが参照するディスプレイ ドライバーによって提供される関数を指す、 [ **DD\_RENDERMOCOMPDATA** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)構造体。 DD\_RENDERMOCOMPDATA 構造は次のように入力されます。

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
<td align="left"><p>指す配列内のエントリの数を示す<strong>lpBufferInfo</strong>します。 1 を足したソース サンプルの数です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpBufferInfo</strong></p></td>
<td align="left"><p>配列を指す<a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_ddmocompbufferinfo" data-raw-source="[&lt;strong&gt;DDMOCOMPBUFFERINFO&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_ddmocompbufferinfo)"> <strong>DDMOCOMPBUFFERINFO</strong> </a>構造体、1 つのソースのサンプルを参照またはサブストリームのサンプルとコピー先のサンプルの 1 つは、各入力します。 コピー先のサンプルは、配列の最初の要素です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dwFunction</strong></p></td>
<td align="left"><p>示す、 <strong>DXVA_DeinterlaceBltExFnCode</strong>で定義された定数<em>dxva.h</em>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpInputData</strong></p></td>
<td align="left"><p>塗りつぶされたを指す<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlacebltex" data-raw-source="[&lt;strong&gt;DXVA_DeinterlaceBltEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlacebltex)"> <strong>DXVA_DeinterlaceBltEx</strong> </a>構造体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>lpOutputData</strong></p></td>
<td align="left"><p>設定<strong>NULL</strong>、現在使用されていません。</p></td>
</tr>
</tbody>
</table>

 

インター レースを解除するため、DirectX VA デバイスのドライバーが指定したコールバックが指す**RenderMoComp**はドライバーによって提供される表示を呼び出さずと呼ばれる**BeginMoCompFrame**または**EndMoCompFrame**関数。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>対象プラットフォーム</p></td>
<td align="left">Desktop</td>
</tr>
<tr class="even">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>バージョン: Windows Server 2003 SP1 以降では Windows XP SP2 および以降のバージョンのみ。</p></td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**DXVA\_AYUVsample2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_ayuvsample2)

[**DXVA\_DeinterlaceBltEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlacebltex)

[**DXVA\_DeinterlaceCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlacecaps)

[**DXVA\_DestinationFlags**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ne-dxva-_dxva_destinationflags)

[**DXVA\_VideoSample2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videosample2)

[**DDMOCOMPBUFFERINFO**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_ddmocompbufferinfo)

[**DD\_MOTIONCOMPCALLBACKS**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)

[**DD\_RENDERMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)

 

 






