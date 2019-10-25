---
title: Direct3D バージョン 10.1 のバージョン番号
description: Direct3D バージョン 10.1 のバージョン番号
ms.assetid: a121900a-49e9-40f6-a3a6-d391e3bf1e37
keywords:
- Direct3D バージョン 10.1 WDK ディスプレイ、バージョン番号
- バージョン番号 WDK 表示
- バージョン番号 WDK ディスプレイ、Direct3D バージョン10.1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a56ddd184d08d7046fef04d4403df799516bfe6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829213"
---
# <a name="version-numbers-for-direct3d-version-101"></a>Direct3D バージョン 10.1 のバージョン番号


Direct3D バージョン10.0 および10.1 は、ユーザーモードの表示ドライバーがバージョン管理に使用することを \#定義します。 ユーザーモードの表示ドライバーでは、 [**D3D10DDIARG\_OPENADAPTER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_openadapter)、 [**D3D10DDIARG\_CREATEDEVICE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice)、 [**D3D10DDIARG\_CALCPRIVATEDEVICESIZE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_calcprivatedevicesize)構造体の**インターフェイス**メンバーを調べる必要があります。ドライバーは、 [**OpenAdapter10**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)、 [**CreateDevice (D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)、および[**CalcPrivateDeviceSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivatedevicesize)関数の呼び出しで、DIRECT3D ランタイムがサポートする direct3d DDI のバージョンを確認します。 **インターフェイス**メンバーの最上位16ビットは、Direct3D DDI メジャーバージョンの番号です。 Direct3D バージョン10.0 および10.1 の場合、この数値は10です。 **インターフェイス**メンバーの最下位16ビットは、Direct3D DDI マイナーバージョンです。 このマイナーバージョンの値は、Direct3D DDI の重大な変更が導入されるたびに大きくなります。 このマイナーバージョンの値は、より厳密なバージョン変更を示すために人為的にバンプされることもあります。 次の \#では、Direct3D DDI マイナーバージョンとリリース済みのバージョン番号 (つまり、D3D10\_0 = = x、D3D10\_1 = = y、y &gt; x) を関連付けるように定義します。

ユーザーモードの表示ドライバーでは、 [**D3D10DDIARG\_OPENADAPTER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_openadapter)、 [**D3D10DDIARG\_CREATEDEVICE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice)、および D3D10DDIARG の**バージョン**メンバーのうち、最も重要な16ビットだけを調べる必要があり[ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_calcprivatedevicesize)Direct3D ランタイムがいつビルドされるかを決定する CALCPRIVATEDEVICESIZE 構造体。 この値は、非互換性の Direct3D DDI 変更が発生するたびに手動で設定されます。 ドライバーは、時間の経過に伴う各非互換性 DDI の変化に依存している可能性があります。 したがって、ドライバーは、渡された DDI ビルドのバージョンが現在のドライバーの\_バージョンをビルドし\_\*以上であることを確認し、ドライバーが互換性を持たない場合 (場合によっては、レジストリの回避策も提供します) に、そのバージョンと同じであることを確認する必要があります。 **バージョン**メンバーの下位16ビットは、DDI リビジョンバージョンです。 一般に、Direct3D API に存在するバグに基づいてドライバーを特別に使用する場合は、最も重要な16ビット**バージョン**が使用されます。 ドライバーは、すべての値の作成を成功させる必要があります。 ただし、ドライバーは特定の値に応じて動作を変更できます。 &gt;= を使用して、これらの値と比較する必要があります。これは、実行時の修正によって数値が自由に増加する可能性があるためです。 また、"&gt;= 作業バージョン" ではなく "&gt; (以前に壊れたバージョン)" を使用しないでください。これは、2つの既知の数値の間にバージョン番号があり、必要な修正が含まれていない可能性があるためです。 次の \#は、Direct3D DDI のバージョン管理のためのを定義しています。

```cpp
#define D3D10_DDI_MAJOR_VERSION 10
#define D3D10_0_DDI_MINOR_VERSION 1
#define D3D10_0_DDI_INTERFACE_VERSION ((D3D10_DDI_MAJOR_VERSION << 16) | D3D10_0_DDI_MINOR_VERSION)
#define D3D10_0_DDI_BUILD_VERSION 4
#define D3D10_0_DDI_VERSION_VISTA_GOLD                          ( ( 4 << 16 ) | 6000 )
#define D3D10_0_DDI_VERSION_VISTA_GOLD_WITH_LINKED_ADAPTER_QFE  ( ( 4 << 16 ) | 6008 )
#define D3D10_0_DDI_IS_LINKED_ADAPTER_QFE_PRESENT(Version)  (Version >= D3D10_0_DDI_VERSION_VISTA_GOLD_WITH_LINKED_ADAPTER_QFE)

#if D3D10DDI_MINOR_HEADER_VERSION >= 1
#define D3D10_1_DDI_MINOR_VERSION 2
#define D3D10_1_DDI_INTERFACE_VERSION ((D3D10_DDI_MAJOR_VERSION << 16) | D3D10_1_DDI_MINOR_VERSION)
#define D3D10_1_DDI_BUILD_VERSION 1
// Note: d3d10_1 doesn't currently ship on vista gold. // This definition is included for completeness in the 
// event that it does at some point in the future:
#define D3D10_1_DDI_VERSION_VISTA_GOLD                          ( ( 1 << 16 ) | 6000 )
#define D3D10_1_DDI_VERSION_VISTA_SP1                           ( ( 1 << 16 ) | 6008 )
#define D3D10_1_DDI_IS_LINKED_ADAPTER_QFE_PRESENT(Version)  (Version >= D3D10_1_DDI_VERSION_VISTA_SP1)

#define D3D10on9_DDI_MINOR_VERSION 0
#define D3D10on9_DDI_INTERFACE_VERSION ((D3D10_DDI_MAJOR_VERSION << 16) | D3D10on9_DDI_MINOR_VERSION)
#define D3D10on9_DDI_BUILD_VERSION 0
```

 

 





