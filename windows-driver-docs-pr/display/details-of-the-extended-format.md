---
title: 拡張形式の詳細
description: 拡張形式の詳細
ms.assetid: e9cd2bc7-99c1-4aca-91b0-9faefa4a856d
keywords:
- Direct3D バージョン 10.1 WDK Windows 7 display、extended format
- 拡張形式 WDK Windows 7 ディスプレイ
ms.date: 09/10/2019
ms.localizationpriority: medium
ms.openlocfilehash: 8d541aed1f35894a3cd71779babb17cf038a02fa
ms.sourcegitcommit: 14a1868c1009fcbac5cf6dfeb844f4c712212f23
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71317531"
---
# <a name="details-of-the-extended-format"></a>拡張形式の詳細

このセクションは、Windows 7 以降のオペレーティングシステムにのみ適用されます。

次の表では、フォーマット名の XR 部分は、UNORM またはシントに類似したビットの新しいシェーダー解釈と見なすことができます。 形式名\_の XR バイアス部分は、この解釈のセマンティックを追加のメタデータと共にオーバーロードする特殊なケースです。 このメタデータは、シェーダーとの間の遷移のシェーダーコードで、明示的にオフセットおよびバイアスする必要があることを示します。 ドライバーは、このような双方向の作業を実行する必要はありません。アプリケーション全体に残されます。

## <a name="table-of-extended-formats"></a>拡張形式の表

