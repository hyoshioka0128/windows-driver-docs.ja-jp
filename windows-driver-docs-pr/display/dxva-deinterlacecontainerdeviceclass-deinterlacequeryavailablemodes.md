---
title: DeinterlaceQueryAvailableModes メソッド
description: Sample DXVA\_DeinterlaceContainerDeviceClass::D einterlaceQueryAvailableModes 関数は、特定の入力ビデオ形式の使用可能なノンインターレースモードまたはフレームレート変換モードを照会します。
ms.assetid: be721bde-3c72-4942-9f33-5ea1bf2d187c
keywords:
- DeinterlaceQueryAvailableModes メソッドの表示デバイス
- DeinterlaceQueryAvailableModes メソッドの表示デバイス, DXVA_DeinterlaceContainerDeviceClass インターフェイス
- DXVA_DeinterlaceContainerDeviceClass インターフェイス表示デバイス, DeinterlaceQueryAvailableModes メソッド
topic_type:
- apiref
api_name:
- DXVA_DeinterlaceContainerDeviceClass.DeinterlaceQueryAvailableModes
api_type:
- COM
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 8895b478bb0d9fa2ae44f6f6beab0dc0489e299a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839721"
---
# <a name="dxva_deinterlacecontainerdeviceclassdeinterlacequeryavailablemodes-method"></a>DXVA\_DeinterlaceContainerDeviceClass::D einterlaceQueryAvailableModes メソッド


Sample *DeinterlaceQueryAvailableModes*関数は、特定の入力ビデオ形式の使用可能なノンインターレースモードまたはフレームレート変換モードを照会します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
HRESULT DeinterlaceQueryAvailableModes(
  [in]      LPDXVA_VideoDesc lpVideoDescription,
  [in, out] LPDWORD          lpdwNumModesSupported,
  [in, out] LPGUID           pGuidsDeinterlaceModes
);
```

<a name="parameters"></a>パラメーター
----------

\] の*Lpvideodescription* \[は、インターレース解除やフレームレート変換を実行するためのビデオストリームの説明を含む[**DXVA\_videodesc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc)構造体へのポインターを提供します。

*lpdwNumModesSupported* \[in、out\] は、配列内の*pGuidsDeinterlaceModes*に返されるインターレース解除モードまたはフレームレート変換モードの数へのポインターを受け取ります。

*pGuidsDeinterlaceModes* \[in、out\] は、ドライバーでサポートされているノンインターレースモードまたはフレームレート変換モードを表す guid の配列へのポインターを受け取ります。

<a name="return-value"></a>戻り値
------------

成功した場合は 0 (S\_OK または DD\_OK) を返します。それ以外の場合は、エラーコードを返します。 エラーコードの完全な一覧については、 *ddraw*を参照してください。

<a name="remarks"></a>注釈
-------

*Lpvideodescription*パラメーターをドライバーに渡して、ドライバーがソースビデオの解像度と形式をサポートできるようにします。 たとえば、ドライバーは480i コンテンツの3つのフィールドのアダプティブインターレースを実行できる場合がありますが、ボブのコンテンツしか使用できない可能性があります。 詳細については、「[ノンインターレースとフレームレート変換のビデオコンテンツ](https://docs.microsoft.com/windows-hardware/drivers/display/video-content-for-deinterlace-and-frame-rate-conversion)」を参照してください。

*PGuidsDeinterlaceModes*パラメーターによって返される guid は、品質の高い順序で返される必要があります (つまり、返された guid 配列の最初の要素が最高品質モードで占有される必要があります)。

すべてのドライバーは、既存の*ビットブロック転送*(blt) ハードウェアを使用して、bob モードをサポートできる必要があります。 モードの詳細については、「[ノンインターレースモード](https://docs.microsoft.com/windows-hardware/drivers/display/deinterlace-modes)」と「[フレームレート変換モード](https://docs.microsoft.com/windows-hardware/drivers/display/frame-rate-conversion-modes)」のトピックを参照してください。

ドライバーは、 *VMR*からの要求に応答して、サポートされている guid (モード) を返します。 ドライバーは、 [*Ddmocomprender*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)コールバック関数の呼び出しに応答します。 このドライバーは、 *Ddmocomprender*ポイントの*lpRenderData*パラメーターが指定されている[**DD\_rendermocompdata**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)構造体の**Lpoutputdata**メンバーを介して、guid を返します。 **Lpoutputdata**メンバーは、 **Guid**メンバーの guid の配列を含む[**DXVA\_DeinterlaceQueryAvailableModes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacequeryavailablemodes)構造体を指します。

**RenderMoComp から DeinterlaceQueryAvailableModes へのマッピング**

Sample *DeinterlaceQueryAvailableModes*関数は、 [**DD\_MOTIONCOMPコールバック**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)構造の**rendermocomp**メンバーへの呼び出しに直接マップされます。 **Rendermocomp**メンバーは、 [**DD\_RENDERMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)構造体を参照するディスプレイドライバーが提供する関数を指します。

**Rendermocomp**コールバックは、ディスプレイドライバーが提供する**beginmocompframe**または**endmocompframe**関数が最初に呼び出されずに呼び出されます。

DD\_RENDERMOCOMPDATA 構造体は、次のように入力されます。

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
<td align="left"><p>回.</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpBufferInfo</strong></p></td>
<td align="left"><p>NULL:</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dwFunction</strong></p></td>
<td align="left"><p><strong>DXVA_DeinterlaceQueryAvailableModesFnCode</strong>定数 ( <em>DXVA</em>で定義されています)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpInputData</strong></p></td>
<td align="left"><p>塗りつぶされた<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc" data-raw-source="[&lt;strong&gt;DXVA_VideoDesc&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc)"><strong>DXVA_VideoDesc</strong></a>構造体へのポインター。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>lpOutputData</strong></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacequeryavailablemodes" data-raw-source="[&lt;strong&gt;DXVA_DeinterlaceQueryAvailableModes&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacequeryavailablemodes)"><strong>DXVA_DeinterlaceQueryAvailableModes</strong></a>構造体へのポインター。</p></td>
</tr>
</tbody>
</table>

 

*VMR*によって、特定のビデオ形式で使用可能なノンインターレースモードまたはフレーム変換モードが決定された後、VMR はドライバーにクエリを実行し、特定のノンインターレースモードとその他の入力要件に関する詳細情報を取得します。そのモードでサポートされている可能性のあるビデオ処理。 ドライバーは、 [**DeinterlaceQueryModeCaps**](dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps.md)関数の呼び出しからこの情報を返します。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**DD\_MOTIONCOMPCALLBACKS バック**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)

[**DD\_RENDERMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)

[**DeinterlaceQueryModeCaps**](dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps.md)

[**DXVA\_VideoDesc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc)

[**DXVA\_SampleFormat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ne-dxva-_dxva_sampleformat)

 

 






