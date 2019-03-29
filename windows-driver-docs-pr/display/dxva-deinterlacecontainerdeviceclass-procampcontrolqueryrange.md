---
title: ProcAmpControlQueryRange メソッド
description: サンプルの DXVA\_DeinterlaceContainerDeviceClass::ProcAmpControlQueryRange 関数により、最小、最大値、ステップのサイズ、および各 ProcAmp プロパティの既定値を決定するドライバーを照会する VMR します。
ms.assetid: 13fd5d4b-f753-4a2c-80e0-c9614d7ebd3d
keywords:
- ディスプレイ デバイスの ProcAmpControlQueryRange メソッド
- ProcAmpControlQueryRange メソッド ディスプレイ デバイス、DXVA_DeinterlaceContainerDeviceClass インターフェイス
- DXVA_DeinterlaceContainerDeviceClass は、ProcAmpControlQueryRange メソッドのディスプレイ デバイスをインターフェイスします。
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
ms.openlocfilehash: 88ab10bc4188c3df053b8f91b650a380311e864f
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350223"
---
# <a name="dxvadeinterlacecontainerdeviceclassprocampcontrolqueryrange-method"></a>DXVA\_DeinterlaceContainerDeviceClass::ProcAmpControlQueryRange メソッド


サンプル**ProcAmpControlQueryRange**関数により、 *VMR*ステップ サイズ、および各 ProcAmp プロパティの既定値、最小、最大値を決定するドライバーをクエリします。

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

*VideoProperty* \[で\]ドライバーが情報を返す必要があります ProcAmp コントロール プロパティを識別します。 このパラメーターに指定できる値を次に示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値</th>
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
<td align="left"><p>対照的情報に返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DXVA_ProcAmp_Hue</p></td>
<td align="left"><p>Hue の情報を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXVA_ProcAmp_Saturation</p></td>
<td align="left"><p>鮮やかさの情報を返します。</p></td>
</tr>
</tbody>
</table>

 

*lpVideoDescription* \[で\]へのポインターを提供する[ **DXVA\_VideoDesc** ](https://msdn.microsoft.com/library/windows/hardware/ff564070)構造体。 この構造体では、ドライバー ProcAmp 調整の適用先となる、ビデオの説明を提供します。 ドライバーは、特定のビデオ ストリームの ProcAmp サポートを調整できます。

*lpPropRange* \[アウト\]へのポインターを受け取る、 [ **DXVA\_VideoPropertyRange** ](https://msdn.microsoft.com/library/windows/hardware/ff564083)の範囲、ステップのサイズを指定してProcAmp の既定値。

<a name="return-value"></a>戻り値
------------

0 を返します (S\_[ok] または DD\_[ok]) エラー コードを返しますそれ以外の場合、成功した場合 (たとえば、E\_NOTIMPL)。 参照してください*ddraw.h*エラー コードの完全な一覧についてはします。

<a name="remarks"></a>コメント
-------

ProcAmp の各プロパティの VMR は、最小、最大値、ステップのサイズ、および既定値を決定するドライバーを照会します。 ドライバーを返す必要があるかどうか、ハードウェアは、特定の ProcAmp コントロール プロパティをサポートしていません、E\_から NOTIMPL、 **ProcAmpControlQueryRange**関数。

ProcAmp プロパティに関する詳細については、次を参照してください。 [ProcAmp プロパティ](https://msdn.microsoft.com/library/windows/hardware/ff569189)します。

サンプル**ProcAmpControlQueryRange**関数のマップへの呼び出しに直接、 **RenderMoComp**のメンバー、 [ **DD\_MOTIONCOMPCALLBACKS**](https://msdn.microsoft.com/library/windows/hardware/ff551660)構造体。 **RenderMoComp**メンバーがドライバーによって提供される指す[ **DdMoCompRender** ](https://msdn.microsoft.com/library/windows/hardware/ff550248)参照コールバック、 [ **DD\_RENDERMOCOMPDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551693)構造体。 DD\_RENDERMOCOMPDATA 構造は次のように入力されます。

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
<td align="left"><p>dwNumBuffers</p></td>
<td align="left"><p>0 を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>lpBufferInfo</p></td>
<td align="left"><p>NULL: </p></td>
</tr>
<tr class="odd">
<td align="left"><p>dwFunction</p></td>
<td align="left"><p><strong>DXVA_ProcAmpControlQueryRangeFnCode</strong>定数 (で定義されている<em>dxva.h</em>)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>lpInputData</p></td>
<td align="left"><p>ポインターを<a href="https://msdn.microsoft.com/library/windows/hardware/ff564032" data-raw-source="[&lt;strong&gt;DXVA_ProcAmpControlQueryRange&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564032)"> <strong>DXVA_ProcAmpControlQueryRange</strong> </a>構造体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>lpOutputData</p></td>
<td align="left"><p>ポインターを<a href="https://msdn.microsoft.com/library/windows/hardware/ff564083" data-raw-source="[&lt;strong&gt;DXVA_VideoPropertyRange&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564083)"> <strong>DXVA_VideoPropertyRange</strong> </a>構造体。</p></td>
</tr>
</tbody>
</table>

 

関数を使用せず、ディスプレイ ドライバーによって提供される BeginMoCompFrame または EndMoCompFrame 最初に呼び出される RenderMoComp 関数が呼び出されることに注意してください。

**コード例**

次のコードを実装する方法の例を示します、 *ProcAmpControlQueryRange*関数。

```cpp
HRESULT
DXVA_DeinterlaceContainerDeviceClass::ProcAmpControlQueryRange(
    DWORD VideoProperty,
    LPDXVA_VideoDesc lpVideoDesc,
    DXVA_VideoPropertyRange* lpPropRange
    )
{
    // only the YUY2 and YV12 formats can be operated on
    if (lpVideoDesc->d3dFormat != '2YUY' &amp;&amp;
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

<a name="requirements"></a>必要条件
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
<td align="left">N/A (Declared ドライバーによって提供されるヘッダー ファイル内)</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**DXVA\_ProcAmpControlQueryRange**](https://msdn.microsoft.com/library/windows/hardware/ff564032)

[**DXVA\_VideoDesc**](https://msdn.microsoft.com/library/windows/hardware/ff564070)

[**DXVA\_VideoPropertyRange**](https://msdn.microsoft.com/library/windows/hardware/ff564083)

 

 






