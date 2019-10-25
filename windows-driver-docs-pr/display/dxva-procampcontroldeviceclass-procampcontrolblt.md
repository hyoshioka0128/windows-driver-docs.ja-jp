---
title: ProcAmpControlBlt メソッド
description: Sample DXVA\_ProcAmpControlDeviceClass::P rocAmpControlBlt 関数は、出力をターゲットサーフェスに書き込んで、ProcAmp の調整操作を実行します。
ms.assetid: bf86fd39-554d-4ef1-adb7-202bb70fd3b4
keywords:
- ProcAmpControlBlt メソッドの表示デバイス
- ProcAmpControlBlt メソッドの表示デバイス, DXVA_ProcAmpControlDeviceClass インターフェイス
- DXVA_ProcAmpControlDeviceClass インターフェイス表示デバイス, ProcAmpControlBlt メソッド
topic_type:
- apiref
api_name:
- DXVA_ProcAmpControlDeviceClass.ProcAmpControlBlt
api_type:
- COM
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6b0da5cf0b0a951b8a4db75032c124ea9e01b2d3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839713"
---
# <a name="dxva_procampcontroldeviceclassprocampcontrolblt-method"></a>DXVA\_ProcAmpControlDeviceClass::P rocAmpControlBlt メソッド


Sample *ProcAmpControlBlt*関数は、出力をターゲットサーフェスに書き込むことによって、ProcAmp の調整操作を実行します。

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

\] の*lpDDSDstSurface* \[は、ターゲットサーフェイスへのポインターを提供します。

\] の*lpDDSSrcSurface* \[は、ソースサーフェイスへのポインターを提供します。

\] の*Ccblt* \[は、 [**DXVA\_ProcAmpControlBlt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_procampcontrolblt)構造体へのポインターを提供します。これは、ターゲットサーフェスに ProcAmp 調整データを出力することを指定します。

<a name="return-value"></a>戻り値
------------

成功した場合は 0 (S\_OK または DD\_OK) を返します。それ以外の場合は、エラーコードを返します。 エラーコードの完全な一覧については、 *ddraw*を参照してください。

<a name="remarks"></a>注釈
-------

ソースとターゲットの四角形は、ProcAmp の調整または伸縮のいずれかに必要です。 拡大のサポートは省略可能であり、 [**DXVA\_ProcAmpControlCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_procampcontrolcaps)構造体の**videoprocessingcaps**メンバーによって報告されます。 サブ四角形のサポートも省略可能です。

移動先の画面には、スクリーンプレーン、D3D レンダーターゲット、D3D テクスチャ、またはレンダーターゲットでもある D3D テクスチャを指定できます。 ターゲットサーフェスは、常にローカルのビデオメモリに割り当てられます。 ターゲットサーフェイスのピクセル形式は、DXVA\_ProcAmpControlCaps 構造体に示されているものになります。ただし、ProcAmp 調整手順の一部として、YUV から RGB へのカラー空間変換が実行されている場合は除きます。 この場合、コピー先のサーフェス形式は、各色コンポーネントに対して8ビット以上の有効桁数を持つ RGB 形式になります。

Sample *ProcAmpControlBlt*関数は、 [**DD\_MOTIONCOMPコールバック**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)構造の**rendermocomp**メンバーへの呼び出しに直接マップされます。 **Rendermocomp**メンバーは、 [**DD\_RENDERMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)構造体を参照する、ドライバーが提供する*ddmocomprender*コールバックを指します。 DD\_RENDERMOCOMPDATA 構造体は、次のように入力されます。

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
<td align="left"><p>バッファーの数。値2である必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpBufferInfo</strong></p></td>
<td align="left"><p>2つのサーフェイスの配列へのポインター。 配列の最初の要素は、コピー先のサーフェイスです。配列の2番目の要素は、ソースサーフェイスです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dwFunction</strong></p></td>
<td align="left"><p><strong>DXVA_ProcAmpControlBltFnCode</strong>定数 ( <em>DXVA</em>で定義されています)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpInputData</strong></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_procampcontrolblt" data-raw-source="[&lt;strong&gt;DXVA_ProcAmpControlBlt&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_procampcontrolblt)"><strong>DXVA_ProcAmpControlBlt</strong></a>構造体へのポインター。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>lpOutputData</strong></p></td>
<td align="left"><p>NULL:</p></td>
</tr>
</tbody>
</table>

 

ProcAmp コントロールに使用される DirectX VA デバイスでは、表示ドライバーが提供する BeginMoCompFrame または EndMoCompFrame 関数を呼び出さずに、RenderMoComp が呼び出されます。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**DXVA\_VideoDesc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc)

[**DXVA\_ProcAmpControlCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_procampcontrolcaps)

[**DXVA\_ProcAmpControlBlt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_procampcontrolblt)

[**DD\_MOTIONCOMPCALLBACKS バック**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)

[**DD\_CREATEMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_createmocompdata)

 

 






