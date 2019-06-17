---
title: Driver Signing (ドライバーの署名)
description: Driver Signing (ドライバーの署名)
ms.assetid: 1f7d5340-c7be-4b6a-a85e-246dcc78b1fa
keywords:
- ドライバー WDK の署名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb5ea4ea7f06f3fa31dd46dceaca0b28c9c33dbc
ms.sourcegitcommit: 91b989fc3256267fab89c36b1fa54ff039dcc687
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "67148521"
---
# <a name="driver-signing"></a>Driver Signing (ドライバーの署名)


ドライバーの署名に関連付け、[デジタル署名](digital-signatures.md)で、[ドライバー パッケージ](driver-packages.md)します。

Windows デバイスのインストールを使用して[デジタル署名](digital-signatures.md)とベンダー (ソフトウェア発行元) の id を検証するドライバー パッケージの整合性を検証するドライバー パッケージを提供します。 さらに、[カーネル モード コードの署名ポリシー](kernel-mode-code-signing-policy--windows-vista-and-later-.md) 64 ビット バージョンの Windows Vista と Windows の以降のバージョンのドライバーの読み込みをカーネル モード ドライバーを署名する必要がありますを指定します。

**注**  デスクトップ エディション (Home、Pro、Enterprise、および Education) および Windows Server 2016 カーネル モード ドライバー用の Windows 10 は EV 証明書が必要です。 Windows ハードウェア デベロッパー センター ダッシュによって署名されている必要があります。 詳細については、次を参照してください。[ドライバー署名ポリシー](kernel-mode-code-signing-policy--windows-vista-and-later-.md)します。

ハードウェア デベロッパー センターによって署名された (バージョン 1507、しきい値 1 から開始) Windows 10 のすべてのドライバーは、SHA2 署名です。  オペレーティング システムのバージョンに固有の詳細は、次を参照してください。[バージョンで署名の要件](kernel-mode-code-signing-policy--windows-vista-and-later-.md#signing-requirements-by-version)します。

カーネル モード ドライバーのバイナリを埋め込むの Windows 10 が読み込まれず、または Windows 10 では、システムのクラッシュを引き起こす可能性がよりも前のオペレーティング システム、サード パーティ証明書のベンダーからデュアル (SHA1 および SHA2) 証明書で署名。 この問題を解決するにはインストール[KB 3081436](https://support.microsoft.com/kb/3081436)します。

## <a name="in-this-section"></a>このセクションの内容


-   [ドライバーのインストールのデジタル署名の概要](overview-of-digital-signatures-for-driver-installation.md)
-   [Windows 10 S モード ドライバーの要件](Windows10SDriverRequirements.md)
-   [署名プロセスを管理します。](managing-the-signing-process.md)
-   [開発およびテスト中にドライバーへの署名](signing-drivers-during-development-and-test.md)
-   [ドライバーのパブリック リリースへの署名](signing-drivers-for-public-release.md)
-   [インストールおよび署名されたドライバー パッケージを使用した負荷の問題のトラブルシューティング](troubleshooting-install-and-load-problems-with-signed-driver-packages.md)
-   [マイクロソフト セキュリティ アドバイザリ 2880823](https://docs.microsoft.com/security-updates/SecurityAdvisories/2016/2880823)

ドライバーに関する一般的な情報を Windows Vista および以降のバージョンの Windows では、署名のホワイト ペーパーを参照[システムを実行している Windows Vista でのカーネル モジュールのデジタル署名](https://msdn.microsoft.com/library/bb530195)します。


 





