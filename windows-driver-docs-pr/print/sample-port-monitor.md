---
title: サンプル ポート モニター
description: サンプル ポート モニター
ms.assetid: dac754bf-f39d-439c-974b-889436211ef3
keywords:
- ポートモニター WDK 印刷、サンプル
ms.date: 08/01/2019
ms.localizationpriority: medium
ms.openlocfilehash: 36f4d2e1634d9eac0e43465ef1f72a0b7a9a0693
ms.sourcegitcommit: b444e3a948c4aae2ca1196167844d694c83c8869
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/01/2019
ms.locfileid: "68720043"
---
# <a name="sample-port-monitor"></a>サンプル ポート モニター

> [!NOTE]
> LOCALMON 印刷モニターサンプルはアーカイブされており、GitHub の[Windows Driver Kit (WDK) 10 サンプル](https://github.com/microsoft/Windows-driver-samples)リポジトリでは使用できません。

ローカルの LPT ポートと COM ポートをサポートするポートモニターである LOCALMON (Localmon .dll) のソースコードは、 [Windows Driver kit (wdk) 8.0 サンプル](https://go.microsoft.com/fwlink/p/?LinkId=616509)アーカイブおよび[windows DRIVER kit (wdk) 8.1 サンプル](https://go.microsoft.com/fwlink/p/?LinkId=618052)アーカイブに含まれています。

LOCALMON によってエクスポートされる関数は、ローカルの印刷プロバイダーである Localmon に組み込まれています。 ポートモニターは、ポートモニターのサーバー DLL とポートモニターのユーザーインターフェイス DLL の2つの Dll に分かれています。

これらの dll \\のソースコードは、印刷モニターのサンプルC++\\ \\C++\\\\の localmon と印刷モニター\\のサンプルの localmon サブディレクトリにあります。上記の WDK サンプルアーカイブ。
