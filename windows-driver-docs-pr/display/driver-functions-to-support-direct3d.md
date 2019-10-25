---
title: Direct3D をサポートするためのドライバー関数
description: Direct3D をサポートするためのドライバー関数
ms.assetid: 949551c3-2172-454c-b398-eba468b90705
keywords:
- Direct3D WDK Windows 2000 display、functions
- functions WDK Direct3D
- コールバック関数 WDK Direct3D
- LPD3DHAL_MYFUNCTIONDATA
- D3DHAL_MYFUNCTIONDATA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f54e86d123eab83b72ff508c1b88bd70e885c67
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838987"
---
# <a name="driver-functions-to-support-direct3d"></a>Direct3D をサポートするためのドライバー関数


## <span id="ddk_driver_functions_to_support_direct3d_gg"></span><span id="DDK_DRIVER_FUNCTIONS_TO_SUPPORT_DIRECT3D_GG"></span>


Direct3D をサポートするドライバーは、Direct3D コールバック関数と DirectDraw DDI 関数の両方を提供します。 Direct3D DDI コールバックは、次のようにプロトタイプが宣言されています。

```cpp
typedef DWORD (APIENTRY *LPD3DHAL_MYFUNCTIONCB) (LPD3DHAL_MYFUNCTIONDATA);
```

上記の構文では、次のようになります。

-   LPD3DHAL\_MYFUNCTIONCB は、 *MyFunction*と呼ばれるドライバーによって実装されるコールバックを指します。 すべてのコールバック名は、ディスプレイドライバーのライターによって pseudonames 決定されます。

-   LPD3DHAL\_MYFUNCTIONDATA は、コールバックに渡される D3DHAL\_MYFUNCTIONDATA 構造体へのポインターです。 コールバックパラメーター構造の特性は次のとおりです。
    -   すべての構造の最初のメンバーである**Dwhcontext**は、コールバックが動作する必要がある3d コンテキストを記述するコンテキストハンドルです。 この規則の唯一の例外は、D3DHAL\_CONTEXTCREATEDATA 構造体です。
    -   すべての構造体の最後のメンバーは**ddrval**です。 このメンバーは、コールバックの戻り値を Direct3D に渡すために使用されます。これにより、呼び出し元のアプリケーションに返すことができます。

Direct3D のコールバック関数を初期化する方法を確認するには、「 [Direct3d ドライバーの初期化](direct3d-driver-initialization.md)」を参照してください。

次の表は、Direct3D ドライバーに実装されている Direct3D コールバック関数の一覧です。 [**D3dValidateTextureStageState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_validatetexturestagestatecb)を除き、すべてのコールバック関数が必要です。これは、ハードウェアの機能によっては省略可能です。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_contextcreatecb" data-raw-source="[&lt;strong&gt;D3dContextCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_contextcreatecb)"><strong>D3dContextCreate</strong></a></p></td>
<td align="left"><p>コンテキストを作成します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_contextdestroycb" data-raw-source="[&lt;strong&gt;D3dContextDestroy&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_contextdestroycb)"><strong>D3dContextDestroy</strong></a></p></td>
<td align="left"><p>コンテキストを破棄します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex" data-raw-source="[&lt;strong&gt;D3dCreateSurfaceEx&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)"><strong>D3dCreateSurfaceEx</strong></a></p></td>
<td align="left"><p>テクスチャハンドルとサーフェイスの関連付けを作成します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_destroyddlocal" data-raw-source="[&lt;strong&gt;D3dDestroyDDLocal&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_destroyddlocal)"><strong>D3dDestroyDDLocal</strong></a></p></td>
<td align="left"><p>指定されたローカル DirectDraw オブジェクトに属する<a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex" data-raw-source="[&lt;strong&gt;D3dCreateSurfaceEx&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)"><strong>D3dCreateSurfaceEx</strong></a>によって以前に作成されたすべての Direct3D サーフェイスを破棄します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb" data-raw-source="[&lt;strong&gt;D3dDrawPrimitives2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)"><strong>D3dDrawPrimitives2</strong></a></p></td>
<td align="left"><p>プリミティブをレンダリングし、更新された状態を Direct3D に返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverstate" data-raw-source="[&lt;strong&gt;D3dGetDriverState&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverstate)"><strong>D3dGetDriverState</strong></a></p></td>
<td align="left"><p>ドライバーに関する状態情報を DirectDraw および Direct3D ランタイムに返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_validatetexturestagestatecb" data-raw-source="[&lt;strong&gt;D3dValidateTextureStageState&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_validatetexturestagestatecb)"><strong>D3dValidateTextureStageState</strong></a></p></td>
<td align="left"><p>テクスチャステージ状態の検証を実行します。これは、テクスチャ処理をサポートするすべてのドライバーに必要です。</p></td>
</tr>
</tbody>
</table>

 

Direct3D をサポートするには、ドライバーが Microsoft DirectDraw を最小限にサポートし、特定の DirectDraw DDI 機能も実装する必要があります。 次の表に、Direct3D のサポートに関連する関数を示します。

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
<td align="left"><p>この関数は、グラフィックスハードウェアの機能を取得します。 この初期化関数では、ドライバーは Direct3D をサポートしていることを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo" data-raw-source="[&lt;strong&gt;DdGetDriverInfo&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)"><strong>DdGetDriverInfo</strong></a></p></td>
<td align="left"><p>ランタイムは、このコールバック関数に対して、ドライバーに関する追加情報の Guid を照会します。 いくつかの Guid は、ドライバーの Direct3D サポートに特に関連しています。</p></td>
</tr>
</tbody>
</table>

 

Directdraw の関数とコールバックの実装の詳細については、「 [directdraw](directdraw.md)」をご確認ください。

 

 





