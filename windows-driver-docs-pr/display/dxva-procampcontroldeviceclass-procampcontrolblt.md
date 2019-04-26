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
ms.openlocfilehash: 409e7b7075f43e116e7cb399ddf94c6b43f4c275
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341102"
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

*ccBlt* \[で\]へのポインターを提供する[ **DXVA\_ProcAmpControlBlt** ](https://msdn.microsoft.com/library/windows/hardware/ff564015) ProcAmp 調整データ出力を指定する構造体、宛先表面。

<a name="return-value"></a>戻り値
------------

0 を返します (S\_[ok] または DD\_OK) 成功した場合、それ以外の場合、エラー コードを返します。 参照してください*ddraw.h*エラー コードの完全な一覧についてはします。

<a name="remarks"></a>注釈
-------

ソースと変換先の四角形は、矩形 ProcAmp 調整または拡大のいずれかの必要があります。 サポート拡張は省略可能なによって報告された、 **VideoProcessingCaps**のメンバー、 [ **DXVA\_ProcAmpControlCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff564019)構造体。 Subrectangles のサポートも省略可能です。

宛先表面は画面の平面、レンダー ターゲット、D3D テクスチャまたはレンダー ターゲットになっている D3D テクスチャを D3D。 宛先表面が、常にローカルのビデオ メモリに割り当てられます。 転送先のサーフェイスのピクセル形式は、DXVA で示されているものになります\_ProcAmp 調整手順の一部として、YUV から RGB 色空間変換が実行される場合を除き、ProcAmpControlCaps が構造体します。 この場合、宛先表面形式は、各色コンポーネントの有効桁数の 8 ビット以上で、RGB 形式になります。

サンプル*ProcAmpControlBlt*関数のマップへの呼び出しに直接、 **RenderMoComp**のメンバー、 [ **DD\_MOTIONCOMPCALLBACKS**](https://msdn.microsoft.com/library/windows/hardware/ff551660)構造体。 **RenderMoComp**メンバーがドライバーによって提供される指す*DdMoCompRender*参照コールバック、 [ **DD\_RENDERMOCOMPDATA**](https://msdn.microsoft.com/library/windows/hardware/ff551693)構造体。 DD\_RENDERMOCOMPDATA 構造は次のように入力されます。

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
<td align="left"><p>ポインターを<a href="https://msdn.microsoft.com/library/windows/hardware/ff564015" data-raw-source="[&lt;strong&gt;DXVA_ProcAmpControlBlt&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564015)"> <strong>DXVA_ProcAmpControlBlt</strong> </a>構造体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>lpOutputData</strong></p></td>
<td align="left"><p>NULL: </p></td>
</tr>
</tbody>
</table>

 

ProcAmp の制御に使用される DirectX VA デバイス、RenderMoComp は呼び出さず、ディスプレイ ドライバーによって提供される BeginMoCompFrame または EndMoCompFrame 関数と呼ばれます。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**DXVA\_VideoDesc**](https://msdn.microsoft.com/library/windows/hardware/ff564070)

[**DXVA\_ProcAmpControlCaps**](https://msdn.microsoft.com/library/windows/hardware/ff564019)

[**DXVA\_ProcAmpControlBlt**](https://msdn.microsoft.com/library/windows/hardware/ff564015)

[**DD\_MOTIONCOMPCALLBACKS**](https://msdn.microsoft.com/library/windows/hardware/ff551660)

[**DD\_CREATEMOCOMPDATA**](https://msdn.microsoft.com/library/windows/hardware/ff550529)

 

 






