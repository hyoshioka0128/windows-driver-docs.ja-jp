---
title: Direct3D ドライバー コールバックのリターン コード
description: Direct3D ドライバー コールバックのリターン コード
ms.assetid: 033beb6e-5872-4cb3-8f39-459e2fff82cd
keywords:
- Direct3D WDK Windows 2000 の表示、リターンコード
- リターンコード WDK Direct3D
- コールバック WDK Direct3D
- コールバック関数 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc613b7dd8ff8364feaf62ad2eaed252c4659a04
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825826"
---
# <a name="return-codes-for-direct3d-driver-callbacks"></a>Direct3D ドライバー コールバックのリターン コード


## <span id="ddk_return_codes_for_direct3d_driver_callbacks_gg"></span><span id="DDK_RETURN_CODES_FOR_DIRECT3D_DRIVER_CALLBACKS_GG"></span>


次の表は、 [Direct3D ドライバーが提供する関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)によって返される値の一覧です。 DDHAL\_DRIVER\_*Xxx*値は実際には DWORD の戻り値で返されます。 特定の関数のパラメーターがポイントする構造体の**ddrval**メンバーで、D3D\_OK 値、D3DHAL\_*xxx*値、および D3DERR\_*xxx*エラーコードが返されます。

各関数が返すことができる特定のエラーコードについては、「参照」セクションの関数と構造の説明を参照してください。 エラーコードと戻り値の完全な一覧については、「Direct3D *header files* d3d8 and *D3dhal* 」 (DirectX バージョン8.0 および9.0 の場合はと*d3d9* ) を参照してください。 エラーコードは負の値で表されるため、組み合わせることはできません。

Direct3D ドライバーの関数は、DDHAL\_DRIVER\_HANDLED または DDHAL\_DRIVER\_NOTHANDLED の2つのリターンコードのいずれかを返す必要があります。 ドライバーが DDHAL\_ドライバー\_処理された場合は、D3D\_OK か、または d3dhal または*に一覧*表示されているいずれかの値を返す必要があります。 Direct3D ドライバーの関数は、次の表の値を返すことができます。 これらの値は、 *d3d*および*d3dhal*で定義されています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>D3D_OK (DD_OK として定義)</p></td>
<td align="left"><p>要求は正常に完了しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DHAL_CONTEXT_BAD</p></td>
<td align="left"><p>渡されたコンテキストが無効です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DDHAL_DRIVER_HANDLED</p></td>
<td align="left"><p>ドライバーは操作を実行し、ドライバーのコールバックに渡された構造体の<strong>ddrval</strong>メンバーでその操作の有効なリターンコードを返しました。 このコードが D3D_OK の場合、Direct3D は関数を続行します。 それ以外の場合、Direct3D はドライバーによって提供されるエラーコードを返し、関数を中止します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DDHAL_DRIVER_NOTHANDLED</p></td>
<td align="left"><p>ドライバーには、要求された操作に関するコメントがありません。 ドライバーが特定のコールバックを実装する必要がある場合、Direct3D はエラー状態を報告します。 それ以外の場合、direct3d は、Direct3D デバイスに依存しない実装を実行してドライバーコールバックが定義されていないかのように操作を処理します。 通常、Direct3D は、そのコールバックのパラメーター構造の<strong>ddrval</strong>メンバーで返される値を無視します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DHAL_OUTOFCONTEXTS</p></td>
<td align="left"><p>このプロセスにはコンテキストが残っていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DERR_UNSUPPORTEDCOLOROPERATION</p></td>
<td align="left"><p>カラー操作はサポートされていません。</p></td>
</tr>
</tbody>
</table>

 

 

 





