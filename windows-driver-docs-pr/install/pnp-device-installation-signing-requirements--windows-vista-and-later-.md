---
title: 署名の要件の PnP デバイスのインストール
description: 署名の要件の PnP デバイスのインストール
ms.assetid: 92527b24-b29a-4a78-886d-fafd620090d1
keywords:
- ドライバーの署名の WDK、PnP デバイスのインストール
- ドライバー WDK、PnP デバイスのインストールへの署名
- デジタル署名 WDK、PnP デバイスのインストール
- 署名 WDK、PnP デバイスのインストール
- PnP WDK ドライバーの署名
- プラグ アンド プレイ WDK ドライバーの署名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd4a1a3331343f6e07f23973ec5130dd8937b61d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537268"
---
# <a name="pnp-device-installation-signing-requirements"></a>署名の要件の PnP デバイスのインストール


ドライバーのプラグ アンド プレイ (PnP) の要件を署名デバイスのインストールは、Windows のバージョンとかどうか、ドライバーは署名されているパブリック リリース用または開発チームによって開発およびドライバーのテスト中にによって異なります。 Windows のすべての 64 ビット バージョンを強制[カーネル モード コード署名の要件](kernel-mode-code-signing-requirements--windows-vista-and-later-.md)カーネル モード ドライバーが読み込まれるかどうかを決定します。

### <a href="" id="pnp-signing-requirements-for-public-release-of-a-driver"></a> PnP ドライバーの一般リリースの要件の署名

[ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?linkid=227016)が[テスト カテゴリ](https://go.microsoft.com/fwlink/p/?linkid=189178)さまざまなデバイスの種類。 取得する必要があります、デバイスの種類のテスト カテゴリがこの一覧に含まれる場合、 [WHQL リリース署名](whql-release-signature.md)します。

パブリッシャーの id を検証有効 WHQL リリース署名は、ドライバーが、HCK の要件に準拠していることを確認し、ドライバーが変更されていないことを確認します。

PnP デバイスのインストールによって署名されたと見なされる、[カタログ ファイル](catalog-files.md)の[ドライバー パッケージ](driver-packages.md)WHQL 署名またはサード パーティによって署名する必要があります[リリース証明書](release-certificates.md)([ソフトウェア発行元証明書 (SPC)](software-publisher-certificate.md)または商用リリース証明書)。 いずれかを取得できる場合、WHQL リリース署名を使用する必要があります。 サード パーティ製のリリースの署名は、パブリッシャーの id を検証し、ドライバーが変更されていません。 ただし、WHQL リリース署名とは異なり、サード パーティ製リリース署名はドライバー機能を確認できません。

また、64 ビット バージョンの Windows Vista と Windows の以降のバージョンでは、署名ポリシーをさらに、カーネル モード コードが必要であるか、WHQL SPC をカーネル モード ドライバーに署名します。

リリース署名の詳細については、[パブリック リリース用のドライバーの署名](signing-drivers-for-public-release--windows-vista-and-later-.md)を参照してください。

### <a href="" id="pnp-signing-requirements-for-development-and-test-of-a-driver"></a> 署名の要件の開発とテスト ドライバーの PnP します。

64 ビット バージョンの Windows Vista および以降のバージョンの Windows でドライバーが必要、 [WHQL テスト署名](whql-test-signature-program.md)によって署名する必要がありますか、[テスト証明書](test-certificates.md)します。 テスト署名ドライバーの詳細については、[開発およびテスト中にドライバーの署名](signing-drivers-during-development-and-test.md)を参照してください。

 

 





