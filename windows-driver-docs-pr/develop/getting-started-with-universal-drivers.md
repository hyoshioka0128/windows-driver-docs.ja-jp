---
ms.assetid: E109BD80-F9CB-4F1F-A6FD-1142E27EC6AD
title: ユニバーサル Windows ドライバーの概要
description: ユニバーサル Windows ドライバーを使用すると、組み込みシステムからタブレットや PC まで、複数の種類のデバイスで動作する 1 つのドライバーを作成できます。
ms.date: 04/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: e09e700906f5fc86f6e100d5ab1c6a60fc0a69c3
ms.sourcegitcommit: 0b38c5075d85ede328bf9901b0d36e84ec0e3d66
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/02/2019
ms.locfileid: "71826519"
---
# <a name="getting-started-with-universal-windows-drivers"></a>ユニバーサル Windows ドライバーの概要

ユニバーサル Windows ドライバーを使うと、組み込みシステムからタブレットやデスクトップ PC まで、複数の種類のデバイスで動作する 1 つのドライバー パッケージを作成できます。

ユニバーサル Windows ドライバー パッケージには、[Windows 10 のユニバーサル Windows プラットフォーム (UWP) ベース エディション](windows-10-editions-for-universal-drivers.md)にインストールされて動作する INF ファイルとバイナリが含まれています。 これらは、共通のインターフェイス セットを共有する Windows 10 の他のエディションにもインストールされ、実行されます。


ドライバー バイナリは、[KMDF](../wdf/index.md)、[UMDF 2](../wdf/getting-started-with-umdf-version-2.md)、または Windows Driver Model (WDM) を使うことができます。

ユニバーサル ドライバーは次の部分から構成されます。
- ベース ドライバー 
- オプションのコンポーネント パッケージ 
- オプションのハードウェア サポート アプリ 

ベース ドライバーには、すべてのコア機能と共有コードが含まれます。 オプションのコンポーネント パッケージには、カスタマイズおよびその他の設定を含めることができます。

通常、デバイスの製造元 (独立系ハードウェア ベンダー (IHV)) が、ベース ドライバーを作成します。 次に、システム ビルダー (相手先ブランド供給 (OEM)) が、オプションのコンポーネント パッケージを提供します。

IHV は、*ドライバー パッケージの分離*の設計ベスト プラクティスに従い、サービス操作に関するドライバーの信頼性と堅牢性を確保します。

IHV がベース ドライバーを認定したら、すべての OEM システムで展開できます。 ベース ドライバーは、ハードウェア部分を共有するすべてのシステム全体で使用できるため、Microsoft では、特定のコンピューターに配布を限定するのではなく、Windows Insider の*ドライバー フライティング*を使用してベース ドライバーを広範にテストできます。

IHV がベース ドライバー パッケージを認定したら、すべての OEM システムで展開できます。 ベース ドライバー パッケージは、ハードウェア部分を共有するすべてのシステム全体で使用できるため、Microsoft では、特定のマシンに配布を限定するのではなく、Windows Insider のフライティングを介してベース ドライバー パッケージを広範にテストできます。 

OEM は、OEM システムに対して提供するオプションのカスタマイズのみを検証します。

ユニバーサル ドライバーは、Windows Update を通じて配布され、ハードウェア サポート アプリは Microsoft Store で配布されます。

## <a name="design-principles"></a>設計原則

ユニバーサル ドライバー パッケージを作成するときは、4 つの設計原則を考慮する必要があります。

* 宣言型 **(D)** : 宣言型の INF ディレクティブのみを使用してドライバーをインストールします。 共同インストーラーや RegisterDll 関数を含めないでください。

* コンポーネント化済み **(C)** : ドライバーのエディション固有、OEM 固有、およびオプションのカスタマイズは、ベース ドライバー パッケージとは別のものです。 このため、コア デバイス機能のみを提供するベース ドライバーは、カスタマイズからは独立してターゲット設定でき、フライティング、メンテナンスを行うことができます。

