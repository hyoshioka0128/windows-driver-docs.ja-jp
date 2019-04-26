---
title: 拡張形式の詳細
description: 拡張形式の詳細
ms.assetid: e9cd2bc7-99c1-4aca-91b0-9faefa4a856d
keywords:
- 拡張形式、Direct3D バージョン 10.1 WDK Windows 7 表示
- Windows 7 の WDK の形式の表示を拡張
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a1983f4c5acfde48a2051a00e450df326ab3187
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348833"
---
# <a name="details-of-the-extended-format"></a>拡張形式の詳細


このセクションでは、Windows 7 およびそれ以降のオペレーティング システムにのみ適用されます。

次の表に、形式名の XR 一部見なすことができます UNORM やシント ・ ビットの新しいシェーダー解釈します。 XR\_形式名の一部をバイアスは特殊なケースでこの解釈のセマンティクスを追加のメタデータをオーバー ロードします。 このメタデータことを示します形式する必要がありますが明示的にオフセット シェーダーとの間の遷移でシェーダー コードのバイアスします。 ドライバーはこの biasing 作業を実行する必要はありません。アプリケーションにそのままです。

次の表には、ハードウェアは、これらの属性を含むリソースのこれらの拡張形式をサポートしているかは、それらのリソースに省略可能な形式を拡張する場合は、拡張の形式を使用する特定の属性を持つリソースが表示されます。

書式設定 (DXGI\_形式\_\*) B8G8R8A8 B8G8R8A8 B8G8R8X8 B8G8R8X8 R10G10B10 リソース B8G8R8A8 \_UNORM \_UNORM B8G8R8X8 \_UNORM \_UNORM R10G10B10A2 \_XR\_バイアス属性\_(既存) TYPELESS \_SRGB \_(既存) TYPELESS \_SRGB \_TYPELESS \_A2\_UNORM バッファー

なし

R

(変更)

なし

なし

R

(変更)

なし

なし

なし

入力

アセンブラー

頂点

バッファー

なし

R

(変更)

なし

なし

R

(変更)

なし

なし

なし

Texture1D

R

R

(変更)

R

R

R

(変更)

R

R

なし

Texture2D

R

R

(変更)

R

R

R

R

R

R

Texture3D

R

R

(変更)

R

R

R

(変更)

R

R

なし

テクスチャ

Cube

R

R

(変更)

R

R

R

(変更)

R

R

なし

シェーダーの ID

なし

R

R

なし

R

R

なし

なし

シェーダー

サンプル

(フィルター)

なし

R

R

なし

R

R

なし

なし

MIP マップ

テクスチャ

R

R

(変更)

R

R

R

(変更)

R

R

なし

MIP マップ

自動-

生成

なし

R

(変更)

R

なし

R

(変更)

R

なし

なし

Render

対象

なし

R

R

なし

R

R

なし

なし

Blendable

Render

対象

なし

R

R

なし

R

R

なし

なし

CPU

Lockable

R

R

R

R

R

R

R

R

マルチ

サンプル

Render

対象

なし

O

O

なし

O

O

なし

なし

マルチ

サンプル

解決

なし

R

(変更)

R

なし

R

(変更)

R

なし

なし

マルチ

サンプル

Load

なし

R

R

なし

R

R

なし

なし

ディスプレイ

スキャンします。

なし

R

(変更)

R

なし

なし

なし

なし

R

キャスト

ビット内

レイアウト

R

R

(変更)

R

R

R

R

R

R

 

**注**  上の表では、セルのエントリは次の意味を持ちます。
-   "R"では、ハードウェアのサポートが必要であることを示します

-   "o"は、ハードウェアのサポートが省略可能であることを示します

-   該当なしリソース属性拡張の形式には適用されません、またはを示します拡張形式を許可しません。

 

**注**   、DXGI\_形式\_B8G8R8A8\_UNORM と DXGI\_形式\_B8G8R8X8\_UNORM 形式は、DXGI に既に存在していた\_形式の列挙体です。 ただし、適切な新しいファミリのメンバー、今すぐと見なされます。 要件は、元の定義の比較対象に変更されました。

 

**注**   "入力アセンブラー インデックス バッファーに"行"シェーダー サンプル\_c (フィルターの比較)"、"シェーダー sample (mono 1 ビット フィルター)"、"シェーダー gather4"および「深度ステンシルのターゲット」リソースの属性には含まれません読みやすくするため、前の表。 これらのリソース属性のすべての意味は、該当なしです。

 

次のセクションでは、新しい拡張形式の詳細について説明します。

[XR レイアウト](xr-layout.md)

[XR 形式のアルファ コンテンツ](xr-format-alpha-content.md)

[DXGI\_形式\_R10G10B10\_XR\_バイアス\_A2\_UNORM](dxgi-format-r10g10b10-xr-bias-a2-unorm.md)

[XR 形式のキャスト機能](casting-ability-of-xr-formats.md)

[XR\_バイアス カラー チャネルの変換規則](xr-bias-color-channel-conversion-rules.md)

[チャネル X の解釈](interpretation-of-x-channel.md)

 

 





