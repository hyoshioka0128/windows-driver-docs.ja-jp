---
title: DirectDraw の値を返す
description: DirectDraw の値を返す
ms.assetid: da4cc7d7-6826-48aa-96c6-004e31fc3e3e
keywords:
- 戻り値 (WDK DirectDraw)
- WDK DirectDraw の描画、戻り値
- DirectDraw WDK Windows 2000 display、戻り値
- エラー WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba99c2d0e57d6521b9cb167fcccbdf6e6ffbf073
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829566"
---
# <a name="return-values-for-directdraw"></a>DirectDraw の値を返す


## <span id="ddk_return_values_for_directdraw_gg"></span><span id="DDK_RETURN_VALUES_FOR_DIRECTDRAW_GG"></span>


次の表は、 [DirectDraw ドライバーが提供する関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)によって返される値を示しています。 DDHAL\_DRIVER\_*Xxx*値は実際には DWORD の戻り値で返されます。 特定の関数のパラメーターが指す構造の**Dderr**メンバーでは、DD\_OK 値と DDERR\_*Xxx*エラーコードが返されます。

各関数が返すことができる特定のエラーコードについては、「参照」セクションの関数の説明を参照してください。 エラーコードと戻り値の完全な一覧については、DirectDraw ヘッダーファイル*ddraw*と*dxmini .h*を参照してください。 エラーコードは負の値で表されるため、組み合わせることはできません。

DirectDraw ドライバーの関数は、DDHAL\_DRIVER\_HANDLED または DDHAL\_DRIVER\_NOTHANDLED の2つのリターンコードのいずれかを返す必要があります。 ドライバーが DDHAL\_ドライバー\_処理された場合は、DD\_OK または*ddraw*に示されているエラーコードのいずれかを返す必要もあります。 DirectDraw ドライバーの関数は、次の表に示すコードを返すことができます。 これらのコードは*ddraw*で定義されています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">リターンコード</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DD_OK</p></td>
<td align="left"><p>要求は正常に完了しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DDHAL_DRIVER_HANDLED</p></td>
<td align="left"><p>ドライバーは操作を実行し、ドライバーのコールバックに渡された構造体の<strong>ddrval</strong>メンバーでその操作の有効なリターンコードを返しました。 このコードが DD_OK の場合、DirectDraw または Direct3D は関数を続行します。 それ以外の場合、DirectDraw または Direct3D はドライバーによって提供されるエラーコードを返し、関数を中止します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DDHAL_DRIVER_NOCKEYHW</p></td>
<td align="left"><p>カラーキーハードウェアリソースが不足しているため、表示ドライバーは通話を処理できませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DDHAL_DRIVER_NOTHANDLED</p></td>
<td align="left"><p>ドライバーには、要求された操作に関するコメントがありません。 ドライバーが特定のコールバックを実装する必要がある場合、DirectDraw または Direct3D はエラー状態を報告します。 それ以外の場合、directdraw または Direct3D は、DirectDraw または Direct3D デバイスに依存しない実装を実行して、ドライバーコールバックが定義されていないかのように操作を処理します。 通常、DirectDraw と Direct3D は、そのコールバックのパラメーター構造の<strong>ddrval</strong>メンバーで返される値を無視します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DDERR_GENERIC</p></td>
<td align="left"><p>未定義のエラー条件が発生しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DDERR_OUTOFCAPS</p></td>
<td align="left"><p>要求された操作に必要なハードウェアが既に割り当てられています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DDERR_UNSUPPORTED</p></td>
<td align="left"><p>この操作はサポートされていません。</p></td>
</tr>
</tbody>
</table>

 

[ビデオミニポートドライバー](video-miniport-drivers-in-the-windows-2000-display-driver-model.md)に実装されている[dxapi 関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)は、次の表に示すいずれかのコードを返します。 これらのコードは、 *dxmini .h*で定義されています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">リターンコード</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DX_OK</p></td>
<td align="left"><p>要求は正常に完了しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXERR_GENERIC</p></td>
<td align="left"><p>未定義のエラー条件が発生しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DXERR_OUTOFCAPS</p></td>
<td align="left"><p>要求された操作に必要なハードウェアが既に割り当てられています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXERR_UNSUPPORTED</p></td>
<td align="left"><p>この操作はサポートされていません。</p></td>
</tr>
</tbody>
</table>

 

 

 