次の表は、拡張形式を使用する特定の属性を持つリソース (DXGI_FORMAT_ *) を示しています。これらの属性を持つリソースに対して、ハードウェアでこれらの拡張形式がサポートされている場合、またはこれらのリソースの拡張形式がオプションである場合に使用されます。 各形式の説明については、「 [DXGI_FORMAT](https://docs.microsoft.com/windows/win32/api/dxgiformat/ne-dxgiformat-dxgi_format) 」を参照してください。

次の表の列キー:

- **A**:DXGI_FORMAT_B8G8R8A8_TYPELESS
- **B**:DXGI_FORMAT_B8G8R8A8_UNORM (既存)
- **C**:DXGI_FORMAT_B8G8R8A8_UNORM_SRGB
- **D**:DXGI_FORMAT_B8G8R8X8_TYPELESS
- **E**:DXGI_FORMAT_B8G8R8X8_UNORM (既存)
- **F**:DXGI_FORMAT_B8G8R8X8_UNORM_SRGB
- **G**:DXGI_FORMAT_R10G10B10A2_TYPELESS
- **H**:DXGI_FORMAT_R10G10B10_XR_BIAS_A2_UNORM

<table>
<head>
    <tr>
        <th>リソース属性</th>
        <th>A</th>
        <th>B</th>
        <th>c</th>
        <th>D</th>
        <th>E</th>
        <th>F</th>
        <th>G</th>
        <th>H</th>
    </tr>
</head>
<body>
    <tr>
        <td>バッファー</td>
        <td>なし</td>
        <td>R (変更済み)</td>
        <td>なし</td>
        <td>なし</td>
        <td>R (変更済み)</td>
        <td>なし</td>
        <td>なし</td>
        <td>なし</td>
    </tr>
    <tr>
        <td>入力アセンブラー頂点バッファー</td>
        <td>なし</td>
        <td>R (変更済み)</td>
        <td>なし</td>
        <td>なし</td>
        <td>R (変更済み)</td>
        <td>なし</td>
        <td>なし</td>
        <td>なし</td>
    </tr>
    <tr>
        <td>Texture1D</td>
        <td>R</td>
        <td>R (変更済み)</td>
        <td>R</td>
        <td>R</td>
        <td>R (変更済み)</td>
        <td>R</td>
        <td>R</td>
        <td>なし</td>
    </tr>
    <tr>
        <td>Texture2D</td>
        <td>R</td>
        <td>R (変更済み)</td>
        <td>R</td>
        <td>R</td>
        <td>R</td>
        <td>R</td>
        <td>R</td>
        <td>R</td>
    </tr>    <tr>
        <td>Texture3D</td>
        <td>R</td>
        <td>R (変更済み)</td>
        <td>R</td>
        <td>R</td>
        <td>R (変更済み)</td>
        <td>R</td>
        <td>R</td>
        <td>なし</td>
    </tr>
    <tr>
        <td>テクスチャキューブ</td>
        <td>R</td>
        <td>R (変更済み)</td>
        <td>R</td>
        <td>R</td>
        <td>R (変更済み)</td>
        <td>R</td>
        <td>R</td>
        <td>なし</td>
    </tr>
    <tr>
        <td>シェーダー ID</td>
        <td>なし</td>
        <td>R</td>
        <td>R</td>
        <td>なし</td>
        <td>R</td>
        <td>R</td>
        <td>なし</td>
        <td>なし</td>
    </tr>
    <tr>
        <td>シェーダーのサンプル (任意のフィルター)</td>
        <td>なし</td>
        <td>R</td>
        <td>R</td>
        <td>なし</td>
        <td>R</td>
        <td>R</td>
        <td>なし</td>
        <td>なし</td>
    </tr>
    <tr>
        <td>MIP-マップテクスチャ</td>
        <td>R</td>
        <td>R (変更済み)</td>
        <td>R</td>
        <td>R</td>
        <td>R (変更済み)</td>
        <td>R</td>
        <td>R</td>
        <td>なし</td>
    </tr>
    <tr>
        <td>MIP マップ自動生成</td>
        <td>なし</td>
        <td>R (変更済み)</td>
        <td>R</td>
        <td>なし</td>
        <td>R (変更済み)</td>
        <td>R</td>
        <td>なし</td>
        <td>なし</td>
    </tr>
    <tr>
        <td>レンダーターゲット</td>
        <td>なし</td>
        <td>R</td>
        <td>R</td>
        <td>なし</td>
        <td>R</td>
        <td>R</td>
        <td>なし</td>
        <td>なし</td>
    </tr>
    <tr>
        <td>Blendable レンダーターゲット</td>
        <td>なし</td>
        <td>R</td>
        <td>R</td>
        <td>なし</td>
        <td>R</td>
        <td>R</td>
        <td>なし</td>
        <td>なし</td>
    </tr>
    <tr>
        <td>CPU のロック可能</td>
        <td>R</td>
        <td>R</td>
        <td>R</td>
        <td>R</td>
        <td>R</td>
        <td>R</td>
        <td>R</td>
        <td>R</td>
    </tr>
    <tr>
        <td>複数サンプルのレンダーターゲット</td>
        <td>なし</td>
        <td>O</td>
        <td>O</td>
        <td>なし</td>
        <td>O</td>
        <td>O</td>
        <td>なし</td>
        <td>なし</td>
    </tr>
    <tr>
        <td>複数サンプルの解決</td>
        <td>なし</td>
        <td>R (変更済み)</td>
        <td>R</td>
        <td>なし</td>
        <td>R (変更済み)</td>
        <td>R</td>
        <td>なし</td>
        <td>なし</td>
    </tr>
    <tr>
        <td>複数サンプルの負荷</td>
        <td>なし</td>
        <td>R</td>
        <td>R</td>
        <td>なし</td>
        <td>R</td>
        <td>R</td>
        <td>なし</td>
        <td>なし</td>
    </tr>
    <tr>
        <td>スキャンアウトを表示する</td>
        <td>なし</td>
        <td>R (変更済み)</td>
        <td>R</td>
        <td>なし</td>
        <td>なし</td>
        <td>なし</td>
        <td>なし</td>
        <td>R</td>
    </tr>
    <tr>
        <td>ビットレイアウト内でのキャスト</td>
        <td>R</td>
        <td>R (変更済み)</td>
        <td>R</td>
        <td>R</td>
        <td>R</td>
        <td>R</td>
        <td>R</td>
        <td>R</td>
    </tr>
</body>
</table>

>[!NOTE]
>上の表では、セルエントリの意味は次のとおりです。
>
>- "R" は、ハードウェアのサポートが必要であることを示します。
>- "o" は、ハードウェアのサポートが省略可能であることを示します。
>- N/A は、リソース属性が拡張形式に適用されない、または拡張形式が許可されていないことを示します。

>[!NOTE]
>\_\_\_Dxgi 形式\_の\_B8G8R8A8 unorm 形式と dxgi 形式の B8G8R8X8 unorm 形式は、既に dxgi 形式の列挙に存在しています。\_\_ ただし、これらのメンバーは、適切な新しいファミリのメンバーと見なされるようになりました。 これらの要件は、元の定義と比較して変更されています。

>[!NOTE]
>読みやすくするために、"入力アセンブラーインデックスバッファー"、\_"シェーダーのサンプル c (比較フィルター)"、"シェーダーのサンプル (mono 1 ビットフィルター)"、"shader gather4"、および "奥行-ステンシルターゲット" の行は、前の表には含まれていません。 これらのリソース属性のすべての意味は、"N/A" です。

次のセクションでは、新しい拡張形式の詳細について説明します。

[XR レイアウト](xr-layout.md)

[XR のアルファコンテンツの書式設定](xr-format-alpha-content.md)

[DXGI\_形式\_R10G10B10XR\_バイアス\_A2UNORM\_\_](dxgi-format-r10g10b10-xr-bias-a2-unorm.md)

[XR 形式のキャスト機能](casting-ability-of-xr-formats.md)

[XR\_バイアスカラーチャネル変換ルール](xr-bias-color-channel-conversion-rules.md)

[X チャネルの解釈](interpretation-of-x-channel.md)
