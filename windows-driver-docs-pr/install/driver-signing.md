---
title: Driver Signing (ドライバーの署名)
description: Driver Signing (ドライバーの署名)
ms.assetid: 1f7d5340-c7be-4b6a-a85e-246dcc78b1fa
keywords:
- ドライバー署名 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 839cac6ab06b61c20054efa133a65b4e9126e8a5
ms.sourcegitcommit: a0e6830b125a86ac0a0da308d5bf0091e968b787
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/21/2020
ms.locfileid: "86557729"
---
# <a name="driver-signing"></a>Driver Signing (ドライバーの署名)


ドライバー署名は、[デジタル署名](digital-signatures.md)を[ドライバーパッケージ](driver-packages.md)に関連付けます。

Windows デバイスのインストールでは、[デジタル署名](digital-signatures.md)を使用してドライバーパッケージの整合性を検証し、ドライバーパッケージを提供するベンダー (ソフトウェア発行元) の id を確認します。 さらに、Windows Vista 以降のバージョンの windows では、[カーネルモードのコード署名64ポリシー](kernel-mode-code-signing-policy--windows-vista-and-later-.md)によって、ドライバーが読み込まれるためにカーネルモードドライバーが署名されている必要があることが指定されています。

**メモ**   Windows 10 for desktop エディション (Home、Pro、Enterprise、および教育) と Windows Server 2016 カーネルモードドライバーは、EV 証明書を必要とする Windows Hardware Dev Center ダッシュボードによって署名されている必要があります。 詳細については、「[ドライバーの署名ポリシー](kernel-mode-code-signing-policy--windows-vista-and-later-.md)」を参照してください。

ハードウェアデベロッパーセンターによって署名された Windows 10 のすべてのドライバー (バージョン1507、しきい値1以降) は、SHA2 署名されています。  オペレーティングシステムのバージョンに固有の詳細については、「[バージョン別の署名要件](kernel-mode-code-signing-policy--windows-vista-and-later-.md#signing-requirements-by-version)」を参照してください。

Windows 10 より前のオペレーティングシステムについて、サードパーティの証明書ベンダーからのデュアル (SHA1 および SHA2) 証明書で署名されたカーネルモードドライバーのバイナリ埋め込みは、読み込まれない場合や、Windows 10 でシステムがクラッシュする場合があります。 この問題を解決するには、 [KB 3081436](https://support.microsoft.com/help/3081436/cumulative-update-for-windows-10-august-11-2015)をインストールします。

## <a name="in-this-section"></a>このセクションの内容


-   [ドライバーのインストール用のデジタル署名の概要](overview-of-digital-signatures-for-driver-installation.md)
-   [Windows 10 S モードでのドライバー要件](Windows10SDriverRequirements.md)
-   [署名プロセスの管理](managing-the-signing-process.md)
-   [開発中とテスト中のドライバーへの署名](signing-drivers-during-development-and-test.md)
-   [一般リリース用のドライバーへの署名](signing-drivers-for-public-release--windows-vista-and-later-.md)
-   [署名済みドライバー パッケージを使用したインストールと読み込みの問題のトラブルシューティング](troubleshooting-install-and-load-problems-with-signed-driver-packages.md)
-   [マイクロソフトセキュリティアドバイザリ2880823](https://docs.microsoft.com/security-updates/SecurityAdvisories/2016/2880823)

Windows Vista 以降のバージョンの Windows でのドライバーの署名に関する一般的な情報については、 [Windows vista を実行しているシステムのカーネルモジュールの](https://docs.microsoft.com/previous-versions/dotnet/articles/bb530195(v=msdn.10))ホワイトペーパー「デジタル署名」を参照してください。


 





