---
title: DDI バージョンのレポート
description: DDI バージョンのレポート
ms.assetid: f539a4b4-4652-4e40-928d-d90a3dd1988d
keywords:
- WDK DirectX 9.0 のバージョン番号
- DDI WDK DirectX 9.0 のバージョンのレポート
- DDI バージョン WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: acffaa94c4ba1a3ba38c3749b7ee94ff2ec70da2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380170"
---
# <a name="reporting-ddi-version"></a>DDI バージョンのレポート


## <span id="ddk_reporting_ddi_version_gg"></span><span id="DDK_REPORTING_DDI_VERSION_GG"></span>


DirectX 9.0 バージョンのドライバーのバージョンを報告する必要があります、 [DDI](direct3d-driver-ddi.md) DirectX 9.0 ランタイムは、ドライバーの処理方法を確認できるようにサポートしています。 DDI バージョンを報告するドライバーに応答する、 **GetDriverInfo2** 、D3DGDI2 を使用する要求\_型\_GETDDIVERSION 値。 **DwDXVersion**のメンバー、 [ **DD\_GETDDIVERSIONDATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_dd_getddiversiondata)構造が 9 に設定を DirectX 9.0 ランタイムが、要求を行うことを示します。

ドライバーのセット、 **dwDDIVersion** DD のメンバー\_GETDDIVERSIONDATA DDI バージョン、DirectX 9.0 ランタイムのためのサポートをします。 ドライバーがプレリリース バージョンの DirectX 9.0 ドライバー開発キット (DDK) DDI バージョン番号が DirectX 9.0 の最終バージョンの数を下回るとビルドされている場合、ランタイム、ドライバーとして扱います DirectX 8.0 代わりにします。

 

 





