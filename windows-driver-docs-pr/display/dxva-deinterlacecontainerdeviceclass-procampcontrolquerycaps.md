---
title: ProcAmpControlQueryCaps メソッド
description: サンプルの DXVA\_DeinterlaceContainerDeviceClass::ProcAmpControlQueryCaps 関数により、クエリ、ProcAmp コントロール デバイスとなる可能性があるその他のビデオの処理操作の入力の要件を決定するドライバーを VMRサポートされています。
ms.assetid: e89f9a01-e8b3-4311-ad3b-296021c9795e
keywords:
- ディスプレイ デバイスの ProcAmpControlQueryCaps メソッド
- ProcAmpControlQueryCaps メソッド ディスプレイ デバイス、DXVA_DeinterlaceContainerDeviceClass インターフェイス
- DXVA_DeinterlaceContainerDeviceClass は、ProcAmpControlQueryCaps メソッドのディスプレイ デバイスをインターフェイスします。
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
ms.openlocfilehash: f95f36d60efeebdd5657274e745b9c96c8dec8f2
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349039"
---
# <a name="dxvadeinterlacecontainerdeviceclassprocampcontrolquerycaps-method"></a>DXVA\_DeinterlaceContainerDeviceClass::ProcAmpControlQueryCaps メソッド


サンプル*ProcAmpControlQueryCaps*関数により、 *VMR* ProcAmp 制御デバイスおよび可能性があります追加ビデオ処理操作の入力の要件を決定するドライバーを照会するにはサポートされます。 クエリに ProcAmp 調整操作が実行されるのと同時に発生します。

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

*lpVideoDescription* \[で\]へのポインターを提供する[ **DXVA\_VideoDesc** ](https://msdn.microsoft.com/library/windows/hardware/ff564070) ProcAmp の制御パラメーターを定義する構造体処理するビデオです。

*lpProcAmpCaps* \[アウト\]へのポインターを受け取る、 [ **DXVA\_ProcAmpControlCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff564019)のドライバーの機能を含む構造体ProcAmp コントロールの操作です。

<a name="return-value"></a>戻り値
------------

0 を返します (S\_[ok] または DD\_OK) 成功した場合、それ以外の場合、エラー コードを返します。 参照してください*ddraw.h*エラー コードの完全な一覧についてはします。

<a name="remarks"></a>コメント
-------

ドライバーの ProcAmp コントロール モードでのユーザー モード コンポーネントには、その機能の報告、 [ **DXVA\_ProcAmpControlCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff564019)によって示される構造*lpProcAmpCaps*.

サンプル*ProcAmpControlQueryCaps*関数のマップへの呼び出しに直接、 **RenderMoComp**のメンバー、 [ **DD\_MOTIONCOMPCALLBACKS**](https://msdn.microsoft.com/library/windows/hardware/ff551660)構造体。 **RenderMoComp**関数は、ドライバーによって提供される指す*DdMoCompRender*参照コールバック、 [ **DD\_RENDERMOCOMPDATA**](https://msdn.microsoft.com/library/windows/hardware/ff551693)構造体。 DD\_RENDERMOCOMPDATA 構造は次のように入力されます。

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
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpBufferInfo</strong></p></td>
<td align="left"><p>NULL</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dwFunction</strong></p></td>
<td align="left"><p><strong>DXVA_ProcAmpControlQueryCapsFnCode</strong>定数 (で定義されている<em>dxva.h</em>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpInputData</strong></p></td>
<td align="left"><p>塗りつぶしへのポインター <a href="https://msdn.microsoft.com/library/windows/hardware/ff564070" data-raw-source="[&lt;strong&gt;DXVA_VideoDesc&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564070)"> <strong>DXVA_VideoDesc</strong> </a>構造体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>lpOutputData</strong></p></td>
<td align="left"><p>ポインターを<a href="https://msdn.microsoft.com/library/windows/hardware/ff564019" data-raw-source="[&lt;strong&gt;DXVA_ProcAmpControlCaps&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564019)"> <strong>DXVA_ProcAmpControlCaps</strong> </a>構造体。</p></td>
</tr>
</tbody>
</table>

 

関数を使用せず、ディスプレイ ドライバーによって提供される BeginMoCompFrame または EndMoCompFrame 最初に呼び出される RenderMoComp 関数が呼び出されることに注意してください。

**コード例**

次のコードを実装する方法の例を示します、 *ProcAmpControlQueryCaps*関数。

```cpp
HRESULT
DXVA_DeinterlaceContainerDeviceClass::ProcAmpControlQueryCaps(
    LPDXVA_VideoDesc lpVideoDesc,
    LPDXVA_ProcAmpControlCaps lpProcAmpControlCaps
    )
{
    // only the YUY2 and YV12 formats can be operated on
    if (lpVideoDesc->d3dFormat != '2YUY' &amp;&amp;
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


[**DXVA\_VideoDesc**](https://msdn.microsoft.com/library/windows/hardware/ff564070)

[**DXVA\_ProcAmpControlCaps**](https://msdn.microsoft.com/library/windows/hardware/ff564019)

[**DD\_MOTIONCOMPCALLBACKS**](https://msdn.microsoft.com/library/windows/hardware/ff551660)

[**DD\_RENDERMOCOMPDATA**](https://msdn.microsoft.com/library/windows/hardware/ff551693)

 

 






