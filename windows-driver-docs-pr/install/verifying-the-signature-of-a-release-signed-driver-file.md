---
title: リリース署名されたドライバー ファイルの署名の検証
description: リリース署名されたドライバー ファイルの署名の検証
ms.assetid: 70876389-6493-4c16-8a82-ca72fc23325c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a96c2fc31034c5fe8876b8fc130bc2d3b928f231
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380438"
---
# <a name="verifying-the-signature-of-a-release-signed-driver-file"></a>リリース署名されたドライバー ファイルの署名の検証


によって作成されるドライバー ファイルの埋め込みの署名を検証する、[ソフトウェア発行元証明書 (SPC)](software-publisher-certificate.md)、次を使用して、 [ **SignTool** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool)コマンド。

```cpp
SignTool verify /v /kp DriverFileName.sys
```

各項目の意味は次のとおりです。

-   **確認**コマンドでは、ドライバー ファイルに埋め込まれている署名を検証する SignTool を構成します。 *DriverFileName.sys します。*

-   **/V**オプションを実行し、警告メッセージを印刷する SignTool を構成します。

-   **/Kp**オプションを構成することを確認する SignTool に埋め込まれている署名*DriverFileName.sys*に準拠している、[カーネル モード コードの署名ポリシー](kernel-mode-code-signing-policy--windows-vista-and-later-.md)と[PnP デバイスのインストール要件を署名](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)Windows Vista および Windows の以降のバージョン。

-   *DriverFileName.sys*ドライバー ファイルの名前を指定します。

次のコマンドことを確認するなど、 *Toaster.sys*有効な埋め込み署名します。 この例では、T で*oaster.sys*では、 *amd64*コマンドが実行されるディレクトリのサブディレクトリ。

```cpp
SignTool verify /kp amd64\toaster.sys
```

 

 





