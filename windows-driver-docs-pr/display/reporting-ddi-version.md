---
title: DDI バージョンのレポート
description: DDI バージョンのレポート
ms.assetid: f539a4b4-4652-4e40-928d-d90a3dd1988d
keywords:
- バージョン番号 WDK DirectX 9.0
- レポート DDI バージョン WDK DirectX 9.0
- DDI バージョン WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa7cb45f8b85649ef8e334d8b2946f477c4e9863
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825944"
---
# <a name="reporting-ddi-version"></a>DDI バージョンのレポート


## <span id="ddk_reporting_ddi_version_gg"></span><span id="DDK_REPORTING_DDI_VERSION_GG"></span>


DirectX 9.0 バージョンのドライバーは、DirectX 9.0 ランタイムがドライバーの処理方法を決定できるように、サポートされているバージョンの[DDI](direct3d-driver-ddi.md)を報告する必要があります。 DDI バージョンを報告するために、ドライバーは D3DGDI2\_TYPE\_GETDDIVERSION value を使用する**GetDriverInfo2**要求に応答します。 [**DD\_GETDDIVERSIONDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_dd_getddiversiondata)構造体の**dwdxversion**メンバーは、DirectX 9.0 ランタイムによって要求が行われることを示すために、9に設定されています。

このドライバーは、DD\_GETDDIVERSIONDATA の**dwDDIVersion**メンバーを DirectX 9.0 ランタイム用にサポートしている DDI バージョンに設定します。 ドライバーが directx 9.0 Driver Development Kit (DDK) の prereleased バージョンでビルドされ、そのバージョン番号が DirectX 9.0 の最終バージョンの番号よりも小さい場合、ランタイムはドライバーを DirectX 8.0 として扱います。

 

 





