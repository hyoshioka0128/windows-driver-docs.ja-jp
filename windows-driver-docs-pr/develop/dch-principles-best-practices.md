---
ms.assetid: 5865ded8-5b50-4646-a993-613b91d360fb
title: DCH 設計原則とベスト プラクティス
description: Windows ドライバーの DCH 原則について説明します。
ms.date: 04/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: d2c96949ba71ad4a77d036fc98989a150b6c5117
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83270467"
---
# <a name="dch-design-principles-and-best-practices"></a>DCH 設計原則とベスト プラクティス

このページでは、Windows ドライバーの設計原則とベスト プラクティスについて説明します。

## <a name="dch-design-principles"></a>DCH 設計原則

Windows ドライバーを DCH に準拠させる際に考慮すべき設計原則は次の 3 つです。

- 宣言型 **(D)** : 宣言型の INF ディレクティブのみを使用してドライバーをインストールします。 共同インストーラーや RegisterDll 関数を含めないでください。

- コンポーネント化済み **(C)** : ドライバーのエディション固有、OEM 固有、およびオプションのカスタマイズは、ベース ドライバー パッケージとは別のものです。 このため、コア デバイス機能のみを提供するベース ドライバーは、カスタマイズからは独立してターゲット設定でき、フライティング、メンテナンスを行うことができます。

- ハードウェア サポート アプリ **(H)** : Windows ドライバーに関連付けられているユーザー インターフェイス (UI) コンポーネントはハードウェア サポート アプリ (HSA) としてパッケージ化するか、OEM デバイスにプレインストールする必要があります。 HSA は、特定のドライバーと関連付けられたオプションのデバイス固有のアプリです。 このアプリケーションは、場合によって、[ユニバーサル Windows プラットフォーム (UWP)](https://docs.microsoft.com/windows/uwp/get-started/universal-application-platform-guide) または[デスクトップ ブリッジ](https://docs.microsoft.com/windows/uwp/porting/desktop-to-uwp-root) アプリとなります。 HSA の配布と更新は、Microsoft Store を通じて行う必要があります。 詳しくは、「[Hardware Support App (HSA): Steps for Driver Developers (ハードウェア サポート アプリ (HSA): ドライバー開発者向け手順)](https://docs.microsoft.com/windows-hardware/drivers/devapps/hardware-support-app--hsa--steps-for-driver-developers)」および「[Hardware Support App (HSA): アプリ開発者向け手順](https://docs.microsoft.com/windows-hardware/drivers/devapps/hardware-support-app--hsa--steps-for-app-developers)

"DCH" という頭字語は上記の原則を示しています。 ドライバーのサンプルで DCH 設計原則を適用する方法を確認するには、「[DCH 準拠のドライバー パッケージの例](dch-example.md)」ページを参照してください。

## <a name="overview"></a>概要 

DCH 準拠のドライバー パッケージには、[Windows 10 のユニバーサル Windows プラットフォーム (UWP) ベース エディション](target-platforms.md)にインストールされて動作する INF ファイルとバイナリが含まれています。 これらは、共通のインターフェイス セットを共有する Windows 10 の他のエディションにもインストールされ、実行されます。

DCH 準拠のドライバー バイナリは、[KMDF](https://docs.microsoft.com/windows-hardware/drivers/wdf/index)、[UMDF 2](https://docs.microsoft.com/windows-hardware/drivers/wdf/getting-started-with-umdf-version-2)、または Windows Driver Model (WDM) を使うことができます。

DCH 準拠のドライバーは、次の要素で構成されています。

- ベース ドライバー
- オプションのコンポーネント パッケージ
- オプションのハードウェア サポート アプリ

ベース ドライバーには、すべてのコア機能と共有コードが含まれます。 オプションのコンポーネント パッケージには、カスタマイズおよびその他の設定を含めることができます。

通常、デバイスの製造元 (独立系ハードウェア ベンダー (IHV)) が、ベース ドライバーを作成します。 次に、システム ビルダー (相手先ブランド供給 (OEM)) が、オプションのコンポーネント パッケージを提供します。

IHV がベース ドライバー パッケージを認定したら、すべての OEM システムで展開できます。 ベース ドライバー パッケージは、ハードウェア部分を共有するすべてのシステム全体で使用できるため、Microsoft では、特定のマシンに配布を限定するのではなく、Windows Insider のフライティングを介してベース ドライバー パッケージを広範にテストできます。

OEM は、OEM システムに対して提供するオプションのカスタマイズのみを検証します。  

## <a name="requirements"></a>要件

DCH 設計原則に従うドライバー パッケージを作成するには、次の手順に従います。

*  ドライバーの[ユニバーサル INF](../install/using-a-universal-inf-file.md) を作成します。
    1.  [Windows ドライバー パッケージにおいて有効な INF のセクションとディレクティブの一覧](../install/using-a-universal-inf-file.md#which-inf-sections-are-invalid-in-a-universal-inf-file)を確認します。
    2.  [InfVerif](../devtest/infverif.md) ツールを使用して、ドライバー パッケージの INF ファイルが Windows ドライバーの宣言型 (D) 要件に従っていることを確認します。
*  主要なドライバー機能を含んでいないオプションのコンポーネント パッケージが、ベース ドライバー パッケージから分離されていることを確認します。    
*  ドライバー パッケージに関連付けられているハードウェア サポート アプリケーションは、Microsoft Store を通じて配布する必要があります。

## <a name="best-practices"></a>ベスト プラクティス

*  利用可能な最新の Visual Studio で **Windows Driver Kit (WDK) バージョン 2004** を使用している場合は、ドライバー プロジェクト プロパティの **[ターゲット プラットフォーム]** の値を `Windows Driver` に設定します。  これによって、正しいライブラリが自動的に追加され、適切な INF 検証と ApiValidator がビルドの一部として実行されます。  そのためには、次の手順に従います。

    1. ドライバー プロジェクトのプロパティを開きます。
    2. **[ドライバーの設定]** を選択します。
    3. ドロップダウン メニューを使用し、 **[ターゲット プラットフォーム]** を `Windows Driver` に設定します。
   
*  INF がターゲット プラットフォームに依存するカスタム セットアップ アクションを実行する場合は、それらのアクションを拡張 INF に分離することを検討してください。 拡張 INF はベース ドライバー パッケージとは独立して更新できるので、堅牢性とサービス性が向上します。 詳細については、「[拡張 INF ファイルの使用](../install/using-an-extension-inf-file.md)」を参照してください。
*  お客様のデバイスで動作するアプリケーションを提供する場合は、UWP アプリを含めてください。 詳しくは、「[ハードウェア サポート アプリ (HSA):ドライバー開発者向け手順](../devapps/hardware-support-app--hsa--steps-for-driver-developers.md)」を参照してください。  OEM は [DISM (展開イメージのサービスと管理)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism---deployment-image-servicing-and-management-technical-reference-for-windows) を使ってそのようなアプリを事前に読み込むことができます。 または、ユーザーは Microsoft Store からアプリを手動でダウンロードすることもできます。
*  [**INF の DestinationDirs セクション**](../install/inf-destinationdirs-section.md)で、対象ディレクトリを [dirid 13](../install/using-dirids) に設定して、ドライバーを[ドライバー ストア](driver-isolation.md#run-from-driver-store)から実行します。 一部のデバイスでは、この設定は機能しません。


