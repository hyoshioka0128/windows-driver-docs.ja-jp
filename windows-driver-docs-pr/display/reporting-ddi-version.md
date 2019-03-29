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
ms.openlocfilehash: 811b93b3c1eba73a60dc6b5691415905bdf5f516
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578841"
---
# <a name="reporting-ddi-version"></a>DDI バージョンのレポート


## <span id="ddk_reporting_ddi_version_gg"></span><span id="DDK_REPORTING_DDI_VERSION_GG"></span>


DirectX 9.0 バージョンのドライバーのバージョンを報告する必要があります、 [DDI](direct3d-driver-ddi.md) DirectX 9.0 ランタイムは、ドライバーの処理方法を確認できるようにサポートしています。 DDI バージョンを報告するドライバーに応答する、 **GetDriverInfo2** 、D3DGDI2 を使用する要求\_型\_GETDDIVERSION 値。 **DwDXVersion**のメンバー、 [ **DD\_GETDDIVERSIONDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551545)構造が 9 に設定を DirectX 9.0 ランタイムが、要求を行うことを示します。

ドライバーのセット、 **dwDDIVersion** DD のメンバー\_GETDDIVERSIONDATA DDI バージョン、DirectX 9.0 ランタイムのためのサポートをします。 ドライバーがプレリリース バージョンの DirectX 9.0 ドライバー開発キット (DDK) DDI バージョン番号が DirectX 9.0 の最終バージョンの数を下回るとビルドされている場合、ランタイム、ドライバーとして扱います DirectX 8.0 代わりにします。

 

 





