---
title: 信頼された発行元の証明書ストア
description: 信頼された発行元の証明書ストア
ms.assetid: e2fcb0ce-82e3-499a-85b9-76e4e742190e
keywords:
- ドライバー WDK、信頼された発行元証明書ストアの署名
- 信頼された発行元の証明書ストア WDK
- 証明書ストアの WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e1d715f3222a5468c134e5230b183d8d6374973
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339527"
---
# <a name="trusted-publishers-certificate-store"></a>信頼された発行元の証明書ストア


*信頼された発行元証明書ストア*のコンピューターにインストールされている信頼された発行元 (署名) Authenticode 証明書に関する情報が含まれています。 テストおよびデバッグするには、[ドライバー パッケージ](driver-packages.md)会社、組織内で信頼された発行元の証明書ストアにドライバー パッケージの署名に使用される Authenticode 証明書をインストールする必要があります。 ワークグループ内の各コンピューターに Authenticode 証明書をインストールするか、署名されたコードを実行している組織単位。 信頼された発行元の証明書ストアの名前は*trustedpublisher です。*

Windows をインストール、発行元の Authenticode 証明書が信頼された発行元の証明書ストアにある場合、[ドライバー パッケージ](driver-packages.md)をによってデジタル署名された証明書を求めることがなく (*サイレント インストール*). 信頼された発行元証明書の Authenticode 証明書をインストールすることによってストアは、内部のテストとデバッグに使用されるさまざまなシステムでドライバー パッケージのインストールを自動化することができます。

**重要な**  ドライバー パッケージのインストールを自動化するのには、この実習は内部システムのみお勧めします。 組織外に分散するドライバー パッケージの場合、この実習をたどることはありません必要があります。

 

信頼された発行元の証明書ストアとは異なります、[信頼されたルート証明機関証明書ストア](trusted-root-certification-authorities-certificate-store.md)するだけで*エンド エンティティ*証明書は信頼できます。 たとえば場合から Authenticode 証明書を CA に使用した[テスト署名](introduction-to-test-signing.md)ドライバー パッケージ、その証明書を信頼された発行元が信頼された証明書ストアがこの CA が発行されたすべての証明書を構成しないに追加します。 各証明書は、信頼された発行元の証明書ストアに個別に追加する必要があります。

グループ ポリシーを使用して、ネットワーク上の組織単位に証明書を配布します。 このような状況では、管理者は、パブリッシャーでの信頼を確立するためにグループ ポリシーを証明書の規則を追加します。 証明書の規則は、次の Windows バージョンでサポートされているソフトウェアの制限のポリシーの一部です。

-   Windows Vista と Windows の以降のバージョン。

-   Windows Server 2003 です。

使用して Authenticode 証明書をコンピューターの信頼された発行元証明書ストアに手動でインストールすることができます、 [ **CertMgr** ](https://msdn.microsoft.com/library/windows/hardware/ff543411)ツール。

**注**  ドライバーのプラグ アンド プレイによって使用される認証ポリシーの署名は、CA の Authenticode 証明書が信頼された発行元の証明書ストアのローカル コンピューターのバージョンで以前にインストールされている必要があります。 詳細については、次を参照してください。[ローカル マシンと現在のユーザー証明書ストア](local-machine-and-current-user-certificate-stores.md)します。

 

ソフトウェア制限ポリシーと証明書の規則を使用する方法の詳細については、Windows ヘルプとサポート センターの情報を参照してください。 さらに、上の詳細については、これらのトピックが見つかったら、 [Microsoft TechNet](https://go.microsoft.com/fwlink/p/?linkid=10111) web サイト。

グループ ポリシーを使用して、エンタープライズでの Authenticode 証明書を展開する方法の詳細については、readme ファイルを参照してください*Selfsign_readme.htm*、にある、 *src\\全般\\。ビルド\\driversigning* WDK のディレクトリ。

証明書ストアの詳細については、次を参照してください。、[コード署名のベスト プラクティス](https://go.microsoft.com/fwlink/p/?linkid=68250)web サイト。

 

 





