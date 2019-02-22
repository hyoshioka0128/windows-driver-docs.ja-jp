---
title: 形式の対応要件の拡張
description: 形式の対応要件の拡張
ms.assetid: eab9c254-fca7-449d-a6cf-1b20d2e7173c
keywords:
- 拡張形式の対応要件 Direct3D バージョン 10.1 WDK Windows 7 表示
- 拡張形式の対応要件 WDK Windows 7 の表示
- XR_BIAS WDK Windows 7 の表示
- XR_BIAS WDK Windows 7 の表示、PresentDXGI
- XR_BIAS WDK Windows 7 の表示、BltDXGI
- PresentDXGI および XR_BIAS WDK Windows 7 の表示
- BltDXGI および XR_BIAS WDK Windows 7 の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f81c0837544feb8c612a09b31a73c934a3d2d36
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529158"
---
# <a name="extended-format-aware-requirements"></a>形式の対応要件の拡張


このセクションでは、Windows 7 およびそれ以降のオペレーティング システムにのみ適用されます。

正確な値を返すユーザー モードのディスプレイ ドライバー対応の形式に拡張されたことを保証、 [ **CheckFormatSupport** ](https://msdn.microsoft.com/library/windows/hardware/ff539390)エントリ ポイント関数のすべての形式での表に、 [拡張形式の詳細](details-of-the-extended-format.md)セクション。 ただし、ドライバーはすべての形式を必ずしもサポートしています。

ドライバーは、そのキャスト バック バッファーを完全に型指定されたを暗黙的に保証対応の拡張の形式がサポートされています。

内のテーブルで定義されている機能を使用した形式の拡張形式のドライバーを暗黙的にすべて BGRX と BGRA のサポートに注意してください、[拡張形式の詳細](details-of-the-extended-format.md)セクション。

拡張形式対応 BGRA と BGRA ドライバーが暗黙的にサポート\_SRGB スキャン アウト」の説明に従って、 [BGRA スキャン アウトのサポート](bgra-scan-out-support.md)セクション。

拡張形式対応のドライバーのサポートのビットを新しい形式のいずれかを返す場合を返す必要がすべての必要なビットの表に、[拡張形式の詳細](details-of-the-extended-format.md)セクション。 ドライバーは、テーブル内の不要なビットを返すことはできません。

### <a name="span-idclaimingsupportunderdirect3dversion101spanspan-idclaimingsupportunderdirect3dversion101spanclaiming-support-under-direct3d-version-101"></a><span id="claiming_support_under_direct3d_version_10_1"></span><span id="CLAIMING_SUPPORT_UNDER_DIRECT3D_VERSION_10_1"></span>Direct3D バージョン 10.1 サポートの要求

Direct3D 10.1 および Ddi 以降は、2 つの新しいバージョンのサポートを要求するユーザー モードのディスプレイ ドライバーを許可する更新されます。 1 つのバージョンが 10.0 の機能レベルをサポートするドライバーに対応し、もう一方のバージョンが 10.1 の機能レベルをサポートするドライバーに対応しています。 次に、新しいバージョンの定義を示します。

```cpp
// D3D10.0 or D3D10.1 with extended format support (but not Windows 7 scheduling)
#define D3D10_0_x_DDI_BUILD_VERSION 10
#define D3D10_0_x_DDI_SUPPORTED ((((UINT64)D3D10_0_DDI_INTERFACE_VERSION) << 32) | (((UINT64)D3D10_0_x_DDI_BUILD_VERSION) << 16))
#define D3D10_1_x_DDI_BUILD_VERSION 10
#define D3D10_1_x_DDI_SUPPORTED ((((UINT64)D3D10_1_DDI_INTERFACE_VERSION) << 32) | (((UINT64)D3D10_1_x_DDI_BUILD_VERSION) << 16))
```

### <a name="span-idxrbiasandpresentdxgispanspan-idxrbiasandpresentdxgispanxrbias-and-presentdxgi"></a><span id="xr_bias_and_presentdxgi"></span><span id="XR_BIAS_AND_PRESENTDXGI"></span>XR\_バイアスと PresentDXGI

ドライバーが XR のウィンドウの存在をサポートする必要はありません\_バイアス リソースの呼び出しを通じて、 [ **PresentDXGI** ](https://msdn.microsoft.com/library/windows/hardware/ff569179)関数。 このような場合は、実行時のレベルで制限されています。 ドライバーが XR の存在を全画面表示を実行するその他のすべての書式を持つ\_フリップ操作または同一のソースと宛先リソースとのビット ブロック転送 (bitblt) 操作のどちらかを通じてバイアス。 Stretch または変換は必要ありません。

### <a name="span-idxrbiasandbltdxgispanspan-idxrbiasandbltdxgispanxrbias-and-bltdxgi"></a><span id="xr_bias_and_bltdxgi"></span><span id="XR_BIAS_AND_BLTDXGI"></span>XR\_バイアスと BltDXGI

Direct3D ランタイムが呼び出すドライバーの[ **BltDXGI** ](https://msdn.microsoft.com/library/windows/hardware/ff538252) XR で次の操作のみを実行する関数\_バイアス ソース リソース。

-   XR も先にコピー\_バイアス

-   未変更のソース データのコピー

-   この時点でサンプルは、許容可能な拡張

-   回転

XR\_バイアスが複数サンプル アンチ エイリアス (MSAA) をサポートしていない、ドライバーが XR を解決する必要はありません\_バイアス リソース。

 

 





