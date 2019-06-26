---
title: DeinterlaceQueryModeCaps メソッド
description: サンプルの DXVA\_DeinterlaceContainerDeviceClass::DeinterlaceQueryModeCaps 関数は、特定の入力機能インター レースを解除モードとそのサポート可能性のある追加ビデオの処理を決定するドライバーをクエリモード。
ms.assetid: 49070e57-2a93-447e-98d5-b98cded78b9c
keywords:
- ディスプレイ デバイスの DeinterlaceQueryModeCaps メソッド
- DeinterlaceQueryModeCaps メソッド ディスプレイ デバイス、DXVA_DeinterlaceContainerDeviceClass インターフェイス
- DXVA_DeinterlaceContainerDeviceClass は、DeinterlaceQueryModeCaps メソッドのディスプレイ デバイスをインターフェイスします。
topic_type:
- apiref
api_name:
- DXVA_DeinterlaceContainerDeviceClass.DeinterlaceQueryModeCaps
api_location:
- N/A
api_type:
- COM
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: b531c3cf7016d6a9a81b9850ed3afd4320c557aa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375826"
---
# <a name="dxvadeinterlacecontainerdeviceclassdeinterlacequerymodecaps-method"></a>DXVA\_DeinterlaceContainerDeviceClass::DeinterlaceQueryModeCaps メソッド


サンプル**DeinterlaceQueryModeCaps**関数は、特定の入力機能インター レースを解除モードとそのモードをサポート可能性のある追加ビデオの処理を決定するドライバーをクエリします。

<a name="syntax"></a>構文
------

```cpp
HRESULT DeinterlaceQueryModeCaps(
  [in]  LPGUID               pGuidDeinterlaceMode,
  [in]  LPDXVA_VideoDesc     lpVideoDescription,
  [out] DXVA_DeinterlaceCaps *lpDeinterlaceCaps
);
```

<a name="parameters"></a>パラメーター
----------

*pGuidDeinterlaceMode* \[で\]ノンインター レース化モードを指定するために使用する GUID へのポインターを提供します。

*lpVideoDescription* \[で\]へのポインターを提供する[ **DXVA\_VideoDesc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videodesc) deinterlaced するビデオの種類を定義する構造またはレート変換されます。

*lpDeinterlaceCaps* \[アウト\]へのポインターを受け取る、 [ **DXVA\_DeinterlaceCaps** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlacecaps)の機能を含む構造体、インター レース モードを解除します。

<a name="return-value"></a>戻り値
------------

0 を返します (S\_[ok] または DD\_OK) 成功した場合、それ以外の場合、エラー コードを返します。 参照してください*ddraw.h*エラー コードの完全な一覧についてはします。

<a name="remarks"></a>コメント
-------

ドライバーを照会、 *VMR* VMR が特定のビデオ形式の使用可能なインター モードを決定した後のインター モードの機能です。 ドライバーでは、使用可能なモードを返しますへの呼び出しからその[ **DeinterlaceQueryAvailableModes** ](dxva-deinterlacecontainerdeviceclass-deinterlacequeryavailablemodes.md)関数。

**DeinterlaceQueryModeCaps**関数で指定されたモードの機能の報告、 [ **DXVA\_DeinterlaceCaps** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlacecaps)構造体。

*LpVideoDescription*ドライバーは、解像度と、ソース ビデオの形式をサポートできるようにパラメーターは、ドライバーに渡されます。 など、ドライバーを実行することがありますが、3 つのフィールド アダプティブ 480i のコンテンツのインター レースを解除、1080 i コンテンツを bob できる可能性があります。 詳細については、次を参照してください。[ビデオ コンテンツのインターとフレーム レート変換](https://docs.microsoft.com/windows-hardware/drivers/display/video-content-for-deinterlace-and-frame-rate-conversion)します。

すべてのドライバーは、既存を使用して、bob のモードをサポートできる必要があります*ビット ブロック転送*ハードウェア。

**マッピングを RenderMoComp *DeinterlaceQueryModeCaps***

**DeinterlaceQueryModeCaps**関数のマップへの呼び出しに直接、 **RenderMoComp**のメンバー、 [ **DD\_MOTIONCOMPCALLBACKS**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)構造体。 **RenderMoComp**メンバーが参照するディスプレイ ドライバーによって提供される関数を指す、 [ **DD\_RENDERMOCOMPDATA** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)構造体。

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
<td align="left"><p>ポインターを<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlacequerymodecaps" data-raw-source="[&lt;strong&gt;DXVA_DeinterlaceQueryModeCaps&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlacequerymodecaps)"> <strong>DXVA_DeinterlaceQueryModeCaps</strong> </a>構造体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>lpOutputData</strong></p></td>
<td align="left"><p>ポインターを<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlacecaps" data-raw-source="[&lt;strong&gt;DXVA_DeinterlaceCaps&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlacecaps)"> <strong>DXVA_DeinterlaceCaps</strong> </a>構造体。</p></td>
</tr>
</tbody>
</table>

 

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


[**DD\_MOTIONCOMPCALLBACKS**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)

[**DD\_RENDERMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)

[**DeinterlaceQueryAvailableModes**](dxva-deinterlacecontainerdeviceclass-deinterlacequeryavailablemodes.md)

[**DXVA\_DeinterlaceQueryModeCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlacequerymodecaps)

[**DXVA\_DeinterlaceCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlacecaps)

[**DXVA\_VideoDesc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videodesc)

 

 






