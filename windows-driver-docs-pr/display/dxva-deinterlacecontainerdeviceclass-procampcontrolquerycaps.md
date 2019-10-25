---
title: ProcAmpControlQueryCaps メソッド
description: Sample DXVA\_DeinterlaceContainerDeviceClass::P rocAmpControlQueryCaps 関数を使用すると、VMR はドライバーに対してクエリを実行し、ProcAmp コントロールデバイスの入力要件とサポートされている追加のビデオ処理操作を決定することができます.
ms.assetid: e89f9a01-e8b3-4311-ad3b-296021c9795e
keywords:
- ProcAmpControlQueryCaps メソッドの表示デバイス
- ProcAmpControlQueryCaps メソッドの表示デバイス, DXVA_DeinterlaceContainerDeviceClass インターフェイス
- DXVA_DeinterlaceContainerDeviceClass インターフェイス表示デバイス, ProcAmpControlQueryCaps メソッド
topic_type:
- apiref
api_name:
- DXVA_DeinterlaceContainerDeviceClass.ProcAmpControlQueryCaps
api_location:
- N/A
api_type:
- COM
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 9daafd95a48c6f312b6871ad90749075a14840c8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839716"
---
# <a name="dxva_deinterlacecontainerdeviceclassprocampcontrolquerycaps-method"></a>DXVA\_DeinterlaceContainerDeviceClass::P rocAmpControlQueryCaps メソッド


Sample *ProcAmpControlQueryCaps*関数を使用すると、 *VMR*はドライバーにクエリを実行し、ProcAmp コントロールデバイスの入力要件とサポートされている追加のビデオ処理操作を確認できます。 クエリは、ProcAmp 調整操作の実行時に同時に発生することがあります。

<a name="syntax"></a>構文
------

```cpp
HRESULT ProcAmpControlQueryCaps(
  [in]  DXVA_VideoDesc          *lpVideoDescription,
  [out] DXVA_ProcAmpControlCaps *lpProcAmpCaps
);
```

<a name="parameters"></a>パラメーター
----------

\] の*Lpvideodescription* \[は、処理するビデオの ProcAmp コントロールパラメーターを定義する[**DXVA\_videodesc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc)構造体へのポインターを提供します。

*lpProcAmpCaps* \[out\] は、ProcAmp コントロール操作のドライバー機能を含む[**DXVA\_ProcAmpControlCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_procampcontrolcaps)構造体へのポインターを受け取ります。

<a name="return-value"></a>戻り値
------------

成功した場合は 0 (S\_OK または DD\_OK) を返します。それ以外の場合は、エラーコードを返します。 エラーコードの完全な一覧については、 *ddraw*を参照してください。

<a name="remarks"></a>注釈
-------

ドライバーは、 *lpProcAmpCaps*が指す[**DXVA\_ProcAmpControlCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_procampcontrolcaps)構造の ProcAmp コントロールモードのユーザーモードコンポーネントに機能を報告します。

Sample *ProcAmpControlQueryCaps*関数は、 [**DD\_MOTIONCOMPコールバック**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)構造の**rendermocomp**メンバーへの呼び出しに直接マップされます。 **Rendermocomp**関数は、 [**DD\_RENDERMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)構造体を参照する、ドライバーが提供する*ddmocomprender*コールバックを指します。 DD\_RENDERMOCOMPDATA 構造体は、次のように入力されます。

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
<td align="left"><p>回</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpBufferInfo</strong></p></td>
<td align="left"><p>NULL</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dwFunction</strong></p></td>
<td align="left"><p><strong>DXVA_ProcAmpControlQueryCapsFnCode</strong>定数 ( <em>DXVA</em>で定義)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpInputData</strong></p></td>
<td align="left"><p>塗りつぶされた<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc" data-raw-source="[&lt;strong&gt;DXVA_VideoDesc&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc)"><strong>DXVA_VideoDesc</strong></a>構造体へのポインター。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>lpOutputData</strong></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_procampcontrolcaps" data-raw-source="[&lt;strong&gt;DXVA_ProcAmpControlCaps&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_procampcontrolcaps)"><strong>DXVA_ProcAmpControlCaps</strong></a>構造体へのポインター。</p></td>
</tr>
</tbody>
</table>

 

RenderMoComp 関数は、ディスプレイドライバーが提供する BeginMoCompFrame または EndMoCompFrame 関数が最初に呼び出されずに呼び出されることに注意してください。

**コード例**

次のコードは、 *ProcAmpControlQueryCaps*関数を実装する方法の例を示しています。

```cpp
HRESULT
DXVA_DeinterlaceContainerDeviceClass::ProcAmpControlQueryCaps(
    LPDXVA_VideoDesc lpVideoDesc,
    LPDXVA_ProcAmpControlCaps lpProcAmpControlCaps
    )
{
    // only the YUY2 and YV12 formats can be operated on
    if (lpVideoDesc->d3dFormat != '2YUY' &&
        lpVideoDesc->d3dFormat != '21VY') {
        return E_INVALIDARG;
    }
    lpProcAmpControlCaps->InputPool = D3DPOOL_DEFAULT;
    lpProcAmpControlCaps->d3dOutputFormat = lpVideoDesc->d3dFormat;
    lpProcAmpControlCaps->ProcAmpControlProps =
        DXVA_ProcAmp_Brightness |
        DXVA_ProcAmp_Contrast |
        DXVA_ProcAmp_Hue |
        DXVA_ProcAmp_Saturation;
    lpProcAmpControlCaps->VideoProcessingCaps = DXVA_VideoProcess_None;
    return S_OK;
}
```

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
<td align="left"><p>Header</p></td>
<td align="left">N/A (ドライバーによって指定されたヘッダーファイルで宣言されています。)</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**DXVA\_VideoDesc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc)

[**DXVA\_ProcAmpControlCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_procampcontrolcaps)

[**DD\_MOTIONCOMPCALLBACKS バック**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)

[**DD\_RENDERMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)

 

 






