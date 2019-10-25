---
title: DirectX 8.0 スタイル Direct3D 機能のレポート
description: DirectX 8.0 スタイル Direct3D 機能のレポート
ms.assetid: a03a7cbc-95be-4251-8e3a-bef4a093f03d
keywords:
- DirectX 8.0 リリースノート WDK Windows 2000 の表示、レポート機能
- D3DCAPS8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdb0125cb026266a5f85b3d37cb477e1ad696386
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825942"
---
# <a name="reporting-directx-80-style-direct3d-capabilities"></a>DirectX 8.0 スタイル Direct3D 機能のレポート


## <span id="ddk_reporting_directx_8_0_style_direct3d_capabilities_gg"></span><span id="DDK_REPORTING_DIRECTX_8_0_STYLE_DIRECT3D_CAPABILITIES_GG"></span>


D3DGDI2\_type\_GETD3DCAPS8 型の**GetDriverInfo2**クエリに応答して、ドライバーは、初期化された D3DCAPS8 構造体を[**DD\_getdriverinfodata**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_getdriverinfodata)構造体の**lpvdata**フィールドにコピーする必要があります。 この構造体は DirectX 8.0 用に新しく追加されたものであり、ドライバーからランタイムへのレポート機能と、ランタイムからアプリケーションまでの両方に使用されます。

D3DCAPS8 には、directx 8.0 に新しく追加された機能と DirectX 7.0 から継承された機能の両方を記述したフィールドがあります。 D3DCAPS8 は、既存の機能を完全に置き換えるものではありません。 この構造 (サポートされている surface 形式の情報と共に) は API の観点からのデバイスの機能についての完全な説明ですが、DDI には不十分です。 ランタイムは、ドライバーによって報告された DirectDraw 機能を、サポートされている surface 機能 (DDSCAPS) などとして使用しますが、DirectX 8.0 API を介して直接公開されることはありません。

さらに、レガシインターフェイス (DirectX 7.0 以前) を使用しているアプリケーションでは、引き続き従来の機能構造 ( [**D3DHAL\_D3DEXTENDEDCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_d3dextendedcaps)など) を報告する必要があります。 そのため、既存の機能レポートメカニズムに代わるものではなく、DirectX 8.0 のスタイルキャップを D3DCAPS8 で報告することは、追加の要件です。 アプリケーションで DirectX 8.0 インターフェイスが使用されている場合、ランタイムは D3DHAL などの拡張された D3D 機能のクエリを実行しません。ドライバーが D3DCAPS8 で DirectX 8.0 の機能を報告する場合、\_などの拡張された D3D 機能については、

D3DCAPS8 については、DirectX 8.0 SDK のドキュメントを参照してください。 ドライバーは、 **(devicetype**または**adapterordinal**フィールドを初期化する必要はありません。 これらは、ランタイムによって適切な値に初期化されます。 ドライバーは、これらのフィールドを0に設定する必要があります。

 

 





