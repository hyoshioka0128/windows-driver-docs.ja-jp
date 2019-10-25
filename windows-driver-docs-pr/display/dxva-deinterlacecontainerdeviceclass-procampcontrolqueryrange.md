---
title: ProcAmpControlQueryRange メソッド
description: Sample DXVA\_DeinterlaceContainerDeviceClass::P rocAmpControlQueryRange 関数を使用すると、VMR はドライバーに対してクエリを実行し、各 ProcAmp プロパティの最小値、最大値、ステップサイズ、および既定値を確認できます。
ms.assetid: 13fd5d4b-f753-4a2c-80e0-c9614d7ebd3d
keywords:
- ProcAmpControlQueryRange メソッドの表示デバイス
- ProcAmpControlQueryRange メソッドの表示デバイス, DXVA_DeinterlaceContainerDeviceClass インターフェイス
- DXVA_DeinterlaceContainerDeviceClass インターフェイス表示デバイス, ProcAmpControlQueryRange メソッド
topic_type:
- apiref
api_name:
- DXVA_DeinterlaceContainerDeviceClass.ProcAmpControlQueryRange
api_location:
- N/A
api_type:
- COM
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 592cec315545cd788d3d7687c1acd144edefbd7a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838964"
---
# <a name="dxva_deinterlacecontainerdeviceclassprocampcontrolqueryrange-method"></a>DXVA\_DeinterlaceContainerDeviceClass::P rocAmpControlQueryRange メソッド


Sample **ProcAmpControlQueryRange**関数を使用すると、 *VMR*はドライバーに対してクエリを実行し、各 ProcAmp プロパティの最小値、最大値、ステップサイズ、および既定値を確認できます。

<a name="syntax"></a>構文
------

```cpp
HRESULT ProcAmpControlQueryRange(
  [in]  DWORD                   VideoProperty,
  [in]  DXVA_VideoDes           *lpVideoDescription,
  [out] DXVA_VideoPropertyRange *lpPropRange
);
```

<a name="parameters"></a>パラメーター
----------

\] の*videoproperty* \[は、ドライバーが情報を返す必要がある ProcAmp コントロールのプロパティを識別します。 このパラメーターに指定できる値は次のとおりです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DXVA_ProcAmp_Brightness</p></td>
<td align="left"><p>明るさの情報を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXVA_ProcAmp_Contrast</p></td>
<td align="left"><p>コントラスト情報を返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DXVA_ProcAmp_Hue</p></td>
<td align="left"><p>色合い情報を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXVA_ProcAmp_Saturation</p></td>
<td align="left"><p>鮮やかさの情報を返します。</p></td>
</tr>
</tbody>
</table>

 

\] の*Lpvideodescription* \[は、 [**DXVA\_videodesc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc)構造体へのポインターを提供します。 この構造体は、ProcAmp 調整が適用されるビデオの説明をドライバーに提供します。 ドライバーは、特定のビデオストリームの ProcAmp サポートを調整できます。

*Lpproprange* out\] は、ProcAmp の範囲、ステップサイズ、および既定値を指定する[**DXVA\_videopropertyrange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videopropertyrange)構造体へのポインターを受け取ります。

<a name="return-value"></a>戻り値
------------

成功した場合は 0 (S\_OK または DD\_OK) を返します。それ以外の場合は、エラーコード (たとえば、E\_NOTIMPL) を返します。 エラーコードの完全な一覧については、 *ddraw*を参照してください。

<a name="remarks"></a>注釈
-------

VMR は、ProcAmp プロパティごとに、ドライバーに対してクエリを実行し、最小値、最大値、ステップサイズ、および既定値を決定します。 ハードウェアが特定の ProcAmp コントロールプロパティをサポートしていない場合、ドライバーは**ProcAmpControlQueryRange**関数から E\_NOTIMPL を返します。

ProcAmp プロパティの詳細については、「 [ProcAmp properties](https://docs.microsoft.com/windows-hardware/drivers/display/procamp-properties)」を参照してください。

Sample **ProcAmpControlQueryRange**関数は、 [**DD\_MOTIONCOMPコールバック**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)構造の**rendermocomp**メンバーへの呼び出しに直接マップされます。 **Rendermocomp**メンバーは、 [**DD\_RENDERMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)構造体を参照する、ドライバーが提供する[**ddmocomprender**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)コールバックを指します。 DD\_RENDERMOCOMPDATA 構造体は、次のように入力されます。

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
<td align="left"><p>dwNumBuffers</p></td>
<td align="left"><p>回.</p></td>
</tr>
<tr class="even">
<td align="left"><p>lpBufferInfo</p></td>
<td align="left"><p>NULL:</p></td>
</tr>
<tr class="odd">
<td align="left"><p>dwFunction</p></td>
<td align="left"><p><strong>DXVA_ProcAmpControlQueryRangeFnCode</strong>定数 ( <em>DXVA</em>で定義されています)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>lpInputData</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_procampcontrolqueryrange" data-raw-source="[&lt;strong&gt;DXVA_ProcAmpControlQueryRange&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_procampcontrolqueryrange)"><strong>DXVA_ProcAmpControlQueryRange</strong></a>構造体へのポインター。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>lpOutputData</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videopropertyrange" data-raw-source="[&lt;strong&gt;DXVA_VideoPropertyRange&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videopropertyrange)"><strong>DXVA_VideoPropertyRange</strong></a>構造体へのポインター。</p></td>
</tr>
</tbody>
</table>

 

RenderMoComp 関数は、ディスプレイドライバーが提供する BeginMoCompFrame または EndMoCompFrame 関数が最初に呼び出されずに呼び出されることに注意してください。

**コード例**

次のコードは、 *ProcAmpControlQueryRange*関数を実装する方法の例を示しています。

```cpp
HRESULT
DXVA_DeinterlaceContainerDeviceClass::ProcAmpControlQueryRange(
    DWORD VideoProperty,
    LPDXVA_VideoDesc lpVideoDesc,
    DXVA_VideoPropertyRange* lpPropRange
    )
{
    // only the YUY2 and YV12 formats can be operated on
    if (lpVideoDesc->d3dFormat != '2YUY' &&
        lpVideoDesc->d3dFormat != '21VY') {
        return E_INVALIDARG;
    }
    // the following are the recommended settings for each property
    switch (VideoProperty) {
    case DXVA_ProcAmp_Brightness:
        lpPropRange->MinValue = -100.F;
        lpPropRange->MaxValue = 100.F;
        lpPropRange->DefaultValue = 0.0F;
        lpPropRange->StepSize = 0.1F;
        break;
    case DXVA_ProcAmp_Contrast:
        lpPropRange->MinValue = 0.F;
        lpPropRange->MaxValue = 10.F;
        lpPropRange->DefaultValue = 1.0F;
        lpPropRange->StepSize = 0.01F;
        break;
    case DXVA_ProcAmp_Hue:
        lpPropRange->MinValue = -180.0F;
        lpPropRange->MaxValue =  180.0F;
        lpPropRange->DefaultValue = 0.0F;
        lpPropRange->StepSize = 0.1F;
        break;
    case DXVA_ProcAmp_Saturation:
        lpPropRange->MinValue = 0.F;
        lpPropRange->MaxValue = 10.F;
        lpPropRange->DefaultValue = 1.0F;
        lpPropRange->StepSize = 0.01F;
        break;
    }
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


[**DXVA\_ProcAmpControlQueryRange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_procampcontrolqueryrange)

[**DXVA\_VideoDesc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc)

[**DXVA\_VideoPropertyRange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videopropertyrange)

 

 






