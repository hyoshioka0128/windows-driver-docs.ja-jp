---
title: DirectDraw の値を返す
description: DirectDraw の値を返す
ms.assetid: da4cc7d7-6826-48aa-96c6-004e31fc3e3e
keywords:
- WDK DirectDraw の値を返す
- WDK DirectDraw を描画するには、戻り値
- DirectDraw WDK Windows 2000 の表示、戻り値
- エラー WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97d48e53198895471f1dd06b011f885ad5682c3d
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349497"
---
# <a name="return-values-for-directdraw"></a>DirectDraw の値を返す


## <span id="ddk_return_values_for_directdraw_gg"></span><span id="DDK_RETURN_VALUES_FOR_DIRECTDRAW_GG"></span>


によって返されるリストの値を以下に、 [DirectDraw ドライバーによって提供される関数](https://msdn.microsoft.com/library/windows/hardware/ff553833)します。 DDHAL\_ドライバー\_*Xxx*実際に値が DWORD の戻り値で返されます。 DD\_[ok] の値と DDERR\_*Xxx*で返されるエラー コード、 **ddRVal**特定の関数のパラメーターが指す構造体のメンバー。

各関数が返すことができる特定のエラー コード、リファレンス セクションでは、関数の説明を参照してください。 DirectDraw ヘッダー ファイルを参照してください*ddraw.h*と*dxmini.h*エラー コードと戻り値の完全な一覧についてはします。 エラー コードは負の値で表され、組み合わせることはできませんに注意してください。

DirectDraw ドライバー内の関数は、2 つのリターン コードのいずれかを返す必要があります。DDHAL\_ドライバー\_処理済みまたは DDHAL\_ドライバー\_NOTHANDLED します。 ドライバーが DDHAL を返す場合\_ドライバー\_DD のいずれかを返すことも必要があり、処理\_[ok] またはいずれかのエラー コードが記載*ddraw.h*します。 DirectDraw ドライバーの関数は、次の表に、コードを返すことができます。 これらのコードが定義されている*ddraw.h*します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">リターン コード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DD_OK</p></td>
<td align="left"><p>要求は正常に完了しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DDHAL_DRIVER_HANDLED</p></td>
<td align="left"><p>ドライバーが操作を実行し、その操作に有効なリターン コードが返されます、 <strong>ddrval</strong>構造体のメンバー、ドライバーのコールバックに渡されます。 このコードが DD_OK の場合は、DirectDraw または Direct3D 関数を実行します。 それ以外の場合、DirectDraw または Direct3D、ドライバーによって提供されるエラー コードを返し、関数を中止します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DDHAL_DRIVER_NOCKEYHW</p></td>
<td align="left"><p>ディスプレイ ドライバーは、色の主要なハードウェア リソースが不足しているため、呼び出しを処理できませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DDHAL_DRIVER_NOTHANDLED</p></td>
<td align="left"><p>要求された操作には、ドライバーのコメントはありません。 ドライバーは、特定のコールバックを実装する必要は、DirectDraw または Direct3D では、エラー状態が報告します。 それ以外の場合、DirectDraw または Direct3D デバイスに依存しない実装を実行することによって、ドライバーのコールバックが定義されていなかった場合に DirectDraw または Direct3D、操作を処理しています。 通常に返される値を無視 DirectDraw、Direct3D、 <strong>ddrval</strong>そのコールバックのパラメーター構造体のメンバー。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DDERR_GENERIC</p></td>
<td align="left"><p>未定義のエラー条件があります。</p></td>
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

 

A [DxApi 関数](https://msdn.microsoft.com/library/windows/hardware/ff557387)で実装される、[ビデオのミニポート ドライバー](video-miniport-drivers-in-the-windows-2000-display-driver-model.md)次の表に、コードのいずれかを返します。 これらのコードが定義されている*dxmini.h*します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">リターン コード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DX_OK</p></td>
<td align="left"><p>要求は正常に完了しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXERR_GENERIC</p></td>
<td align="left"><p>未定義のエラー条件があります。</p></td>
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

 

 

 





