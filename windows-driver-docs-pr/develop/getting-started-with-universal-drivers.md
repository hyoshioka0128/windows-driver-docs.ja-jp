---
ms.assetid: E109BD80-F9CB-4F1F-A6FD-1142E27EC6AD
title: ユニバーサル Windows ドライバーの概要
description: ユニバーサル Windows ドライバーを使うと、組み込みシステムからタブレットや PC まで、複数の種類のデバイスで動作する 1 つのドライバーを作成できます。
ms.date: 04/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: e459c16e551ac28ad902204f55426281176d81d5
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "63391513"
---
# <a name="getting-started-with-universal-windows-drivers"></a>ユニバーサル Windows ドライバーの概要

ユニバーサル Windows ドライバーを使うと、組み込みシステムからタブレットやデスクトップ PC まで、複数の種類のデバイスで動作する 1 つのドライバー パッケージを作成できます。

ユニバーサル Windows ドライバー パッケージには INF ファイルとバイナリが含まれ、[Windows 10 のユニバーサル Windows プラットフォーム (UWP) ベース エディション](windows-10-editions-for-universal-drivers.md)、および共通のインターフェイス セットを共有する Windows 10 の他のエディションにインストールされて動作します。

ドライバー バイナリは、[KMDF](../wdf/index.md)、[UMDF 2](../wdf/getting-started-with-umdf-version-2.md)、または Windows Driver Model (WDM) を使うことができます。

ユニバーサル ドライバーは、ベース ドライバー、オプション コンポーネント パッケージ、およびオプションのハードウェア サポート アプリの部分で構成されます。 ベース ドライバーには、すべてのコア機能と共有コードが含まれます。 別に、オプション コンポーネント パッケージには、カスタマイズおよびその他の設定を含めることができます。

通常、デバイスの製造元 (IHV) はベース ドライバーに書き込み、システム ビルダー (OEM) は、すべてのオプション コンポーネント パッケージを提供します。

IHV がベース ドライバーを認定したら、すべての OEM システムで展開できます。 ベース ドライバーは、ハードウェア部分を共有するすべてのシステム全体で使用できるため、Microsoft では、特定のコンピューターに配布を限定するのではなく、Windows Insider のフライティングを介してベース ドライバーを広範にテストできます。 

OEM は、OEM デバイスに対して提供するオプションのカスタマイズのみを検証します。

ユニバーサル ドライバーは、Windows Update を通じて配布され、ハードウェア サポート アプリは Microsoft Store で配布されます。

## <a name="design-principles"></a>設計原則

ユニバーサル ドライバー パッケージを作成するときは、4 つの設計原則を考慮する必要があります。

