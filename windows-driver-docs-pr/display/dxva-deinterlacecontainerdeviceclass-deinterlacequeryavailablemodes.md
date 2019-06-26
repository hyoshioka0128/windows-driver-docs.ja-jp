---
title: DeinterlaceQueryAvailableModes メソッド
description: サンプルの DXVA\_DeinterlaceContainerDeviceClass::DeinterlaceQueryAvailableModes 関数のクエリの特定の入力ビデオ形式の使用可能なデインター レースまたはフレーム レート変換モード。
ms.assetid: be721bde-3c72-4942-9f33-5ea1bf2d187c
keywords:
- ディスプレイ デバイスの DeinterlaceQueryAvailableModes メソッド
- DeinterlaceQueryAvailableModes メソッド ディスプレイ デバイス、DXVA_DeinterlaceContainerDeviceClass インターフェイス
- DXVA_DeinterlaceContainerDeviceClass は、DeinterlaceQueryAvailableModes メソッドのディスプレイ デバイスをインターフェイスします。
topic_type:
- apiref
api_name:
- DXVA_DeinterlaceContainerDeviceClass.DeinterlaceQueryAvailableModes
api_type:
- COM
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: d2f3195b3fbc9b73786a2a4c8f7fa5fd7f2b3442
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375834"
---
# <a name="dxvadeinterlacecontainerdeviceclassdeinterlacequeryavailablemodes-method"></a>DXVA\_DeinterlaceContainerDeviceClass::DeinterlaceQueryAvailableModes メソッド


サンプル*DeinterlaceQueryAvailableModes*関数の特定の入力ビデオ形式の使用可能なデインター レースまたはフレーム レート変換モードのクエリ。

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

*lpVideoDescription* \[で\]へのポインターを提供する[ **DXVA\_VideoDesc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videodesc)のビデオ ストリームの説明を含む構造体実行するデインター レースまたはフレーム レート変換します。

*lpdwNumModesSupported* \[入力、出力\]インターまたはフレーム レートの変換モードは、配列で返される数へのポインターを受け取る*pGuidsDeinterlaceModes*します。

*pGuidsDeinterlaceModes* \[入力、出力\]ドライバーによってサポートされているインターまたはフレーム レート変換モードを表す Guid の配列へのポインターを受け取ります。

<a name="return-value"></a>戻り値
------------

0 を返します (S\_[ok] または DD\_OK) 成功した場合、それ以外の場合、エラー コードを返します。 参照してください*ddraw.h*エラー コードの完全な一覧についてはします。

<a name="remarks"></a>注釈
-------

*LpVideoDescription*ドライバーは、解像度と、ソース ビデオの形式をサポートできるようにパラメーターは、ドライバーに渡されます。 など、ドライバーを実行することがありますが、3 つのフィールド アダプティブ 480i のコンテンツのインター レースを解除、1080 i コンテンツを bob できる可能性があります。 詳細については、次を参照してください。[ビデオ コンテンツのインターとフレーム レート変換](https://docs.microsoft.com/windows-hardware/drivers/display/video-content-for-deinterlace-and-frame-rate-conversion)します。

によって返される Guid、 *pGuidsDeinterlaceModes*パラメーターの品質を降順で返す (つまり、最高品質のモードに占める返される GUID の配列の最初の要素)。

すべてのドライバーは、既存を使用して、bob のモードをサポートできる必要があります*ビット ブロック転送*(blt) ハードウェア。 モードの詳細については、次を参照してください。、[インター レースを解除モード](https://docs.microsoft.com/windows-hardware/drivers/display/deinterlace-modes)と[フレーム レート変換モード](https://docs.microsoft.com/windows-hardware/drivers/display/frame-rate-conversion-modes)トピック。

ドライバーからの要求に対する応答でサポートされている Guid (モード) を返します、 *VMR*します。 ドライバーがへの呼び出しに応答の[ *DdMoCompRender* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)コールバック関数。 ドライバーはから Guid を返します、 **lpOutputData**のメンバー、 [ **DD\_RENDERMOCOMPDATA** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)構造体、 *lpRenderData*パラメーターの*DdMoCompRender*ポイント。 **LpOutputData**へのポインター、 [ **DXVA\_DeinterlaceQueryAvailableModes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlacequeryavailablemodes) でGuidの配列を格納する構造体**Guid**メンバー。

**マッピングを RenderMoComp** ***DeinterlaceQueryAvailableModes***

サンプル*DeinterlaceQueryAvailableModes*関数のマップへの呼び出しに直接、 **RenderMoComp**のメンバー、 [ **DD\_MOTIONCOMPCALLBACKS**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)構造体。 **RenderMoComp**メンバーが参照するディスプレイ ドライバーによって提供される関数を指す、 [ **DD\_RENDERMOCOMPDATA** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)構造体。

**RenderMoComp**ドライバーによって提供される表示せずにコールバックが呼び出されて**BeginMoCompFrame**または**EndMoCompFrame**最初に呼び出される関数。

DD\_RENDERMOCOMPDATA 構造は次のように入力されます。

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
<td align="left"><p>0 を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpBufferInfo</strong></p></td>
<td align="left"><p>NULL:</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dwFunction</strong></p></td>
<td align="left"><p><strong>DXVA_DeinterlaceQueryAvailableModesFnCode</strong>定数 (で定義されている<em>dxva.h</em>)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpInputData</strong></p></td>
<td align="left"><p>塗りつぶしへのポインター <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videodesc" data-raw-source="[&lt;strong&gt;DXVA_VideoDesc&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videodesc)"> <strong>DXVA_VideoDesc</strong> </a>構造体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>lpOutputData</strong></p></td>
<td align="left"><p>ポインターを<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlacequeryavailablemodes" data-raw-source="[&lt;strong&gt;DXVA_DeinterlaceQueryAvailableModes&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlacequeryavailablemodes)"> <strong>DXVA_DeinterlaceQueryAvailableModes</strong> </a>構造体。</p></td>
</tr>
</tbody>
</table>

 

後に、 *VMR*インターまたはフレームの変換モードを決定しました VMR クエリの特定のインター モードの入力の要件に関する詳細情報を取得するドライバーを特定のビデオ形式の使用可能なそのモードをサポート可能性のある、追加のビデオを処理します。 ドライバーでは、この情報を返しますの呼び出しからその[ **DeinterlaceQueryModeCaps** ](dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps.md)関数。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**DD\_MOTIONCOMPCALLBACKS**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)

[**DD\_RENDERMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)

[**DeinterlaceQueryModeCaps**](dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps.md)

[**DXVA\_VideoDesc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videodesc)

[**DXVA\_SampleFormat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ne-dxva-_dxva_sampleformat)

 

 






