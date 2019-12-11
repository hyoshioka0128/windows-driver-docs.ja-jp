---
title: 信頼された発行元の証明書ストア
description: 信頼された発行元の証明書ストア
ms.assetid: e2fcb0ce-82e3-499a-85b9-76e4e742190e
keywords:
- ドライバー署名 WDK、信頼された発行元の証明書ストア
- 信頼された発行元の証明書ストア WDK
- 証明書ストア WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bca68269e78525209763a43925edafe035a0d378
ms.sourcegitcommit: d94de638476cdd15f9d73a1374acceae4699984b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2019
ms.locfileid: "74995274"
---
# <a name="trusted-publishers-certificate-store"></a>信頼された発行元の証明書ストア


*信頼された発行元の証明書ストア*には、コンピューターにインストールされている信頼された発行元の Authenticode (署名) 証明書に関する情報が含まれています。 組織内の[ドライバーパッケージ](driver-packages.md)をテストおよびデバッグするには、信頼された発行元の証明書ストアのドライバーパッケージに署名するために使用される Authenticode 証明書を会社がインストールする必要があります。 ワークグループまたは組織単位内の署名済みコードを実行する各コンピューターに、Authenticode 証明書をインストールします。 信頼された発行元の証明書ストアの名前は、 *trustedpublisher です。*

発行元の Authenticode 証明書が信頼された発行元の証明書ストアにある場合、Windows は、ユーザーにメッセージを表示せずに証明書によってデジタル署名された[ドライバーパッケージ](driver-packages.md)をインストールします (*サイレントインストール*)。 信頼された発行元の証明書ストアに Authenticode 証明書をインストールすることにより、内部テストおよびデバッグに使用されるさまざまなシステムへのドライバーパッケージのインストールを自動化できます。

**重要**  ドライバーパッケージのインストールを自動化するこの方法は、内部システムに対してのみ推奨されます。 組織外に配布されたドライバーパッケージについては、この方法に従わないでください。

 

信頼された発行元の証明書ストアは、*エンドエンティティ*証明書のみを信頼できるという点で、信頼された[ルート証明機関の証明書ストア](trusted-root-certification-authorities-certificate-store.md)とは異なります。 たとえば、CA からの Authenticode 証明書を使用してドライバーパッケージの[テスト署名](introduction-to-test-signing.md)を行った場合、その証明書を信頼された発行元の証明書ストアに追加しても、この ca が信頼済みとして発行したすべての証明書は構成されません。 各証明書は、信頼された発行元の証明書ストアに個別に追加する必要があります。

ネットワーク上の組織単位に証明書を配布するには、グループポリシーを使用します。 この場合、管理者はグループポリシーに証明書の規則を追加して、パブリッシャーで信頼を確立します。 証明書の規則は、次の Windows バージョンでサポートされているソフトウェアの制限のポリシーに含まれています。

-   Windows Vista 以降のバージョンの Windows。

-   、「Windows Server 2003」を参照してください。

[**Certmgr.exe**](https://docs.microsoft.com/windows-hardware/drivers/devtest/certmgr)ツールを使用して、Authenticode 証明書をコンピューターの信頼された発行元の証明書ストアに手動でインストールできます。

プラグアンドプレイによって使用されるドライバー署名検証**ポリシー  は**、CA の Authenticode 証明書が、信頼された発行元の証明書ストアのローカルコンピューターのバージョンに既にインストールされている必要があります。 詳しくは、「[Local Machine and Current User Certificate Stores](local-machine-and-current-user-certificate-stores.md)」(ローカル マシンおよび現在のユーザーの証明書ストア) をご覧ください。

 

ソフトウェアの制限のポリシーと証明書の規則の使用の詳細については、Windows ヘルプとサポートセンターの情報を参照してください。 

グループポリシーを使用して企業で Authenticode 証明書を展開する方法の詳細については、readme ファイル Selfsign_readme を参照してください *。* このファイルは、「src\\general」 (WDK の *\\ビルド\\driversigning*ディレクトリ) にあります。

証明書ストアの詳細については、「[コード署名のベストプラクティス](https://go.microsoft.com/fwlink/p/?linkid=68250)」 web サイトを参照してください。

 

 





