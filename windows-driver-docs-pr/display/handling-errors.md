---
title: エラーの処理
description: エラーの処理
ms.assetid: ac4e056e-3304-4934-887a-5cc2b87989bd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e813dad58955ae171befc7b3714e783cbf8d649d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839663"
---
# <a name="handling-errors"></a>エラーの処理


ユーザーモードディスプレイドライバーによって実装される[Direct3D version 10 関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)は、通常、戻りパラメーターの型に対して VOID を持ちます。 このルールの主な例外は、 *CalcPrivate***ObjType***Size*型の関数 (たとえば、 [**CalcPrivateResourceSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivateresourcesize)関数) です。 この型の関数は、* Create ***ObjType**関数 (たとえば、 [**createresource () を使用して、ドライバーが特定のオブジェクトの種類を作成するために必要なメモリ領域のサイズを示すサイズ\_t パラメーター型を返します。D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource))。

VOID を返すことにより、ユーザーモードの表示ドライバーは、通常の方法 (つまり、ユーザーモードの表示ドライバーの関数の戻りパラメーターを通じて) の Direct3D ランタイムにエラーを通知しません。 代わりに、ユーザーモードの表示ドライバーは、このような情報をランタイムに渡すために、Direct3D ランタイムの[**pfnSetErrorCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_seterror_cb) callback 関数を使用する必要があります。 ランタイムは、 [**D3D10DDI\_CORELAYER\_DEVICECALLBACKS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddi_corelayer_devicecallbacks)構造体内の**pfnSetErrorCb**へのポインターを提供します。この構造体は、 [**D3D10DDIARG\_CREATEDEVICE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice)構造体の**pUMCallbacks**メンバーが指すようにします。[**CreateDevice (D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)関数の呼び出しです。

各ユーザーモードの display driver 関数のリファレンスページでは、関数が**pfnSetErrorCb**の呼び出しを通じて渡すことができるエラーを指定します。 つまり、ユーザーモード表示ドライバーが、現在のユーザーモードの表示ドライバー関数で許可されていないエラーコードを使用して**pfnSetErrorCb**を呼び出すと、エラー状態が重大であり、適切に動作することがランタイムによって判断されます。 ランタイムは**pfnSetErrorCb**中に適切に動作するため、 **pfnSetErrorCb**(S\_OK) などを呼び出すことによって、 **pfnSetErrorCb**(E\_FAIL) の呼び出しによる影響を元に戻すことはできません。 実際、ランタイムは、S\_OK が "無効" または "重大" であると判断し、E\_失敗します。 S\_OK リターンコードの概念は、 **pfnSetErrorCb**を呼び出さないユーザーモードの表示ドライバー関数と同じです。

Direct3D ランタイムによって、エラー状態が重大であると判断された場合、まず、ワトソン博士でエラーをログに記録することによってアクションが実行されます。これは、既定の事後事後 (just-in-time) デバッガーです。 その後、ランタイムはデバイスを破棄して、D3DDDIERR\_DEVICEREMOVED エラーコードを受け取るシナリオをエミュレートします。 ドライバーが[**pfnSetErrorCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_seterror_cb)コールバック関数を呼び出すように要求することで、ドライバーから送信されるすべてのエラーに、役に立つコールスタックが関連付けられるようになります。 エラーに関連付けられたコールスタックを使用すると、迅速な診断と正確なワトソン博士ログが有効になります。

特定のドライバー関数に対してランタイムが許可しないエラーコードを返した場合でも、ドライバーのバグまたは問題としてランタイムによって決定されるため、ドライバーコードで[**pfnSetErrorCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_seterror_cb)を使用する必要があります。 ユーザーモードの表示ドライバーで重大なエラーを吸収して続行することは、さらに悪化します。 ユーザーモードの表示ドライバーでは、エラー検出のポイントの近くに**pfnSetErrorCb**を呼び出して、事後分析用に便利な呼び出し履歴を提供する必要があります。

次の表は、Direct3D ランタイムが特定のドライバー関数から許可するエラーのカテゴリを示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">エラーカテゴリ</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>NoErrors</p></td>
<td align="left"><p>ドライバーでは、D3DDDIERR_DEVICEREMOVED を含むエラーは発生しません。 ランタイムは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_seterror_cb" data-raw-source="[&lt;strong&gt;pfnSetErrorCb&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_seterror_cb)"><strong>pfnSetErrorCb</strong></a>へのすべての呼び出しが重要であると判断します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>AllowDeviceRemoved</p></td>
<td align="left"><p>D3DDDIERR_DEVICEREMOVED を除き、ドライバーでエラーが発生することはありません。 ランタイムは、D3DDDIERR_DEVICEREMOVED を渡さない<strong>pfnSetErrorCb</strong>の呼び出しが重要であると判断します。 デバイスが削除されている場合、ドライバーは DEVICEREMOVED を返す必要はありません。 ただし、ランタイムでは、ドライバーが DEVICEREMOVED 盗み見るを使用して DEVICEREMOVED を返すことができます。この場合、通常は発生しません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>AllowOutOfMemory</p></td>
<td align="left"><p>ドライバーのメモリが不足している可能性があります。 このため、ドライバーは<strong>pfnSetErrorCb</strong>経由で E_OUTOFMEMORY と D3DDDIERR_DEVICEREMOVED を渡すことができます。 ランタイムは、他のすべてのエラーコードが重要であると判断します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Allowcounterのエラー</p></td>
<td align="left"><p>ドライバーのメモリが不足している可能性があります。 また、ドライバーは、カウンターが排他的な性質を持つためにカウンターを作成できない場合もあります。 このため、ドライバーは E_OUTOFMEMORY、DXGI_DDI_ERR_NONEXCLUSIVE、および D3DDDIERR_DEVICEREMOVED を<strong>pfnSetErrorCb</strong>経由で渡すことができます。 ランタイムは、他のすべてのエラーコードが重要であると判断します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>AllowMapErrors</p></td>
<td align="left"><p>ドライバーはリソースの競合を確認する必要があります。 このため、ドライバーの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourcemap" data-raw-source="[&lt;strong&gt;ResourceMap&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourcemap)"><strong>Resourcemap</strong></a>関数に D3D10_DDI_MAP_FLAG_DONOTWAIT フラグが渡された場合、ドライバーは<strong>pfnSetErrorCb</strong>を介して DXGI_DDI_ERR_WASSTILLDRAWING を渡すことができます。 ドライバーは、 <strong>pfnSetErrorCb</strong>を介して D3DDDIERR_DEVICEREMOVED を渡すこともできます。 ランタイムは、他のすべてのエラーコードが重要であると判断します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>AllowGetDataErrors</p></td>
<td align="left"><p>ドライバーは、クエリの完了を確認する必要があります。 そのため、クエリがまだ完了していない場合、ドライバーは<strong>pfnSetErrorCb</strong>を介して DXGI_DDI_ERR_WASSTILLDRAWING を渡すことができます。 ドライバーは、 <strong>pfnSetErrorCb</strong>を介して D3DDDIERR_DEVICEREMOVED を渡すこともできます。 ランタイムは、他のすべてのエラーコードが重要であると判断します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>AllowWKCheckCounterErrors</p></td>
<td align="left"><p>ドライバーの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_checkcounter" data-raw-source="[&lt;strong&gt;CheckCounter&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_checkcounter)"><strong>Checkcounter</strong></a>関数は、ランタイム定義のカウンターをサポートしているかどうかを示します。 このため、ドライバーは<strong>pfnSetErrorCb</strong>を介して DXGI_DDI_ERR_UNSUPPORTED を渡すことができます。 ランタイムは、他のすべてのエラーコードが重要であると判断します。</p>
<p>ドライバーは、どのチェック型関数に対しても D3DDDIERR_DEVICEREMOVED を返すことはできません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>AllowDDCheckCounterErrors</p></td>
<td align="left"><p>ドライバーは、デバイス依存カウンター識別子 (カウンター ID) を検証して、カウンター ID が範囲内にあり、各カウンター文字列を指定されたバッファーにコピーするのに十分な空き領域があることを確認する必要があります。 この方法では、パラメーターが正しくない場合、ドライバーは<strong>pfnSetErrorCb</strong>を介して E_INVALIDARG を渡すことができます。</p>
<p>ドライバーは、どのチェック型関数に対しても D3DDDIERR_DEVICEREMOVED を返すことはできません。</p></td>
</tr>
</tbody>
</table>

 

 

 





