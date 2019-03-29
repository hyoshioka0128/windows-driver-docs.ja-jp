---
title: エンタープライズ CA テスト証明書
description: エンタープライズ CA テスト証明書
ms.assetid: c2b075c9-cb85-446d-ac07-65aad5507e62
keywords:
- エンタープライズ CA テスト証明書 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8031a46471c7c777058646ef11437d34ba26f00d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574789"
---
# <a name="enterprise-ca-test-certificate"></a>エンタープライズ CA テスト証明書


*テスト証明書をエンタープライズ CA*はエンタープライズ証明機関 (エンタープライズ CA) によって、企業全体で展開されている Authenticode デジタル証明書。 ドメイン管理者がエンタープライズ規模の Authenticode 証明書の管理にエンタープライズ CA を作成、公開キー基盤の一部として、[ドライバー パッケージ](driver-packages.md)は開発中です。

エンタープライズ CA では、Active Directory に統合し、証明書と証明書失効リストを Active Directory を発行します。 エンタープライズ CA では、ユーザー アカウントと証明書要求を承認または拒否のセキュリティ グループを含む、Active Directory に格納されている情報が使用されます。

エンタープライズ CA では、証明書テンプレートを使用します。 証明書が発行されると、エンタープライズ CA は証明書テンプレートの情報を使用してその証明書の種類に適した属性を持つ証明書を生成します。

証明書の自動承認と自動ユーザー証明書の登録を有効にする場合は、エンタープライズ CA インフラストラクチャが Active Directory と統合する必要があります。

要約すると、ドメイン管理者がエンタープライズ規模の Authenticode 証明書の管理にエンタープライズ CA を作成するには、次の操作を行いますが[ドライバー パッケージ](driver-packages.md)は開発中です。

-   エンタープライズ CA をインストールします。

-   テスト (コード署名の) 証明書テンプレートを作成します。

-   Active Directory で、テスト証明書テンプレートを発行します。

-   エンタープライズ CA によって発行されるテスト証明書を配布するグループ ポリシーを構成します。

エンタープライズ CA を構成する方法の詳細については、このドキュメントの範囲外です。 公開キー基盤とエンタープライズ CA のインストールを設計する方法については、次を参照してください、[コード署名のベスト プラクティス](https://go.microsoft.com/fwlink/p/?linkid=68250)web サイト、。

Windows Server 2003 展開キット、Windows Server 2003 ヘルプとサポート センター、および[Public Key Infrastructures](https://go.microsoft.com/fwlink/p/?linkid=62645)の web ページ、 [Microsoft TechNet](https://go.microsoft.com/fwlink/p/?linkid=62647) web サイト。 TechNet web サイトには、証明書、証明書サービス、および証明書テンプレートに関する情報が含まれています。

テストへの署名をエンタープライズ CA の構成について[ドライバー パッケージ](driver-packages.md)、readme ファイルも用意されて*Selfsign_readme.htm*、内に配置されています、 *src\\一般的な\\ビルド\\driversigning* WDK のディレクトリ。

 

 





