---
title: カタログ ファイルの SPC 署名の検証
description: カタログ ファイルの SPC 署名の検証
ms.assetid: 57bc65fe-1c31-4ebb-a1bc-e1fe275f8d10
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45ae9e413b8d0e42ed7040684606c2792470d1be
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569947"
---
# <a name="verifying-the-spc-signature-of-a-catalog-file"></a>カタログ ファイルの SPC 署名の検証


確認する、[カタログ ファイル](catalog-files.md)によって、有効な署名が[ソフトウェア発行元証明書 (SPC)](software-publisher-certificate.md)と対応するクロス証明書を次を使用して、 [ **SignTool**](https://msdn.microsoft.com/library/windows/hardware/ff551778)コマンド。

```cpp
SignTool verify /v /kp CatalogFileName.cat 
```

確認するに記載されているファイル、[ドライバー パッケージの](driver-packages.md) [カタログ ファイル](catalog-files.md)によって署名された、[ソフトウェア発行元証明書 (SPC)](software-publisher-certificate.md)と対応するクロス証明書、SignTool の次のコマンドを使用します。

```cpp
SignTool verify /v /kp /c CatalogFileName.cat DriverFileName
```

各項目の意味は次のとおりです。

-   **確認**コマンドの署名を検証する SignTool を構成する、[ドライバー パッケージの](driver-packages.md)カタログ ファイル*CatalogFileName.cat*またはドライバー ファイル*DriverFileName*します。

-   **/V**オプションを実行し、警告メッセージを印刷する SignTool を構成します。

-   **/Kp**オプションの構成ファイルの署名に準拠していることを確認する SignTool、[カーネル モード コードの署名ポリシー](kernel-mode-code-signing-policy--windows-vista-and-later-.md) 、 [PnP デバイスのインストールの署名の要件](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)の Windows Vista および Windows の以降のバージョン。

-   *CatalogFileName.cat*ドライバー パッケージのカタログ ファイルの名前を指定します。

-   ***/C*** *CatalogFileName.cat*オプション ファイルのエントリを含むカタログ ファイルを指定*DriverFileName*します。

-   *DriverFileName*カタログ ファイルにエントリがあるファイルの名前は、 *CatalogFileName.cat*します。

次のコマンドことを確認するなど、 *Tstamd64.cat*カーネル モード コード署名ポリシーと Windows Vista 以降の要件を署名 PnP デバイスのインストールに準拠しているデジタル署名があります。Windows のバージョン。 この例で*Tstam64.cat*コマンドが実行される同じディレクトリにします。

```cpp
SignTool verify /kp tstamd64.cat
```

次の例では、次のコマンドを検証する*Toastpkg.inf*、カタログ ファイルにエントリをある*Tstamd64.cat*、カーネル モード コード署名に準拠しているデジタル署名があります。ポリシーと Windows Vista の要件と以降のバージョンの Windows を署名 PnP デバイスのインストール。 この例で*Tstam64.cat*と*Toastpkg.inf*コマンドが実行される同じディレクトリには。

```cpp
SignTool verify /kp /c tstamd64.cat toastpkg.inf
```

 

 





