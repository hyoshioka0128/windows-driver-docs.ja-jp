---
title: DirectX 8.0 スタイル Direct3D 機能のレポート
description: DirectX 8.0 スタイル Direct3D 機能のレポート
ms.assetid: a03a7cbc-95be-4251-8e3a-bef4a093f03d
keywords:
- DirectX 8.0 WDK Windows 2000 のリリース ノートを表示するレポートの機能
- D3DCAPS8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76134b93c2313808675ee2db1a417eef3a374778
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380158"
---
# <a name="reporting-directx-80-style-direct3d-capabilities"></a>DirectX 8.0 スタイル Direct3D 機能のレポート


## <span id="ddk_reporting_directx_8_0_style_direct3d_capabilities_gg"></span><span id="DDK_REPORTING_DIRECTX_8_0_STYLE_DIRECT3D_CAPABILITIES_GG"></span>


応答を**GetDriverInfo2** D3DGDI2 の種類を使用したクエリ\_型\_GETD3DCAPS8、ドライバーに初期化された、D3DCAPS8 構造をコピーする必要があります、 **lpvData**のフィールド、[ **DD\_GETDRIVERINFODATA** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_getdriverinfodata)構造体。 この構造体は、DirectX 8.0 の新機能は、ランタイムにドライバーとアプリケーションにランタイムから両方のレポート機能の使用されます。

D3DCAPS8 は DirectX 8.0 の両方の機能を記述するフィールドを備え、機能は、DirectX 7.0 からの転送を実行します。 D3DCAPS8 は既存の機能の完全な置換ではありません。 (サポートされている画面形式の情報) と共にこの構造体は、API の観点から、デバイスの機能の詳細については、DDI のための十分なことはありません。 ランタイムは、DirectDraw の利用などの情報のドライバーによって報告された機能は、これらは、DirectX 8.0 API を介して直接公開されない場合でも、サーフェイスの機能 (DDSCAPS) をサポートされています。

ドライバーが引き続きレガシ機能の構造をレポートするために必要なさらに、(など[ **D3DHAL\_D3DEXTENDEDCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_d3dextendedcaps)) レガシー インターフェイスを使用するアプリケーション (DirectX 7.0 とこれらの機能の要求を続行前)。 そのため、レポート D3DCAPS8 を通じて DirectX 8.0 スタイルの上限は、既存機能のレポート機構に代わるものではなく、追加の要件。 DirectX 8.0 インターフェイスが D3DHAL など、D3D の拡張機能で、ランタイムは照会されませんアプリケーションで使用する場合\_D3DEXTENDEDCAPS ドライバー D3DCAPS8 DirectX 8.0 機能の報告された場合。

D3DCAPS8 は DirectX 8.0 SDK ドキュメントで説明します。 ドライバーを初期化する必要がありますできません、 **DeviceType**または**AdapterOrdinal**フィールド。 これらは、ランタイムによって適切な値に初期化されます。 ドライバーは、これらのフィールドを 0 に設定する必要があります。

 

 





