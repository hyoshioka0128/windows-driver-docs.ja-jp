---
title: 一般リリース用のドライバーへの署名
description: 一般リリース用のドライバーへの署名
ms.assetid: 29e465b4-42f2-4c41-afa7-3f0adf579b0c
keywords:
- ドライバー WDK、一般リリースの署名
- 署名ドライバー WDK のパブリック リリースします。
- デジタル署名 WDK のパブリック リリースします。
- 署名 WDK のパブリック リリースします。
- パブリック リリース ドライバーの WDK の署名
- 署名の WDK リリース
- WDK、署名のパブリック リリース ドライバー署名のリリース
- リリースのリリースの署名について、WDK を署名
- WDK の署名をリリースします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60596af7ee0ad6c35c80fe7bf09c81fce599c499
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373488"
---
# <a name="signing-drivers-for-public-release"></a>一般リリース用のドライバーへの署名


カーネル モード バイナリの発行元を識別するリリース署名 (たとえば、ドライバーまたは *.dll*) Windows Vista および Windows の以降のバージョンを読み込みます。 カーネル モード バイナリは、いずれかでリリース署名です。

-   A [WHQL リリース署名](whql-release-signature.md)経由で取得した、 [Windows ロゴ プログラム](https://docs.microsoft.com/windows-hardware/drivers)します。

-   使って作成されたリリース署名、[ソフトウェア発行元証明書 (SPC)](software-publisher-certificate.md)します。

リリースの署名に関連する手順を理解する[ドライバー パッケージ](driver-packages.md)、次のトピックを確認してください。

<a href="" id="introduction-to-release-signing"></a>[リリース署名の概要](introduction-to-release-signing.md)  
このトピックでは、ドライバー パッケージをリリース署名が、重要な理由を説明し、リリース署名プロセスの概要を示します。

<a href="" id="how-to-release-sign-a-driver-package"></a>[ドライバー パッケージをリリース署名する方法](how-to-release-sign-a-driver-package.md)  
このトピックでは、リリース署名プロセスの大まかな概要を提供しを使用してリリース署名の例の多くをレビュー、 *ToastPkg*サンプル ドライバー パッケージ内で、Windows Driver Kit (WDK)。

リリース署名プロセスの詳細については、次のトピックを参照してください。

[WHQL リリース署名](whql-release-signature.md)

[証明書をリリースします。](release-certificates.md)

[ドライバー パッケージのリリース署名](release-signing-driver-packages.md)

 

 