* 宣言型 **("D")** : 宣言型 INF ディレクティブのみを使用してドライバーをインストールし、共同インストーラーや RegisterDlls などを含めません。
* コンポーネント化済み **("C")** : ドライバーに対するエディション固有、OEM 固有、オプションのカスタマイズはベース ドライバー パッケージとは別であるため、コアとなるデバイス機能のみを提供するベース ドライバーをカスタマイズからは独立して対象にし、フライティングおよび処理することができます。
* ハードウェア サポート アプリ **("H")** :ユニバーサル ドライバーに関連付けられているユーザー インターフェイス (UI) コンポーネントはハードウェア サポート アプリ (HSA) としてパッケージ化するか、OEM デバイスにプレインストールする必要があります。  HSA は、特定のドライバーと関連付けられたオプションのデバイス固有のアプリです。  このアプリケーションは、場合によって、[ユニバーサル Windows プラットフォーム (UWP)](https://docs.microsoft.com/windows/uwp/get-started/universal-application-platform-guide) または[デスクトップ ブリッジ](https://docs.microsoft.com/windows/uwp/porting/desktop-to-uwp-root) アプリとなります。  HSA の配布と更新は、Microsoft Store を通じて行う必要があります。  詳しくは、「[Hardware Support App (HSA): Steps for Driver Developers (ハードウェア サポート アプリ (HSA): ドライバー開発者向け手順)](../devapps/hardware-support-app--hsa--steps-for-driver-developers.md)」および「[Hardware Support App (HSA): Steps for App Developers (ハードウェア サポート アプリ (HSA): アプリ開発者向け手順)](../devapps/hardware-support-app--hsa--steps-for-app-developers.md)」をご覧ください。
* ユニバーサル API コンプライアンス **("U")** : ユニバーサル ドライバー パッケージ内のバイナリは、Windows 10 の UWP ベースのエディションに含まれる API と DDI だけを呼び出します。 このような DDI には、ドキュメントのリファレンス ページで "**ユニバーサル**" というマークが付いています。 INF ファイルは、ユニバーサル INF 構文のみを使います。

このドキュメントでは、上記の原則を参照する際に頭字語 **DCHU** を使用します。
ドライバー パッケージを DCHU 互換にする方法については、以下にガイダンスを示しています。
[DCHU ユニバーサル ドライバー サンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/DCHU)での DCHU 設計原則の適用方法について説明されている「[ユニバーサル ドライバーのシナリオ](universal-driver-scenarios.md)」もご覧ください。

## <a name="requirements"></a>要件

ユニバーサル ドライバー パッケージを作成するときは以下のことが必要です。

*  ドライバーの[ユニバーサル INF ファイル](../install/using-an-extension-inf-file.md)を作成します。
    1.  [ユニバーサル ドライバー パッケージにおいて有効な INF のセクションとディレクティブの一覧](../install/using-a-universal-inf-file.md#which-inf-sections-are-invalid-in-a-universal-inf-file)を確認します。
    2.  [InfVerif](../devtest/infverif.md) ツールを使って、ドライバー パッケージの INF ファイルがユニバーサルであることを検証します。
*  [ApiValidator ツール](validating-universal-drivers.md)を使って、バイナリで呼び出される API がユニバーサル ドライバー パッケージに対して有効であることを検証します。

## <a name="best-practices"></a>ベスト プラクティス

*  Visual Studio で WDK を使用する場合は、ドライバー プロジェクト プロパティの **[ターゲット プラットフォーム]** の値を `Universal` に設定します。  これによって、正しいライブラリが自動的に追加され、ユニバーサル INF 検証と APIValidator がビルドの一部として実行されます。  これには、次の手順を実行します。

    1. ドライバー プロジェクトのプロパティを開きます。
    2. **[ドライバーの設定]** を選択します。
    3. ドロップダウン メニューを使用し、 **[ターゲット プラットフォーム]** を `Universal` に設定します。
    
*  INF がターゲット プラットフォームに依存するカスタム セットアップ アクションを実行する場合は、それらのアクションを拡張 INF に分離することを検討してください。  拡張 INF はベース ドライバー パッケージとは独立して更新できるので、堅牢性とサービス性が向上します。  「[拡張 INF ファイルの使用](../install/using-an-extension-inf-file.md)」をご覧ください。
*  お客様のデバイスで動作するアプリケーションを提供する場合は、UWP アプリを提供してください。  詳しくは、「[Hardware Support App (HSA): Steps for Driver Developers (ハードウェア サポート アプリ (HSA): ドライバー開発者向け手順)](../devapps/hardware-support-app--hsa--steps-for-driver-developers.md)」をご覧ください。  OEM は [DISM (展開イメージのサービスと管理)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism---deployment-image-servicing-and-management-technical-reference-for-windows) を使ってそのようなアプリを事前に読み込むことができます。  または、ユーザーは Microsoft Store からアプリを手動でダウンロードすることもできます。
*  [  **INF の DestinationDirs セクション**](../install/inf-destinationdirs-section.md)で、対象ディレクトリを [dirid 13](../install/using-dirids.md) に設定して、ドライバーをドライバー ストアから実行します。  これは一部のデバイスでは動作しません。
*  Windows ハードウェア互換性プログラム認定を取得するためのユニバーサル ドライバー パッケージの提出 詳しくは、次のトピックをご覧ください。

   *  [新しいハードウェア申請を作成する](../dashboard/create-a-new-hardware-submission.md)
   *  [Windows ハードウェア デベロッパー センター ダッシュボードでハードウェア申請を管理する](../dashboard/manage-your-hardware-submissions.md)
   *  [複数の Windows バージョンで Microsoft によって署名されたドライバーを取得する](../dashboard/get-drivers-signed-by-microsoft-for-multiple-windows-versions.md)
   *  [ドライバーのフライティング](../dashboard/driver-flighting.md)
