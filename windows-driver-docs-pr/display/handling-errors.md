---
title: エラーの処理
description: エラーの処理
ms.assetid: ac4e056e-3304-4934-887a-5cc2b87989bd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7486da413eac637f7f54e03a79a435dd04255dab
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382309"
---
# <a name="handling-errors"></a>エラーの処理


[Direct3D のバージョン 10 関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)の戻り値パラメーターの型 VOID があるユーザー モード ドライバーの実装を通常表示することです。 このルールの主な例外は、 *CalcPrivate***ObjType***サイズ*-関数の入力 (たとえば、 [ **CalcPrivateResourceSize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivateresourcesize)関数)。 この種類の関数は、サイズを返します\_T パラメーターの型を使用して特定のオブジェクト型を作成するため、ドライバーが必要とするメモリ領域のサイズを示す、* 作成 ***ObjType**-type (関数例では、 [ **CreateResource(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource))。

ユーザー モードのディスプレイ ドライバーが従来の方法でエラーの Direct3D ランタイムに通知するを防ぎます VOID を返すこと (つまり、ユーザー モードのディスプレイ ドライバーの関数を返すパラメーター)。 代わりに、ユーザー モードのディスプレイ ドライバーは、Direct3D ランタイムを使用する必要があります[ **pfnSetErrorCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_seterror_cb)にこのような情報をランタイムに渡すコールバック関数。 ランタイムへのポインターを提供するその**pfnSetErrorCb**で、 [ **D3D10DDI\_CORELAYER\_DEVICECALLBACKS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddi_corelayer_devicecallbacks)構造体、 **pUMCallbacks**のメンバー、 [ **D3D10DDIARG\_CREATEDEVICE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice)への呼び出しで指す構造体、 [ **CreateDevice(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)関数。

各ユーザー モードのディスプレイ ドライバーの関数のリファレンス ページを呼び出すことによって渡すことができる関数は、エラーを指定する**pfnSetErrorCb**します。 つまり、ユーザー モード ドライバーの呼び出しを表示する場合**pfnSetErrorCb**エラー条件が重要なし、機能は、現在のユーザー モードのディスプレイ ドライバー関数は許可されていません、エラー コード、ランタイムを決定します適当に。 中に、ランタイムが適切に機能するため、 **pfnSetErrorCb**、呼び出し元の効果を反転することは期待できません**pfnSetErrorCb**(E\_失敗) を呼び出してよう**pfnSetErrorCb**(S\_OK)。 実際には、ランタイムが決定される S\_[ok] は単に無効か、重要な電子メールとして\_失敗します。 S の概念\_[ok] を返すコードは呼び出さないユーザー モードのディスプレイ ドライバー関数に相当**pfnSetErrorCb**まったくです。

Direct3D ランタイム、認識された場合、エラー状態が重要なことはまずかかりますアクション dr 実施時のエラーをログに記録します。ワトソン--事後 (だけの時間) の既定のデバッガーです。 ランタイムは、デバイスをエミュレートする、D3DDDIERR の受信のシナリオのため、意図的に失われます\_DEVICEREMOVED エラー コード。 呼び出すドライバーを要求することによって、 [ **pfnSetErrorCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_seterror_cb)コールバック関数では、可能性は非常に大きいので、ドライバーから送信されたすべてのエラーが関連付けられている便利なコール スタックにあります。 簡易診断を行うと Dr の正確なエラーに関連付けられている呼び出し履歴が有効にします。ワトソン博士を記録します。

使用する必要があります[ **pfnSetErrorCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_seterror_cb)返すエラー コード、ランタイムは関数の特定のドライバーが許可されない場合でも、ドライバーで問題が発生する場合、ドライバーのコードでドライバーのバグまたは問題として、ランタイムによって決定されます。 重大なエラーを吸収してで続行ユーザー モードのディスプレイ ドライバーにも悪いでしょう。 ユーザー モードのディスプレイ ドライバーを呼び出す必要があります**pfnSetErrorCb**近く事後のデバッグに便利なコール スタックを提供する限り、エラー検出のポイント。

次の表は、Direct3D ランタイムにより、特定のドライバーの関数からエラーのカテゴリを一覧表示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">エラー カテゴリ</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>NoErrors</p></td>
<td align="left"><p>ドライバーでは、D3DDDIERR_DEVICEREMOVED などのエラーが発生しない必要があります。 すべての呼び出しに、ランタイムが決定されます<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_seterror_cb" data-raw-source="[&lt;strong&gt;pfnSetErrorCb&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_seterror_cb)"> <strong>pfnSetErrorCb</strong> </a>が重要です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>AllowDeviceRemoved</p></td>
<td align="left"><p>ドライバーでは、D3DDDIERR_DEVICEREMOVED を除く、すべてのエラーが発生しない必要があります。 すべての呼び出しに、ランタイムが決定されます<strong>pfnSetErrorCb</strong> D3DDDIERR_DEVICEREMOVED に合格しないが重要です。 ドライバーは、デバイスが削除されている場合は、DEVICEREMOVED を返す必要はありません。 ただし、ランタイムでは、ドライバー関数は、通常は発生しません干渉 DEVICEREMOVED 場合に返す DEVICEREMOVED、ドライバーができます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>AllowOutOfMemory</p></td>
<td align="left"><p>ドライバーは、メモリ不足実行できます可能性があります。 ドライバー E_OUTOFMEMORY とを通じて D3DDDIERR_DEVICEREMOVED に渡すことができますので、 <strong>pfnSetErrorCb</strong>します。 ランタイムは、その他のエラー コードが重要なことが決定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>AllowCounterCreationErrors</p></td>
<td align="left"><p>ドライバーは、メモリ不足実行できます可能性があります。 ドライバーもできない可能性がありますカウンターの排他的な性質のためのカウンターを作成できません。 ドライバー E_OUTOFMEMORY、DXGI_DDI_ERR_NONEXCLUSIVE、およびを通じて D3DDDIERR_DEVICEREMOVED に渡すことができますので、 <strong>pfnSetErrorCb</strong>します。 ランタイムは、その他のエラー コードが重要なことが決定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>AllowMapErrors</p></td>
<td align="left"><p>ドライバーは、リソースの競合を確認する必要があります。 そのため、ドライバーがを通じて DXGI_DDI_ERR_WASSTILLDRAWING を渡すことができます<strong>pfnSetErrorCb</strong> D3D10_DDI_MAP_FLAG_DONOTWAIT フラグが、ドライバーに渡されたかどうか<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourcemap" data-raw-source="[&lt;strong&gt;ResourceMap&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourcemap)"> <strong>ResourceMap</strong> </a>関数。 ドライバーはを通じて D3DDDIERR_DEVICEREMOVED を渡すことができますも<strong>pfnSetErrorCb</strong>します。 ランタイムは、その他のエラー コードが重要なことが決定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>AllowGetDataErrors</p></td>
<td align="left"><p>ドライバーは、クエリの完了を確認する必要があります。 そのため、ドライバーがを通じて DXGI_DDI_ERR_WASSTILLDRAWING を渡すことができます<strong>pfnSetErrorCb</strong>クエリがまだ完了しない場合。 ドライバーはを通じて D3DDDIERR_DEVICEREMOVED を渡すことができますも<strong>pfnSetErrorCb</strong>します。 ランタイムは、その他のエラー コードが重要なことが決定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>AllowWKCheckCounterErrors</p></td>
<td align="left"><p>ドライバーの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_checkcounter" data-raw-source="[&lt;strong&gt;CheckCounter&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_checkcounter)"> <strong>CheckCounter</strong> </a>関数は、実行時に定義されているカウンターがサポートしているかどうかを示す必要があります。 そのため、ドライバーがを通じて DXGI_DDI_ERR_UNSUPPORTED を渡すことができます<strong>pfnSetErrorCb</strong>します。 ランタイムは、その他のエラー コードが重要なことが決定します。</p>
<p>ドライバーは、任意の型チェック関数の D3DDDIERR_DEVICEREMOVED を返すことはできません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>AllowDDCheckCounterErrors</p></td>
<td align="left"><p>ドライバーは、カウンター ID が範囲内と、各カウンターの文字列を指定されたバッファーにコピーする十分な空き領域があることを確認するには、デバイスに依存するカウンター id (カウンター ID) を検証する必要があります。 ドライバーである E_INVALIDARG を渡すことができます<strong>pfnSetErrorCb</strong>パラメーターがこの方法で正しくない場合、します。</p>
<p>ドライバーは、任意の型チェック関数の D3DDDIERR_DEVICEREMOVED を返すことはできません。</p></td>
</tr>
</tbody>
</table>

 

 

 





