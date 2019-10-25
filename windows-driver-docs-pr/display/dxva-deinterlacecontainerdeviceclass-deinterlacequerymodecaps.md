---
title: DeinterlaceQueryModeCaps メソッド
description: Sample DXVA\_DeinterlaceContainerDeviceClass::D einterlaceQueryModeCaps 関数は、ドライバーに対してクエリを実行し、特定のノンインターレースモードと、そのモードでサポートされている可能性のある追加のビデオ処理の入力機能を確認します。
ms.assetid: 49070e57-2a93-447e-98d5-b98cded78b9c
keywords:
- DeinterlaceQueryModeCaps メソッドの表示デバイス
- DeinterlaceQueryModeCaps メソッドの表示デバイス, DXVA_DeinterlaceContainerDeviceClass インターフェイス
- DXVA_DeinterlaceContainerDeviceClass インターフェイス表示デバイス, DeinterlaceQueryModeCaps メソッド
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
ms.openlocfilehash: f7b3b2e06439e3628855432a43ce77747eb36f8f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838966"
---
# <a name="dxva_deinterlacecontainerdeviceclassdeinterlacequerymodecaps-method"></a>DXVA\_DeinterlaceContainerDeviceClass::D einterlaceQueryModeCaps メソッド


Sample **DeinterlaceQueryModeCaps**関数は、ドライバーに対してクエリを実行し、特定のノンインターレースモードと、そのモードでサポートされている可能性のある追加のビデオ処理の入力機能を確認します。

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

\] の*pGuidDeinterlaceMode* \[は、ノンインターレースモードを指定するために使用される GUID へのポインターを提供します。

\] の*Lpvideodescription* \[は、 [**DXVA\_videodesc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc)構造体へのポインターを提供します。この構造は、deinterlaced またはレート変換されるビデオの種類を定義します。

*lpDeinterlaceCaps* \[out\] は、ノンインターレースモードの機能を含む[**DXVA\_DeinterlaceCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacecaps)構造体へのポインターを受け取ります。

<a name="return-value"></a>戻り値
------------

成功した場合は 0 (S\_OK または DD\_OK) を返します。それ以外の場合は、エラーコードを返します。 エラーコードの完全な一覧については、 *ddraw*を参照してください。

<a name="remarks"></a>注釈
-------

ドライバーは、 *VMR*によって、VMR が特定のビデオ形式で使用可能なノンインターレースモードを特定した後に、ノンインターレースモードの機能に対して照会されます。 ドライバーは、 [**DeinterlaceQueryAvailableModes**](dxva-deinterlacecontainerdeviceclass-deinterlacequeryavailablemodes.md)関数の呼び出しから使用可能なモードを返します。

**DeinterlaceQueryModeCaps**関数は、 [**DXVA\_DeinterlaceCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacecaps)構造体の特定のモードの機能を報告します。

*Lpvideodescription*パラメーターをドライバーに渡して、ドライバーがソースビデオの解像度と形式をサポートできるようにします。 たとえば、ドライバーは480i コンテンツの3つのフィールドのアダプティブインターレースを実行できる場合がありますが、ボブのコンテンツしか使用できない可能性があります。 詳細については、「[ノンインターレースとフレームレート変換のビデオコンテンツ](https://docs.microsoft.com/windows-hardware/drivers/display/video-content-for-deinterlace-and-frame-rate-conversion)」を参照してください。

すべてのドライバーは、既存の*ビットブロック転送*ハードウェアを使用して、bob モードをサポートできる必要があります。

**RenderMoComp から*DeinterlaceQueryModeCaps*へのマッピング**

**DeinterlaceQueryModeCaps**関数は、 [**DD\_MOTIONCOMPコールバック**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)構造の**rendermocomp**メンバーへの呼び出しに直接マップされます。 **Rendermocomp**メンバーは、 [**DD\_RENDERMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)構造体を参照するディスプレイドライバーが提供する関数を指します。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacequerymodecaps" data-raw-source="[&lt;strong&gt;DXVA_DeinterlaceQueryModeCaps&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacequerymodecaps)"><strong>DXVA_DeinterlaceQueryModeCaps</strong></a>構造体へのポインター。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>lpOutputData</strong></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacecaps" data-raw-source="[&lt;strong&gt;DXVA_DeinterlaceCaps&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacecaps)"><strong>DXVA_DeinterlaceCaps</strong></a>構造体へのポインター。</p></td>
</tr>
</tbody>
</table>

 

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
<td align="left">N/A (ドライバーによって指定されたヘッダーファイルで宣言)</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**DD\_MOTIONCOMPCALLBACKS バック**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)

[**DD\_RENDERMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)

[**DeinterlaceQueryAvailableModes**](dxva-deinterlacecontainerdeviceclass-deinterlacequeryavailablemodes.md)

[**DXVA\_DeinterlaceQueryModeCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacequerymodecaps)

[**DXVA\_DeinterlaceCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacecaps)

[**DXVA\_VideoDesc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc)

 

 






