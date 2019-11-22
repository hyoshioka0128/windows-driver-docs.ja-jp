---
title: DXVA\_DeinterlaceBobDeviceClass DeinterlaceBltEx メソッド
description: Sample DeinterlaceBltEx 関数は、インターレース解除またはフレームレート変換を実行し、合成されたビデオまたはフレームレート変換されたビデオを提供されたビデオサブストリームと結合し、結合された出力をターゲットサーフェイスに書き込みます。
ms.assetid: 12a0e467-54f8-4cca-8ec0-aa8d04480ab6
keywords:
- DeinterlaceBltEx メソッドの表示デバイス
- DeinterlaceBltEx メソッドの表示デバイス、DXVA_DeinterlaceBobDeviceClass インターフェイス
- DXVA_DeinterlaceBobDeviceClass インターフェイス表示デバイス、DeinterlaceBltEx メソッド
topic_type:
- apiref
api_name:
- DXVA_DeinterlaceBobDeviceClass.DeinterlaceBltEx
api_type:
- COM
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: a3f01e8e3709612783616651999159b2ab8832a0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838969"
---
# <a name="dxva_deinterlacebobdeviceclassdeinterlacebltex-method"></a>DXVA\_DeinterlaceBobDeviceClass::D einterlaceBltEx メソッド


Sample **DeinterlaceBltEx**関数は、インターレース解除またはフレームレート変換を実行し、合成されたビデオまたはフレームレート変換されたビデオを提供されたビデオサブストリームと結合し、結合された出力をターゲットサーフェイスに書き込みます。

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

