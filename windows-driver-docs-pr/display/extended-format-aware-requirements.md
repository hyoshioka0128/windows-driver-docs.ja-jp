---
title: 拡張形式の認識要件
description: 拡張形式の認識要件
ms.assetid: eab9c254-fca7-449d-a6cf-1b20d2e7173c
keywords:
- Direct3D バージョン 10.1 WDK Windows 7 の表示、拡張フォーマットに対応した要件
- 拡張形式に対応する要件 WDK Windows 7 ディスプレイ
- XR_BIAS WDK Windows 7 ディスプレイ
- XR_BIAS WDK Windows 7 ディスプレイ、ある Dxgi
- XR_BIAS WDK Windows 7 display、BltDXGI
- XR_BIAS WDK Windows 7 ディスプレイ
- BltDXGI および XR_BIAS WDK Windows 7 ディスプレイ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3a7ae4eaf7c5c41f768be5b2b9d09caba0ed3f5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838943"
---
# <a name="extended-format-aware-requirements"></a>拡張形式の認識要件


このセクションは、Windows 7 以降のオペレーティングシステムにのみ適用されます。

ユーザーモードでは、拡張形式を認識するドライバーによって、拡張形式のセクション[の詳細](details-of-the-extended-format.md)にあるテーブル内のすべての形式について、 [**checkformatsupport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_checkformatsupport)エントリポイント関数から正確な値を返すことが保証されます。 ただし、ドライバーは、必ずしもすべての形式をサポートするわけではありません。

拡張形式を認識するドライバーは、完全に型指定されたバックバッファーのキャストがサポートされることを暗黙的に保証します。

拡張フォーマットを認識するドライバーでは、[拡張形式のセクションの詳細につい](details-of-the-extended-format.md)ては、表に定義されている機能を使用して、すべての BGRX および BGRX 形式を暗黙的にサポートしています。

拡張形式対応のドライバーは、bgra[スキャンアウトサポート](bgra-scan-out-support.md)セクションで説明されているように、bgra と bgra\_SRGB スキャンを暗黙的にサポートします。

拡張フォーマットを認識するドライバーが、新しい形式のいずれかのサポートビットを返す場合、[拡張形式のセクションの詳細](details-of-the-extended-format.md)については、テーブルに必要なすべてのビットを返す必要があります。 ドライバーは、テーブルに不要なビットを返すことはできません。

### <a name="span-idclaiming_support_under_direct3d_version_10_1spanspan-idclaiming_support_under_direct3d_version_10_1spanclaiming-support-under-direct3d-version-101"></a><span id="claiming_support_under_direct3d_version_10_1"></span><span id="CLAIMING_SUPPORT_UNDER_DIRECT3D_VERSION_10_1"></span>Direct3D バージョン10.1 でサポートを要求しています

Direct3D 10.1 以降の DDIs が更新され、ユーザーモードの表示ドライバーで2つの新しいバージョンのサポートを要求できるようになりました。 1つのバージョンは、機能レベル10.0 をサポートするドライバーに対応しており、その他のバージョンは、機能レベル10.1 をサポートするドライバーに対応しています。 新しいバージョンの定義を次に示します。

```cpp
// D3D10.0 or D3D10.1 with extended format support (but not Windows 7 scheduling)
#define D3D10_0_x_DDI_BUILD_VERSION 10
#define D3D10_0_x_DDI_SUPPORTED ((((UINT64)D3D10_0_DDI_INTERFACE_VERSION) << 32) | (((UINT64)D3D10_0_x_DDI_BUILD_VERSION) << 16))
#define D3D10_1_x_DDI_BUILD_VERSION 10
#define D3D10_1_x_DDI_SUPPORTED ((((UINT64)D3D10_1_DDI_INTERFACE_VERSION) << 32) | (((UINT64)D3D10_1_x_DDI_BUILD_VERSION) << 16))
```

### <a name="span-idxr_bias_and_presentdxgispanspan-idxr_bias_and_presentdxgispanxr_bias-and-presentdxgi"></a><span id="xr_bias_and_presentdxgi"></span><span id="XR_BIAS_AND_PRESENTDXGI"></span>XR\_バイアスおよびある Dxgi

ドライバーは、現在の[**dxgi**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)関数の呼び出しによって、XR\_バイアスリソースのウィンドウ表示をサポートする必要はありません。 これらのケースは、ランタイムレベルで制限されます。 他のすべての形式と同様に、ドライバーは、反転操作または同じソースと宛先のリソースを持つビットブロック転送 (bitblt) 操作によって、XR\_バイアスの全画面表示を実行します。 ストレッチや変換は必要ありません。

### <a name="span-idxr_bias_and_bltdxgispanspan-idxr_bias_and_bltdxgispanxr_bias-and-bltdxgi"></a><span id="xr_bias_and_bltdxgi"></span><span id="XR_BIAS_AND_BLTDXGI"></span>XR\_BIAS と BltDXGI

Direct3D ランタイムは、ドライバーの[**Bltdxgi**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)関数を呼び出して、XR\_バイアスソースリソースに対して次の操作のみを実行します。

-   XR\_バイアスでもある宛先へのコピー。

-   未変更のソースデータのコピー

-   ポイントサンプルが許容される伸縮

-   回転

XR\_バイアスでは複数のサンプルアンチエイリアシング (MSAA) がサポートされていないため、XR\_バイアスリソースを解決するためにドライバーは必要ありません。

 

 





