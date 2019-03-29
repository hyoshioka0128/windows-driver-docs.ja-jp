---
title: Direct3D バージョン 10.1 のバージョン番号
description: Direct3D バージョン 10.1 のバージョン番号
ms.assetid: a121900a-49e9-40f6-a3a6-d391e3bf1e37
keywords:
- Direct3D のバージョン 10.1 WDK 表示、バージョン番号
- バージョン番号 WDK の表示
- バージョン番号 WDK の表示、Direct3D バージョン 10.1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f58e30c1cda2a80c6fce69b519451a8eae862e7f
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349823"
---
# <a name="version-numbers-for-direct3d-version-101"></a>Direct3D バージョン 10.1 のバージョン番号


Direct3D のバージョン 10.0 および 10.1 サプライ\#ユーザー モードのディスプレイ ドライバーがバージョン管理に使用するかを定義します。 ユーザー モードのディスプレイ ドライバーを確認する必要があります、**インターフェイス**のメンバー、 [ **D3D10DDIARG\_OPENADAPTER**](https://msdn.microsoft.com/library/windows/hardware/ff541724)、 [ **D3D10DDIARG\_CREATEDEVICE**](https://msdn.microsoft.com/library/windows/hardware/ff541664)、および[ **D3D10DDIARG\_CALCPRIVATEDEVICESIZE** ](https://msdn.microsoft.com/library/windows/hardware/ff541649)構造をドライバー呼び出しで受信、 [ **OpenAdapter10**](https://msdn.microsoft.com/library/windows/hardware/ff568602)、 [ **CreateDevice(D3D10)**](https://msdn.microsoft.com/library/windows/hardware/ff540635)、および[ **CalcPrivateDeviceSize** ](https://msdn.microsoft.com/library/windows/hardware/ff538288) Direct3D ランタイムをサポートする Direct3D DDI のバージョンを判断する関数。 最上位の 16 ビット、**インターフェイス**メンバーは、Direct3D DDI メジャー バージョンの数。 10.0 および 10.1 Direct3D のバージョンではこの数は 10 です。 最下位 16 ビット、**インターフェイス**メンバーは、Direct3D DDI マイナー バージョン。 このマイナー バージョンの値は、Direct3D DDI が互換性に影響する変更が導入されるたびに高くなります。 このマイナー バージョンの値より強力なバージョンの変更を示すために意図的にも高くことができます。 次\#にリリースされたバージョン番号を関連付け、Direct3D DDI のマイナー バージョンを定義します (つまり D3D10\_0 = = x、D3D10\_1、y = = 場所 y &gt; x)。

ユーザー モードのディスプレイ ドライバーがの最上位の 16 ビットを調べる必要がありますのみ、**バージョン**のメンバー、 [ **D3D10DDIARG\_OPENADAPTER**](https://msdn.microsoft.com/library/windows/hardware/ff541724)、 [**D3D10DDIARG\_CREATEDEVICE**](https://msdn.microsoft.com/library/windows/hardware/ff541664)、および[ **D3D10DDIARG\_CALCPRIVATEDEVICESIZE** ](https://msdn.microsoft.com/library/windows/hardware/ff541649)に構造体Direct3D のランタイムを構築するときに決定します。 この値は、Direct3D DDI 互換性に影響しない変更があるたびに手動で高くなります。 ドライバーは、時間の経過と共に各互換性に影響しない DDI 変更に依存するは可能性があります。 そのため、ドライバーを確認する必要があります以上の値には、渡された DDI ビルド バージョン、 \*\_ビルド\_失敗するかどうかを現在のドライバーのバージョン、ドライバーは、互換性が (おそらくしながら、レジストリの回避)。 最下位 16 ビット、**バージョン**メンバーが DDI リビジョンのバージョン。 最下位 16 ビットの**バージョン**は通常、ドライバーは、Direct3D API に存在するバグに基づく特殊なケースを使用します。 ドライバーは、すべての値の作成に成功する必要があります。 ただし、ドライバーは、特定の値に応じて動作を変更できます。 使用してこれらの値と比較する必要があります&gt;= ランタイム修正のため、数字が任意に上昇可能性があります。 使用しないでも、"&gt; (切断された以前のバージョン)"(なく"&gt;作業バージョン =") を 2 つの既知のバージョン番号が必要な修正が含まれていない新しいリビジョンが表示されるためです。 次\#定義は、Direct3D DDI バージョン管理。

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

 

 





