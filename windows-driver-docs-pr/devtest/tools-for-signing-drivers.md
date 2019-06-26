---
title: ドライバーの署名用ツール
description: ドライバーの署名用ツール
ms.assetid: 2654388d-b39e-4009-bcba-56b318fd5119
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8130dc90539e05078cc175ff267bd36300c95c6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360917"
---
# <a name="tools-for-signing-drivers"></a>ドライバーの署名用ツール


Microsoft Windows Driver Kit (WDK) には、次のコード署名証明書、署名の作成に使用できるツールが含まれています、[カタログ ファイル](https://docs.microsoft.com/windows-hardware/drivers/install/catalog-files)の[ドライバー パッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)とでの署名を埋め込むには、ドライバー ファイル:

[**CertMgr**](certmgr.md)

[**Inf2Cat**](inf2cat.md)

[**MakeCat**](makecat.md)

[**MakeCert**](makecert.md)

[**Pvk2Pfx**](pvk2pfx.md)

[**SignTool**](signtool.md)

これらのツールは、次のディレクトリに配置されます。

-   Inf2Cat ツールが WindowsSdkDir % である\\bin\\x86 ディレクトリ。

-   32 ビットの Windows プラットフォーム用のディレクトリにあるその他のツール (%windowssdkdir\\bin\\x86) および 64 ビット Windows プラットフォーム (WindowsSdkDir %\\bin\\x64)。

**注**  WindowsSdkDir %、Visual Studio 環境変数は、Windows キット ディレクトリに、WDK のこのバージョンがインストールされている例では、c: パスを表す\\Program Files (x86)\\Windows キット\\10。

 

Microsoft Windows SDK には、サービス、コンポーネント、および暗号化セキュリティをアプリケーションに追加するためのツールについての情報が含まれます。 これが含まれています、 [ **CertMgr**](certmgr.md)、 [ **MakeCert**](makecert.md)、および[ **SignTool** ](signtool.md)ツール。

ドライバーの署名の詳細については、[ドライバー パッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)を参照してください[ドライバーの署名](https://docs.microsoft.com/windows-hardware/drivers/install/driver-signing)します。

テスト署名ドライバーについてパッケージは、「[開発およびテスト中にドライバーの署名](https://docs.microsoft.com/windows-hardware/drivers/install/signing-drivers-during-development-and-test)します。

 

 





