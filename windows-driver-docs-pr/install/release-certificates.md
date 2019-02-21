---
title: 証明書をリリースします。
description: 証明書をリリースします。
ms.assetid: 61bd5002-b3b6-4f11-b0c2-80eeaf2fec39
keywords:
- パブリック リリース ドライバーの WDK、リリースの証明書の署名
- WDK、リリースの証明書の署名をリリースします。
- 証明書の WDK リリースします。
- 証明書の WDK リリース
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0aeb74c1ab2cb88a51cd779948026e77b9b0dc4f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548792"
---
# <a name="release-certificates"></a>証明書をリリースします。


に準拠して署名ポリシーを 64 ビット バージョンの Windows Vista と Windows の以降のバージョンのカーネル モード コードを取得する必要があります、 [WHQL リリース署名](whql-release-signature.md)を使用して、または、[ソフトウェア発行元証明書 (SPC)](software-publisher-certificate.md)署名、[カタログ ファイル](catalog-files.md)カーネル モードの[ドライバー パッケージ](driver-packages.md)します。

ドライバーの場合、*ブート開始ドライバー* 64 ビット システムでは、する必要もあります[埋め込む](embedded-signatures-in-a-driver-file.md)ドライバー ファイルに、SPC 署名します。 これは、プラグ アンド プレイ (PnP) または非 PnP のカーネル モード ドライバーの任意の型に適用されます。

[ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?linkid=227016)が[テスト カテゴリ](https://go.microsoft.com/fwlink/p/?linkid=189178)さまざまなデバイスの種類。 準拠する、 [PnP デバイスのインストール要件](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)の 32 ビット バージョンの Windows Vista と以降のバージョンの Windows HCK は、デバイスの種類のテスト カテゴリがある場合、WHQL リリース署名を取得する必要があります。 WHQL リリース署名を取得できない場合は、SPC いずれかを使用する必要がありますまたは[コマーシャル リリースの証明書](commercial-release-certificate.md)PnP カーネル モード ドライバーに署名します。

 

 





