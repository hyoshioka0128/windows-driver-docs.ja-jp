---
title: サンプル ポート モニター
description: サンプル ポート モニター
ms.assetid: dac754bf-f39d-439c-974b-889436211ef3
keywords:
- ポート モニターを WDK の印刷、サンプル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f739b15987fd73acfbf2e937cb7d232911f1ccf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366716"
---
# <a name="sample-port-monitor"></a>サンプル ポート モニター





LOCALMON (Localmon.dll) ローカル lpt ポートと COM ポートをサポートしているポート モニターのソース コードは、Windows Driver Kit (WDK) で含まれています。

Windows 2000 以降、すべての LOCALMON をエクスポートする関数に反映されています Localspl.dll、ローカルの印刷プロバイダー。 Windows 2000 以降のオペレーティング システムのバージョンでもう 1 つの変更は、モニターは、2 つの Dll に分かれています。 そのポート: ポート監視のサーバー DLL、およびポート モニターのユーザー インターフェイス DLL。 これらの Dll のソース コードにある、 \\Src\\印刷\\モニター\\Localmon と\\Src\\印刷\\モニター\\Localui サブディレクトリ。

 

 




