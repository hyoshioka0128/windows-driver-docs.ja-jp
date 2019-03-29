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
ms.openlocfilehash: 592b5fa84f0fe0e99ea7234c9e78cef3a6d80ddb
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350379"
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

次の表には、Direct3D ドライバーに実装されている Direct3D のコールバック関数が一覧表示します。 以外の必要なすべてのコールバック関数[ **D3dValidateTextureStageState**](https://msdn.microsoft.com/library/windows/hardware/ff549064)、これはハードウェア機能に応じて省略可能です。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542178" data-raw-source="[&lt;strong&gt;D3dContextCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542178)"><strong>D3dContextCreate</strong></a></p></td>
<td align="left"><p>コンテキストを作成します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542180" data-raw-source="[&lt;strong&gt;D3dContextDestroy&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542180)"><strong>D3dContextDestroy</strong></a></p></td>
<td align="left"><p>コンテキストを破棄します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542840" data-raw-source="[&lt;strong&gt;D3dCreateSurfaceEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542840)"><strong>D3dCreateSurfaceEx</strong></a></p></td>
<td align="left"><p>テクスチャのハンドルと、画面間のアソシエーションを作成します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff544685" data-raw-source="[&lt;strong&gt;D3dDestroyDDLocal&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544685)"><strong>D3dDestroyDDLocal</strong></a></p></td>
<td align="left"><p>以前に作成したすべての Direct3D サーフェイスが破棄<a href="https://msdn.microsoft.com/library/windows/hardware/ff542840" data-raw-source="[&lt;strong&gt;D3dCreateSurfaceEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542840)"> <strong>D3dCreateSurfaceEx</strong> </a>同じに属しているローカルの DirectDraw オブジェクト。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff544704" data-raw-source="[&lt;strong&gt;D3dDrawPrimitives2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544704)"><strong>D3dDrawPrimitives2</strong></a></p></td>
<td align="left"><p>プリミティブを描画し、Direct3D に更新された状態を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff544708" data-raw-source="[&lt;strong&gt;D3dGetDriverState&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544708)"><strong>D3dGetDriverState</strong></a></p></td>
<td align="left"><p>状態 DirectDraw、Direct3D のランタイムにドライバーに関する情報を返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549064" data-raw-source="[&lt;strong&gt;D3dValidateTextureStageState&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549064)"><strong>D3dValidateTextureStageState</strong></a></p></td>
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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556229" data-raw-source="[&lt;strong&gt;DrvGetDirectDrawInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556229)"><strong>DrvGetDirectDrawInfo</strong></a></p></td>
<td align="left"><p>この関数は、グラフィックス ハードウェアの機能を取得します。 この初期化関数では、ドライバーは、Direct3D をサポートしていることを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549404" data-raw-source="[&lt;strong&gt;DdGetDriverInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549404)"><strong>DdGetDriverInfo</strong></a></p></td>
<td align="left"><p>ランタイムは、このコールバック関数を Guid の詳細については、ドライバーを照会します。 ドライバーの Direct3D のサポートに特有のいくつかの Guid。</p></td>
</tr>
</tbody>
</table>

 

DirectDraw 関数とコールバックの実装の詳細については、 [DirectDraw](directdraw.md)します。

 

 