\] の*Rttargetframe* \[は、入力フレームのシーケンス内の出力フレームの位置を提供します。 純粋なノンインターレースを実行する場合、 [**DXVA\_VideoSample2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videosample2)構造体で定義されているように、目標時間は、サンプルの**rtstart**時刻または中点時間 (つまり、(**rtstart**+**rtend**)/2) のいずれかと一致する必要があります.

フレームレート変換が要求された場合、 *Rttargetframe*の時間は、サンプルの**rtstart** times または中点の時間とは異なる場合があります。

\] の*lprcTargetRect* \[は、 **DeinterlaceBltEx**が書き込む必要があるターゲットサーフェイス内の場所を記述する[**RECT**](https://docs.microsoft.com/windows/desktop/api/windef/ns-windef-tagrect)構造体へのポインターを提供します。 ドライバーは*lprcTargetRect*を使用して、書き込み先のピクセルを決定します。 出力イメージは、 *lprcTargetRect*の四角形内のピクセルに制限されていることに注意してください。 つまり、 *lprcTargetRect*の四角形内のすべてのピクセルを書き込む必要があります。また、 *lprcTargetRect*で四角形の外側のピクセルを変更することはできません。

\] の*BackgroundColor* \[には、すべてのビデオストリームとサブストリームが構成されている背景の色と不透明度を識別する[**DXVA\_AYUVsample2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_ayuvsample2)構造体が用意されています。 Microsoft Windows Server 2003 SP1 および Windows XP SP2 では、不透明度レベルは使用されず、ドライバーによって無視される必要があります。

*Dwdestinationformat format*は、 *lpDDSDstSurface*のポインターに指定されている変換先サーフェスの形式情報を\] 提供します。\[ Windows Server 2003 SP1 および Windows XP SP2 の場合、このパラメーターは0に設定されます。

\] の*Dwdestinationflags* \[は、前のターゲットサーフェイスからの現在の移動先サーフェイスの変更を示すフラグのコレクションを提供します。 このパラメーターは、 [**DXVA\_DestinationFlags**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ne-dxva-_dxva_destinationflags)列挙型の1つ以上のフラグのビットごとの or です。 これらのフラグを使用して、ドライバーコードを最適化することができます。 つまり、前のターゲットサーフェイスから変更が行われていない場合、現在のターゲットサーフェイスに対する操作を実行するためにコードは必要ありません。

\] の*lpDDSDstSurface* \[は、ターゲットサーフェイスへのポインターを提供します。 移動先の画面は、ビデオメモリにあるオフスクリーンのプレーンな表面です。 ターゲットサーフェスのピクセル形式は、 [**DXVA\_DeinterlaceCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacecaps)構造体の**d3dOutputFormat**メンバーに指定されます。 ピクセル形式は、YUV 色空間にある必要があります。

\] の*lpDDSrcSurfaces* \[は、ビットブロック転送に必要なビデオソース参照サンプルとサブストリームサンプルを記述する DXVA\_VideoSample2 構造体の配列へのポインターを提供します。

*Dwnumsurfaces* \[\] では、 *lpDDSrcSurfaces*配列内のサンプルの数を指定します。

\] の*fAlpha* \[は、ドライバーが出力先のサーフェイスイメージに適用する平面透明度の値を提供します。これは、背景色、ビデオストリーム、およびビデオサブストリームの複合型です。 Windows Server 2003 SP1 および Windows XP SP2 では、この値は常に 1.0 F です。これは、全体のイメージが不透明であり、イメージ全体でアルファブレンドが不要であることを示します。

<a name="return-value"></a>戻り値
------------

成功した場合、0 (S\_OK または DD\_OK) を返します。それ以外の場合は、エラーコードを返します。 エラーコードの完全な一覧については、 *ddraw*を参照してください。

<a name="remarks"></a>注釈
-------

**DeinterlaceBltEx**関数は、インターレース解除またはフレームレート変換操作を実行し、指定されたビデオサブストリームと、変換されたインターレースまたはフレームレートのビデオを同時に結合します。 次に、 **DeinterlaceBltEx**関数は出力をターゲットサーフェスに書き込みます。 プログレッシブビデオサンプルで**DeinterlaceBltEx**を呼び出すことができることに注意してください。この場合、ドライバーはインターレース解除操作を実行できません。 ドライバーは、指定されたビデオサブストリームとビデオを結合し、 *lprcTargetRect*および*BackgroundColor*パラメーターで示されているように各ストリームを変換し、 [**DXVA\_VideoSample2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videosample2)構造体の**Rcsrc**および**rcdst**メンバーを*pddsrcsurfaces*パラメーターで渡される配列に変換します。

複数の参照ストリームを必要とするノンインターレースモードがプログレッシブビデオと共に使用されている場合でも、それらのフレームが出力を生成する必要がない場合でも、複数のフレームがドライバーに送信されます。 詳細については、「[入力バッファーの順序](https://docs.microsoft.com/windows-hardware/drivers/display/input-buffer-order)の例5」を参照してください。

*Pddsrcsurfaces*パラメーターで渡される配列内の参照ビデオサンプルの場合、サンプルの**Rtstart**と**rtend** DXVA VideoSample2 構造体のメンバーは、サンプルの一時的な場所を示します。\_ 配列内の各ビデオサブストリームのサンプルでは、各サンプルの**Rtstart**と**Rtend** DXVA の VideoSample2 構造体のメンバーが0にクリアされます。\_

ドライバーに指定できるのは、AI44、IA44、および AYUV *FOURCC*ピクセル形式のビデオサブストリームだけです。 詳細については、「[ビデオサブストリームとターゲットサーフェスの提供](https://docs.microsoft.com/windows-hardware/drivers/display/supplying-video-substream-and-destination-surfaces)」を参照してください。

パレットビデオサブストリームのピクセル形式の場合、各ビデオサブストリームの[**DXVA\_VideoSample2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videosample2)構造体の**パレット**メンバーには、サブストリームのサンプルを合成するときにドライバーが使用する16パレットのエントリの配列が含まれています。 Nonpalletized ピクセル形式の場合、パレットエントリはゼロにクリアされ、無視することができます。

各入力サンプルの[**DXVA\_VideoSample2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videosample2)構造体の**sampleflags**メンバーには、前のサンプルの現在のサンプルの変更を示すフラグのコレクションが含まれています。 フラグには、サンプルのパレット、色データ、ソース四角形、および変換先の四角形に加えられた変更が反映されます。 これらのフラグを使用して、ドライバーコードを最適化することができます。 つまり、前のサンプルフレームから変更が行われていない場合は、現在のサンプルフレームに対して操作を実行する必要はありません。

*Dwnumsurfaces*パラメーターは、 *lpDDSrcSurface*配列内の要素の数を示します。 ビデオ参照サンプルは配列の最初にあり、その後にビデオのサブストリームが Z オーダーで示されます。 詳細については、「[入力バッファーの順序](https://docs.microsoft.com/windows-hardware/drivers/display/input-buffer-order)」を参照してください。 ドライバーが受信するビデオサブストリームの数は、0 ~ 15 の範囲で指定できます。 **DeinterlaceBltEx**が呼び出されると、通常、ドライバーは0または1個のビデオサブストリームを受け取ります。 ただし、複数のビデオサブストリームを処理できるように、ドライバーを実装する必要があります。

**DeinterlaceBltEx**関数は、 [**DD\_MOTIONCOMPコールバック**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)構造の**rendermocomp**メンバーへの呼び出しに直接マップされます。 **Rendermocomp**メンバーは、 [**DD\_RENDERMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)構造体を参照するディスプレイドライバーが提供する関数を指します。 DD\_RENDERMOCOMPDATA 構造体は、次のように入力されます。

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
<td align="left"><p><strong>Lpbufferinfo</strong>が指す配列内のエントリの数を示します。 この数値は、ソースのサンプル数に1を加えた値です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpBufferInfo</strong></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_ddmocompbufferinfo" data-raw-source="[&lt;strong&gt;DDMOCOMPBUFFERINFO&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_ddmocompbufferinfo)"><strong>Ddmocompbufferinfo</strong></a>構造体の配列を指します。各入力参照ソースサンプルまたはサブストリームサンプルに1つ、および変換先サンプル用です。 コピー先のサンプルは、配列の最初の要素です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dwFunction</strong></p></td>
<td align="left"><p><em>DXVA</em>で定義されている<strong>DXVA_DeinterlaceBltExFnCode</strong>定数を示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpInputData</strong></p></td>
<td align="left"><p>塗りつぶされた<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacebltex" data-raw-source="[&lt;strong&gt;DXVA_DeinterlaceBltEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacebltex)"><strong>DXVA_DeinterlaceBltEx</strong></a>構造体を指します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>lpOutputData</strong></p></td>
<td align="left"><p>現在使用されていない<strong>NULL</strong>に設定します。</p></td>
</tr>
</tbody>
</table>

 

インターレース解除に使用する DirectX VA デバイスでは、 **Rendermocomp**によってポイントされたドライバーから提供されるコールバックは、ディスプレイドライバーが提供する**beginmocompframe**または**endmocompframe**関数を呼び出さずに呼び出されます。

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
<td align="left"><p>バージョン: Windows Server 2003 SP1 以降および Windows XP SP2 以降のバージョンのみ。</p></td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**DXVA\_AYUVsample2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_ayuvsample2)

[**DXVA\_DeinterlaceBltEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacebltex)

[**DXVA\_DeinterlaceCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacecaps)

[**DXVA\_DestinationFlags**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ne-dxva-_dxva_destinationflags)

[**DXVA\_VideoSample2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videosample2)

[**DDMOCOMPBUFFERINFO**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_ddmocompbufferinfo)

[**DD\_MOTIONCOMPCALLBACKS バック**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)

[**DD\_RENDERMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)

 

 






