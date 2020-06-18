---
title: サンプル ポート モニター
description: サンプル ポート モニター
ms.assetid: dac754bf-f39d-439c-974b-889436211ef3
keywords:
- ポートモニター WDK 印刷、サンプル
ms.date: 06/17/2020
ms.localizationpriority: medium
ms.openlocfilehash: 84457f81c4c88898c854e8121e4873cdb0e82773
ms.sourcegitcommit: f4f861a9f833ef1389ff5c08e2b9de0d3df81bef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2020
ms.locfileid: "84974152"
---
# <a name="sample-port-monitor"></a>サンプル ポート モニター

LOCALMON によってエクスポートされる関数は、ローカル印刷プロバイダー Localspl.dll に組み込まれています。 ポートモニターは、ポートモニターのサーバー DLL とポートモニターのユーザーインターフェイス DLL の2つの Dll に分かれています。

> [!NOTE]
> 以前のバージョンの Windows 用の LOCALMON (Localmon.dll) 印刷モニターのサンプルは、次に示すようにアーカイブされています。 LOCALMON (Localmon.dll) print monitor サンプルコードは、GitHub の Windows Driver Kit (WDK) 10 サンプルでは使用できません。

以前のバージョンの Windows では、LOCALMON のサンプルソースコード (Localmon.dll) は次の場所にあります。

- Windows 7 の場合、Localmon.dll のサンプルソースコードは、 [Windows Driver Kit バージョン 7.1.0](https://www.microsoft.com/en-us/download/details.aspx?id=11800)のインストールダウンロードに含まれています。 このサンプルは、 ** \\ src \\ print \\ monitors \\ localmon**サブディレクトリにあります (たとえば、C:\WinDDK\7600.16385.1\src\print\monitors\localmon)。

- Windows 8 の場合、Localmon.dll のサンプルソースコードは、GitHub の Windows Driver Kit (WDK) 8.0 サンプルアーカイブリポジトリの[localmon](https://github.com/microsoftarchive/msdn-code-gallery-microsoft/tree/master/Official%20Windows%20Driver%20Kit%20Sample/Windows%20Driver%20Kit%20(WDK)%208.0%20Samples/%5BC%2B%2B%5D-Windows%20Driver%20Kit%20(WDK)%208.0%20Samples/C%2B%2B/WDK%208.0%20Samples/Print%20Monitors%20Samples/Solution/localmon)ディレクトリにあります。

- Windows 8.1 の場合、Localmon.dll のサンプルソースコードは、GitHub の Windows Driver Kit (WDK) 8.1 サンプルアーカイブリポジトリの[localmon](https://github.com/microsoftarchive/msdn-code-gallery-microsoft/tree/master/Official%20Windows%20Driver%20Kit%20Sample/Windows%20Driver%20Kit%20(WDK)%208.1%20Samples/%5BC%2B%2B%5D-windows-driver-kit-81-cpp/WDK%208.1%20C%2B%2B%20Samples/Print%20Monitors%20Samples/C%2B%2B/localmon)ディレクトリにあります。
