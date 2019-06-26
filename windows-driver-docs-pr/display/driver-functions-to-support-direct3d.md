---
title: Direct3D をサポートするためのドライバー関数
description: Direct3D をサポートするためのドライバー関数
ms.assetid: 949551c3-2172-454c-b398-eba468b90705
keywords:
- Direct3D WDK Windows 2000 の表示、関数
- WDK Direct3D 関数
- WDK Direct3D のコールバック関数
- LPD3DHAL_MYFUNCTIONDATA
- D3DHAL_MYFUNCTIONDATA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32d64ea7b6c1a20f51807a8afc56d6843c7d8d93
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381092"
---
# <a name="driver-functions-to-support-direct3d"></a>Direct3D をサポートするためのドライバー関数


## <span id="ddk_driver_functions_to_support_direct3d_gg"></span><span id="DDK_DRIVER_FUNCTIONS_TO_SUPPORT_DIRECT3D_GG"></span>


Direct3D をサポートするドライバーは、関数コールバック関数の Direct3D、DirectDraw DDI の両方を提供します。 Direct3D DDI コールバックは、次のようにプロトタイプ宣言されて。

```cpp
typedef DWORD (APIENTRY *LPD3DHAL_MYFUNCTIONCB) (LPD3DHAL_MYFUNCTIONDATA);
```

上記の構文。

-   LPD3DHAL\_MYFUNCTIONCB が呼び出すことができるドライバーによって実装されるコールバックを指す*MyFunction*します。 コールバック名はすべて pseudonames ディスプレイ ドライバー作成者によって決定します。

-   LPD3DHAL\_MYFUNCTIONDATA、D3DHAL へのポインターは、\_コールバックに渡される MYFUNCTIONDATA 構造体。 コールバック パラメーター構造体の特徴は次のとおりです。
    -   すべての構造体の最初のメンバー **dwhContext**は、コールバックが動作する 3D のコンテキストを説明するコンテキスト ハンドルです。 このルールの唯一の例外は、D3DHAL\_CONTEXTCREATEDATA 構造体。
    -   すべての構造体の最後のメンバーは**ddrval**します。 このメンバーは、呼び出し元アプリケーションに返せるように Direct3D にコールバックの戻り値を渡すために使用されます。

Direct3D のコールバック関数を初期化する方法を確認するのを参照してください。 [Direct3D ドライバーの初期化](direct3d-driver-initialization.md)します。

次の表には、Direct3D ドライバーに実装されている Direct3D のコールバック関数が一覧表示します。 以外の必要なすべてのコールバック関数[ **D3dValidateTextureStageState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_validatetexturestagestatecb)、これはハードウェア機能に応じて省略可能です。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_contextcreatecb" data-raw-source="[&lt;strong&gt;D3dContextCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_contextcreatecb)"><strong>D3dContextCreate</strong></a></p></td>
<td align="left"><p>コンテキストを作成します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_contextdestroycb" data-raw-source="[&lt;strong&gt;D3dContextDestroy&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_contextdestroycb)"><strong>D3dContextDestroy</strong></a></p></td>
<td align="left"><p>コンテキストを破棄します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex" data-raw-source="[&lt;strong&gt;D3dCreateSurfaceEx&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)"><strong>D3dCreateSurfaceEx</strong></a></p></td>
<td align="left"><p>テクスチャのハンドルと、画面間のアソシエーションを作成します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_destroyddlocal" data-raw-source="[&lt;strong&gt;D3dDestroyDDLocal&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_destroyddlocal)"><strong>D3dDestroyDDLocal</strong></a></p></td>
<td align="left"><p>以前に作成したすべての Direct3D サーフェイスが破棄<a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex" data-raw-source="[&lt;strong&gt;D3dCreateSurfaceEx&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)"> <strong>D3dCreateSurfaceEx</strong> </a>同じに属しているローカルの DirectDraw オブジェクト。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb" data-raw-source="[&lt;strong&gt;D3dDrawPrimitives2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)"><strong>D3dDrawPrimitives2</strong></a></p></td>
<td align="left"><p>プリミティブを描画し、Direct3D に更新された状態を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverstate" data-raw-source="[&lt;strong&gt;D3dGetDriverState&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverstate)"><strong>D3dGetDriverState</strong></a></p></td>
<td align="left"><p>状態 DirectDraw、Direct3D のランタイムにドライバーに関する情報を返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_validatetexturestagestatecb" data-raw-source="[&lt;strong&gt;D3dValidateTextureStageState&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_validatetexturestagestatecb)"><strong>D3dValidateTextureStageState</strong></a></p></td>
<td align="left"><p>テクスチャをサポートするすべてのドライバーに対して必要とされるテクスチャ ステージ ステート検証を実行します。</p></td>
</tr>
</tbody>
</table>

 

Direct3D をサポートするために、ドライバーは Microsoft DirectDraw をサポートする必要が最小限とも、特定の DirectDraw DDI 関数を実装する必要があります。 Direct3D のサポートに関連の関数は、次の表に一覧表示されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgetdirectdrawinfo" data-raw-source="[&lt;strong&gt;DrvGetDirectDrawInfo&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgetdirectdrawinfo)"><strong>DrvGetDirectDrawInfo</strong></a></p></td>
<td align="left"><p>この関数は、グラフィックス ハードウェアの機能を取得します。 この初期化関数では、ドライバーは、Direct3D をサポートしていることを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo" data-raw-source="[&lt;strong&gt;DdGetDriverInfo&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)"><strong>DdGetDriverInfo</strong></a></p></td>
<td align="left"><p>ランタイムは、このコールバック関数を Guid の詳細については、ドライバーを照会します。 ドライバーの Direct3D のサポートに特有のいくつかの Guid。</p></td>
</tr>
</tbody>
</table>

 

DirectDraw 関数とコールバックの実装の詳細については、 [DirectDraw](directdraw.md)します。

 

 





