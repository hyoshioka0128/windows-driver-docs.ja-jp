---
title: Direct3D ドライバー コールバックのリターン コード
description: Direct3D ドライバー コールバックのリターン コード
ms.assetid: 033beb6e-5872-4cb3-8f39-459e2fff82cd
keywords:
- Direct3D WDK Windows 2000 の表示、リターン コード
- リターン コード WDK Direct3D
- WDK Direct3D のコールバック
- WDK Direct3D のコールバック関数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecbec2faa083aefec43c830027915d2a5ddcbbdd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331284"
---
# <a name="return-codes-for-direct3d-driver-callbacks"></a>Direct3D ドライバー コールバックのリターン コード


## <span id="ddk_return_codes_for_direct3d_driver_callbacks_gg"></span><span id="DDK_RETURN_CODES_FOR_DIRECT3D_DRIVER_CALLBACKS_GG"></span>


次の表に、によって返される値、 [Direct3D Driver-Supplied 関数](https://msdn.microsoft.com/library/windows/hardware/ff552859)します。 DDHAL\_ドライバー\_*Xxx*実際に値が DWORD の戻り値で返されます。 D3D\_[ok] の値、D3DHAL\_*Xxx*値、および D3DERR\_*Xxx*で返されるエラー コード、 **ddrval**のメンバー、特定の関数のパラメーターが指す構造体。

各関数が返すことができる特定のエラー コード、リファレンス セクションでは関数と構造体の説明を参照してください。 Direct3D のヘッダー ファイルを参照してください*d3d.h*と*d3dhal.h*エラー コードと戻り値の完全な一覧について (また、 *d3d8.h*と*d3d9.h*8.0、9.0、DirectX のバージョン)。 エラー コードは負の値で表され、組み合わせることはできませんに注意してください。

Direct3D ドライバー内の関数は、2 つのリターン コードのいずれかを返す必要があります。DDHAL\_ドライバー\_処理済みまたは DDHAL\_ドライバー\_NOTHANDLED します。 ドライバーが DDHAL を返す場合\_ドライバー\_D3D のいずれかを返すことも必要があり、処理\_[ok] またはいずれかに記載した値*d3d.h*または*d3dhal.h*します。 Direct3D ドライバーの関数は、次の表に、値を返すことができます。 これらの値が定義されている*d3d.h*と*d3dhal.h*します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値</th>
<th align="left">説明</th>
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
<td align="left"><p>ドライバーが操作を実行し、その操作に有効なリターン コードが返されます、 <strong>ddrval</strong>構造体のメンバー、ドライバーのコールバックに渡されます。 このコードが D3D_OK の場合は、Direct3D は、関数を実行します。 それ以外の場合、Direct3D は、ドライバーによって提供されるエラー コードを返し、関数を中止します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DDHAL_DRIVER_NOTHANDLED</p></td>
<td align="left"><p>要求された操作には、ドライバーのコメントはありません。 ドライバーは、特定のコールバックを実装する必要は、Direct3D は、エラー状態を報告します。 それ以外の場合、Direct3D では、Direct3D デバイスに依存しない実装を実行することによって、ドライバーのコールバックが定義されていなかった場合と同様に、操作が処理します。 Direct3D で返される値を通常は無視、 <strong>ddrval</strong>そのコールバックのパラメーター構造体のメンバー。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DHAL_OUTOFCONTEXTS</p></td>
<td align="left"><p>このプロセスの複数のコンテキストがありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DERR_UNSUPPORTEDCOLOROPERATION</p></td>
<td align="left"><p>色の操作がサポートされていません。</p></td>
</tr>
</tbody>
</table>

 

 

 