* ハードウェア サポート アプリ **(H)** : ユニバーサル ドライバーに関連付けられているユーザー インターフェイス (UI) コンポーネントはハードウェア サポート アプリ (HSA) としてパッケージ化するか、OEM デバイスにプレインストールする必要があります。  HSA は、特定のドライバーと関連付けられたオプションのデバイス固有のアプリです。 このアプリケーションは、場合によって、[ユニバーサル Windows プラットフォーム (UWP)](https://docs.microsoft.com/windows/uwp/get-started/universal-application-platform-guide) または[デスクトップ ブリッジ](https://docs.microsoft.com/windows/uwp/porting/desktop-to-uwp-root) アプリとなります。  HSA の配布と更新は、Microsoft Store を通じて行う必要があります。  詳しくは、「[Hardware Support App (HSA): Steps for Driver Developers (ハードウェア サポート アプリ (HSA): ドライバー開発者向け手順)](../devapps/hardware-support-app--hsa--steps-for-driver-developers.md)」および「[Hardware Support App (HSA): Steps for app developers (ハードウェア サポート アプリ (HSA): アプリ開発者向け手順)](../devapps/hardware-support-app--hsa--steps-for-app-developers.md)」を参照してください。

* ユニバーサル API コンプライアンス **(U)** : ユニバーサル ドライバー パッケージ内のバイナリは、Windows 10 の UWP ベースのエディションに含まれる API と DDI のみを呼び出します。 このような DDI には、ドキュメントのリファレンス ページで "**ユニバーサル**" というマークが付いています。 INF ファイルは、ユニバーサル INF 構文のみを使います。

また、ユニバーサル ドライバーでは、ドライバー パッケージの分離の原則からも恩恵を得ることができます。  これらのベスト プラクティスに従うための詳細なガイダンスについては、「ドライバー パッケージの分離」ページをご覧ください。

このドキュメントでは、これらの原則を参照する際に **DCHU** の頭字語を使用します。 この記事の後半には、ドライバー パッケージを DCHU 互換にする方法についてのガイダンスが示されています。
[DCHU ユニバーサル ドライバー サンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/DCHU)での DCHU 設計原則の適用方法について説明されている「[ユニバーサル ドライバーのシナリオ](universal-driver-scenarios.md)」もご覧ください。

## <a name="requirements"></a>要件

ユニバーサル ドライバー パッケージを作成するときは、次の手順に従います。

*  ドライバーの[ユニバーサル INF ファイル](../install/using-an-extension-inf-file.md)を作成します。
    1.  [ユニバーサル ドライバー パッケージにおいて有効な INF のセクションとディレクティブの一覧](../install/using-a-universal-inf-file.md#which-inf-sections-are-invalid-in-a-universal-inf-file)を確認します。
    2.  [InfVerif](../devtest/infverif.md) ツールを使って、ドライバー パッケージの INF ファイルがユニバーサルであることを検証します。
*  [ApiValidator ツール](validating-universal-drivers.md)を使って、バイナリで呼び出される API がユニバーサル ドライバー パッケージに対して有効であることを検証します。

## <a name="best-practices"></a>ベスト プラクティス

*  Visual Studio で Windows Driver Kit (WDK) を使用している場合は、ドライバー プロジェクト プロパティの **[ターゲット プラットフォーム]** の値を `Universal` に設定します。  これによって、正しいライブラリが自動的に追加され、ユニバーサル INF 検証と APiValidator がビルドの一部として実行されます。  これには、次の手順を実行します。

    1. ドライバー プロジェクトのプロパティを開きます。
    2. **[ドライバーの設定]** を選択します。
    3. ドロップダウン メニューを使用し、 **[ターゲット プラットフォーム]** を `Universal` に設定します。

* ドライバー パッケージの分離:

  * ユニバーサル ドライバーの信頼性とサービス性を最大化するために、ドライバーが**ドライバー パッケージの分離**の原則に従っていることを確認します
  * ドライバー パッケージの分離は新しい概念であり、ドライバーを自己完結型にし、OS の変更に対する堅牢性を高めることができます
  * 詳細については「[ドライバー パッケージの分離](driver-isolation.md)」を参照してください
    
*  INF がターゲット プラットフォームに依存するカスタム セットアップ アクションを実行する場合は、それらのアクションを拡張 INF に分離することを検討してください。 拡張 INF はベース ドライバー パッケージとは独立して更新できるので、堅牢性とサービス性が向上します。 詳細については、「[拡張 INF ファイルの使用](../install/using-an-extension-inf-file.md)」を参照してください。
*  お客様のデバイスで動作するアプリケーションを提供する場合は、UWP アプリを含めてください。 詳しくは、「[ハードウェア サポート アプリ (HSA):ドライバー開発者向け手順](../devapps/hardware-support-app--hsa--steps-for-driver-developers.md)」を参照してください。  OEM は [DISM (展開イメージのサービスと管理)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism---deployment-image-servicing-and-management-technical-reference-for-windows) を使ってそのようなアプリを事前に読み込むことができます。 または、ユーザーは Microsoft Store からアプリを手動でダウンロードすることもできます。
*  [**INF の DestinationDirs セクション**](../install/inf-destinationdirs-section.md)で、対象ディレクトリを [dirid 13](../install/using-dirids.md) に設定して、ドライバーを[ドライバー ストア](https://docs.microsoft.com/en-us/windows-hardware/drivers/install/driver-store)から実行します。 一部のデバイスでは、この設定は機能しません。
*  Windows ハードウェア互換性プログラム認定を取得するためのユニバーサル ドライバー パッケージの提出 詳しくは、以下のトピックをご覧ください。

   *  [新しいハードウェア申請を作成する](../dashboard/create-a-new-hardware-submission.md)
   *  [Windows ハードウェア デベロッパー センター ダッシュボードでハードウェア申請を管理する](../dashboard/manage-your-hardware-submissions.md)
   *  [複数の Windows バージョンで Microsoft によって署名されたドライバーを取得する](../dashboard/get-drivers-signed-by-microsoft-for-multiple-windows-versions.md)
   *  [ドライバーのフライティング](../dashboard/driver-flighting.md)
