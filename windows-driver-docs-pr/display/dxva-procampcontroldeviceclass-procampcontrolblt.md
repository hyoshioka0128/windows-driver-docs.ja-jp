---
title: ProcAmpControlBlt メソッド
description: サンプルの DXVA\_ProcAmpControlDeviceClass::ProcAmpControlBlt 関数を変換先の画面に出力を記述することで ProcAmp 調整操作を実行します。
ms.assetid: bf86fd39-554d-4ef1-adb7-202bb70fd3b4
keywords:
- ディスプレイ デバイスの ProcAmpControlBlt メソッド
- ProcAmpControlBlt メソッド ディスプレイ デバイス、DXVA_ProcAmpControlDeviceClass インターフェイス
- DXVA_ProcAmpControlDeviceClass は、ProcAmpControlBlt メソッドのディスプレイ デバイスをインターフェイスします。
topic_type:
- apiref
api_name:
- DXVA_ProcAmpControlDeviceClass.ProcAmpControlBlt
api_type:
- COM
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 31577a3347939a500bc061a5273e63c1501ab3e9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375811"
---
# <a name="dxvaprocampcontroldeviceclassprocampcontrolblt-method"></a>DXVA\_ProcAmpControlDeviceClass::ProcAmpControlBlt メソッド


サンプル*ProcAmpControlBlt*関数を変換先の画面に出力を記述することで ProcAmp 調整操作を実行します。

<a name="syntax"></a>構文
------

```cpp
HRESULT ProcAmpControlBlt(
  [in] LPDDSURFACE            lpDDSDstSurface,
  [in] LPDDSURFACE            lpDDSSrcSurface,
  [in] DXVA_ProcAmpControlBlt *ccBlt
);
```

<a name="parameters"></a>パラメーター
----------

*lpDDSDstSurface* \[で\]宛先表面へのポインターを提供します。

*lpDDSSrcSurface* \[で\]ソース画面へのポインターを提供します。

*ccBlt* \[で\]へのポインターを提供する[ **DXVA\_ProcAmpControlBlt** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_procampcontrolblt) ProcAmp 調整データ出力を指定する構造体、宛先表面。

<a name="return-value"></a>戻り値
------------

0 を返します (S\_[ok] または DD\_OK) 成功した場合、それ以外の場合、エラー コードを返します。 参照してください*ddraw.h*エラー コードの完全な一覧についてはします。

<a name="remarks"></a>注釈
-------

ソースと変換先の四角形は、矩形 ProcAmp 調整または拡大のいずれかの必要があります。 サポート拡張は省略可能なによって報告された、 **VideoProcessingCaps**のメンバー、 [ **DXVA\_ProcAmpControlCaps** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_procampcontrolcaps)構造体。 Subrectangles のサポートも省略可能です。

宛先表面は画面の平面、レンダー ターゲット、D3D テクスチャまたはレンダー ターゲットになっている D3D テクスチャを D3D。 宛先表面が、常にローカルのビデオ メモリに割り当てられます。 転送先のサーフェイスのピクセル形式は、DXVA で示されているものになります\_ProcAmp 調整手順の一部として、YUV から RGB 色空間変換が実行される場合を除き、ProcAmpControlCaps が構造体します。 この場合、宛先表面形式は、各色コンポーネントの有効桁数の 8 ビット以上で、RGB 形式になります。

サンプル*ProcAmpControlBlt*関数のマップへの呼び出しに直接、 **RenderMoComp**のメンバー、 [ **DD\_MOTIONCOMPCALLBACKS**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)構造体。 **RenderMoComp**メンバーがドライバーによって提供される指す*DdMoCompRender*参照コールバック、 [ **DD\_RENDERMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)構造体。 DD\_RENDERMOCOMPDATA 構造は次のように入力されます。

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
<td align="left"><p>値 2 は、バッファーの数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpBufferInfo</strong></p></td>
<td align="left"><p>2 つのサーフェスの配列へのポインター。 配列の最初の要素が宛先表面;配列の 2 番目の要素では、ソース サーフェイスです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dwFunction</strong></p></td>
<td align="left"><p><strong>DXVA_ProcAmpControlBltFnCode</strong>定数 (で定義されている<em>dxva.h</em>)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpInputData</strong></p></td>
<td align="left"><p>ポインターを<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_procampcontrolblt" data-raw-source="[&lt;strong&gt;DXVA_ProcAmpControlBlt&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_procampcontrolblt)"> <strong>DXVA_ProcAmpControlBlt</strong> </a>構造体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>lpOutputData</strong></p></td>
<td align="left"><p>NULL:</p></td>
</tr>
</tbody>
</table>

 

ProcAmp の制御に使用される DirectX VA デバイス、RenderMoComp は呼び出さず、ディスプレイ ドライバーによって提供される BeginMoCompFrame または EndMoCompFrame 関数と呼ばれます。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**DXVA\_VideoDesc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videodesc)

[**DXVA\_ProcAmpControlCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_procampcontrolcaps)

[**DXVA\_ProcAmpControlBlt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_procampcontrolblt)

[**DD\_MOTIONCOMPCALLBACKS**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)

[**DD\_CREATEMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_createmocompdata)

 

 






