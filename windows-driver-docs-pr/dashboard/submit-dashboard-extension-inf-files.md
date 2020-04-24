---
title: Windows ハードウェア ダッシュボードでの拡張 INF の使用
description: Windows ハードウェア デベロッパー センターで拡張 INF ファイルの出荷ラベルを作成し、その他の申請と同様に共有し、公開することができます。
ms.topic: article
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6803f0632e501678688a48a50fc457dfa58fb359
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "67364416"
---
# <a name="working-with-extension-infs-in-the-partner-center"></a>パートナー センターでの拡張 INF の使用

Windows ハードウェア デベロッパー センターで拡張 INF ファイルの出荷ラベルを作成し、その他の申請と同様に共有し、公開することができます。 このトピックでは、これらのパッケージのパッケージ化、提出、公開のプロセスについて説明します。 拡張 INF が作成およびインストールされるしくみの詳細については、「[拡張 INF ファイルの使用](https://docs.microsoft.com/windows-hardware/drivers/install/using-an-extension-inf-file)」を参照してください。

## <a name="requirements-for-publishing-extension-infs-to-windows-update"></a>Windows Update に拡張 INF を公開するための要件 

Windows Update に拡張 INF を公開するには、出荷ラベルで自動ドライバーのプロモーションのチェック ボックスをオンにする必要があります。 拡張 INF をオプションとして公開することができない理由は、デバイス マネージャーの一覧に表示されないため、エンドユーザーが "ドライバーの更新" 操作を開始できないためです。   これらのチェック ボックスを確認するには、まず[ドライバーのフライティング](https://docs.microsoft.com/windows-hardware/drivers/dashboard/driver-flighting)にサインアップする必要があります。 

> [!NOTE]
> Windows Update で拡張 INF を提供できるようにするには、すべてのシステムで RS3 [2018 年 1 月更新プログラム](https://support.microsoft.com/help/4056892/windows-10-update-kb4056892) (10.0.16299.192) 以上が実行されている必要があります。

## <a name="submitting-and-publishing-extension-infs"></a>拡張 INF の提出と公開

ここでは、INF パッケージを提出および公開する方法について説明します。 よくある誤りとよく寄せられる質問については、強調表示されている項目とよく寄せられる質問を参照してください。

> [!IMPORTANT]
> 常に、それぞれの拡張 INF に個別の申請を作成し、ベース ドライバーのみを含む申請を別に作成することをお勧めします。 ベース ドライバーと拡張 INF を 1 つの申請で公開すると、次の問題が発生します。
>
> * パートナー センターによって、すべての出荷ラベルが "拡張ドライバー" として分類および評価されます。 拡張機能である項目を検索するには、デベロッパー センターの検索ボックスに「`@IsExtensionDriver:"True"`」と入力します。
> * Windows Update に公開した後、ユーザーが何回もドライバー パッケージのダウンロードを強制される場合があります。ベース ドライバーがインストールされるときに 1 回と、PnP で検出された該当する拡張機能ごとに 1 回ずつです。

### <a name="creating-a-submission-package"></a>提出パッケージの作成

#### <a name="base-driver-package"></a>ベース ドライバー パッケージ

1. ベース ドライバーと拡張 INF で通常どおり HLK テスト実行を開始します。 HLK 結果は、下のすべてのパッケージ作成手順で使用されます。 

    ![HLK テスト実行によって出力されたファイルを示す画像](images/hlk-result-files.png)

2. 次に示すように、Drivers フォルダーから 拡張 INF テンプレート項目を削除し、ベース ドライバー ファイルのみを HLK パッケージにもう一度追加します。

    ![ベース ドライバー ファイルを示す画像](images/hlk-result-files2.png)

3. この HLKx パッケージを作成して署名し、ベース ドライバー パッケージを作成します。

    > [!NOTE]
    > ベース ドライバー パッケージは常に既存の拡張との下位互換性を保つようにする必要があります。

#### <a name="extension-inf-package"></a>拡張 INF パッケージ

1. 前述の同じ HLK 結果を使用して、 **[パッケージ]**  >  **[ドライバーの置換]** の順に選択します。

    ![HLK の [ドライバーの置換] オプションを示す画像](images/hlk-replace-driver.png)

2. 参照される任意のバイナリを使ってドライバーのフォルダーに拡張 INF を追加します。 複数の拡張 INF がある場合は、1 つのファイルのみを追加します。 

3. この新しい HLK パッケージを作成して署名します。 これが拡張 INF パッケージになります。

4. それぞれの拡張 INF についてこのプロセスを繰り返し、毎回、ドライバー フォルダーの内容を削除します。

### <a name="submitting-your-packages-to-the-partner-center"></a>パートナー センターへのパッケージの提出

上で作成したパッケージごとに、新しい申請を作成し、ハードウェア デベロッパー センターにアップロードします。  その後、共有または公開するパッケージの出荷ラベルを作成します。 詳細については、「[新しいハードウェア提出の作成](https://docs.microsoft.com/windows-hardware/drivers/dashboard/create-a-new-hardware-submission)」および「[出荷ラベルによるドライバーの配布の管理](https://docs.microsoft.com/windows-hardware/drivers/dashboard/manage-driver-distribution-by-submission)」を参照してください。

#### <a name="extensionid"></a>ExtensionID

ExtensionID は、生成する GUID で、ドライバーの系列 ID とバージョン管理に使用されます。 ExtensionID は、ハードウェア デバイスの部品または部品の系列を記述したもので、それを提出した SellerID に[自動的に登録されます](https://techcommunity.microsoft.com/t5/Windows-Hardware-Certification/bg-p/WindowsHardwareCertification)。 この SellerID の所有者は、CHID の管理と同様に、ExtensionID 使用状況とマッピングの追跡を行います。 

たとえば、新しいシステムの部品に ExtensionID を作成する場合は、次のようになります。

* ExtensionID 所有権は、SellerID に割り当てられます。
* 部品または部品の系列を使用する組織の各システム プロジェクトで同じ ExtensionID を共有します。
* ExtensionID は、その部品の寿命が終了するまで変更されません。

> [!NOTE]
>
> * SellerID に関連付けられていない ExtensionID を使用する場合は、パートナー センターによって申請が拒否され、その ExtensionID が既に別の組織に属していることが通知されます。
> * 特定のデバイスについて、一意の ExtensionID 値ごとに 1 つの拡張 INF のみがインストールされます。 そのため、デバイスに複数の拡張 INF がある場合は、それぞれの 拡張 INF について新しい ExtensionID が必要になります。  これはまた、2 つの拡張 INF が別の ExtensionID を持つ同じデバイスをターゲットにする場合、両方の拡張 INF が適用されることを意味します。 詳細については、「[拡張 INF ファイルの使用](https://docs.microsoft.com/windows-hardware/drivers/install/using-an-extension-inf-file)」を参照してください。
>
> 組織で別の組織のプロジェクトと申請を管理している場合、次の点に注意してください。
>
> * ExtensionID 所有権は、申請を終了した SellerID に割り当てられます。 
> * 別の組織の SellerID を使用すると、その組織の ExtensionID を使用できます。
> * 自分の組織の SellerID を使用するには、部品または部品の系列に対して独自の ExtensionID を作成する必要があります。

最初のバージョンの拡張 INF に対して新しい ExtensionID を生成する必要があります (つまり、初めて拡張 INF をカスタマイズして送信したとき)。 これには、新しいデバイスの新しい共有出荷ラベルを初めて受け取ったときが含まれます。 Visual Studio には、[ツール] > [GUID の作成] に GUID の作成ユーティリティがあります。ただし、次に示すレジストリ形式に一致すれば、任意のオンライン GUID 生成ツールが機能します。

![Visual Studio の [GUID の作成] 画面を示す画像](images/guid-formatting.png)

公開済みの拡張 INF を更新する場合は、ExtensionID を同じにし、[DriverVer ディレクティブ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-driverver-directive)で指定されたバージョンおよび日付を増分します。 ドライバーの日付とドライバーのバージョンがこの順番で、同じ ExtensionID を持つ複数の拡張 INF を区別するために使用されます。

### <a name="publishing-an-extension-inf"></a>拡張 INF の公開

拡張 INF の提出を公開するには、[Windows Update にドライバーを公開する](https://docs.microsoft.com/windows-hardware/drivers/dashboard/publish-a-driver-to-windows-update)の手順に従ってください。 両方の自動ドライバーのプロモーション オプションがオンになっていること、また拡張 INF に具体的なターゲットがあることを確認します。 

![自動のドライバーのプロモーションを示す画像](images/automatic-driver-promotion-options.png)

これらのドライバーのプロモーション オプションが表示されない場合は、[ドライバーのフライティング](https://docs.microsoft.com/windows-hardware/drivers/dashboard/driver-flighting)にサインアップする必要があります。

すべての拡張 INF は、Windows Update を通じて配布されるドライバーのフライティング プロセスを通過します。 フライトに成功すると、小売システムでファイルが利用可能になります。 Windows Insider プログラムに参加すると、この段階でドライバーに迅速にアクセスできます。

## <a name="extension-inf-targeting-and-ranking-differences"></a>拡張 INF のターゲットとランク付けの相違点

拡張機能は、特定のデバイス用のカスタマイズであるため、常に具体的にターゲットにする必要があります。  拡張 INF のターゲットを使用する場合は、次のガイドラインに従ってください。

* 拡張 INF ファイルには、可能であれば 4 部構成のハードウェア ID (HWID) が必要です。 
* 4 部構成の HWID に加えて、CHID が拡張 INF の出荷ラベルに追加される可能性があります。
* 4 部構成の HWID を持たない部品および部品系列については、出荷ラベルで CHID ターゲットが必要になります。

このターゲット情報は、Windows Update (WU) による配布中に拡張 INF を正確に評価するために不可欠です。 WU がドライバーを評価する際に次の 2 つのステージがあります。

1. 特定のシステムに適用されるドライバーの一覧を WU で作成するときの適用性ステージ。
2. Windows PnP および WU が一覧からインストールするドライバーを判断するランク付けステージ。

一般に、拡張 INF のランク付け/ターゲット設定に関して、いくつかの重要な原則があります。  

* 拡張 INF の ExtensionID は適用性に使用されません – 系列とバージョン管理 ID にのみ使用されます。

* 該当する各 ExtensionID の最も順位の高い拡張ドライバーが WU によって提供 (および PnP によってインストール) されます。

* 拡張ドライバーは、DriverVer ディレクティブに含まれている日付 & バージョンでのみランク付けされます。 これは、WU と PnP の両方によって使用されます。  詳細については、「[INF Version セクション](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)」および「[INF DriverVer ディレクティブ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-driverver-directive)」を参照してください。
* PnP および WU では、拡張ドライバーに関して機能または識別子スコア (つまり、2 部と 4 部) が考慮されないことに注意してください。

* WU で拡張ドライバーをランク付けするときに CHID 情報は使用されません (つまり、CHID ターゲットを持つ他の拡張ドライバーを "ブロック" できません)。

* Windows オペレーティング システム内のドライバーの選択およびターゲットについては、「[拡張 INF ファイルの使用](https://docs.microsoft.com/windows-hardware/drivers/install/using-an-extension-inf-file)」を参照してください。

## <a name="faq"></a>FAQ

### <a name="driver-development"></a>ドライバーの開発

#### <a name="do-we-need-to-change-the-extensionid-every-time-we-make-an-update-to-our-base-driver"></a>ベース ドライバーを更新するたびに、ExtensionID を変更する必要がありますか?

いいえ、ベース ドライバーに更新を行うときに、同じ ExtensionID を保持する必要があります。  バージョンの比較およびドライバーの系列 ID に ExtensionID が使用されます。  ExtensionID はドライバーの系列内で変更しないでください。 

### <a name="manufacturing"></a>製造

#### <a name="can-we-use-an-ihv-supplied-extension-inf-with-their-extensionid-for-manufacturing-purposes"></a>製造の目的で IHV 提供の拡張 INF をその ExtensionID と一緒に使用できますか?

いいえ。 拡張機能のサービスの側面を所有する場合は、製造時に独自の拡張 INF と ExtensionID を使用する必要があります。  

### <a name="driver-updates"></a>ドライバーの更新

#### <a name="do-we-need-to-publish-an-updated-extension-inf-to-windows-update-every-time-a-base-driver-package-is-updated-and-published"></a>ベース ドライバー パッケージが更新および公開されるたびに、Windows Update に更新された拡張 INF を公開する必要がありますか?

いいえ、公開してはいけません。  ベース ドライバー パッケージは常に既存の拡張子との下位互換性を保つようにする必要があります。

#### <a name="what-happens-when-an-updated-base-driver-is-published-and-applied-to-an-end-users-system"></a>更新済みのベース ドライバーが公開され、エンド ユーザーのシステムに適用されるとどうなりますか?

ベース ドライバーの更新プログラムが適用されると、現在インストールされている拡張 INF が評価され、必要に応じて適用されます。 拡張 INF がインストールされていない場合は、Windows Update が適用可能な最新のバージョンをダウンロードします。

#### <a name="do-we-need-to-publish-an-updated-extension-inf-or-extensionid-when-we-update-our-os-to-the-latest-version"></a>OS を最新バージョンに更新するときに更新された拡張 INF または ExtensionID を公開する必要がありますか?

いいえ、既存の ExtensionID と拡張 INF は引き続き機能します。

#### <a name="can-two-systems-share-the-same-extension-inf-if-their-customizations-are-the-same"></a>2 つのシステムのカスタマイズが同じ場合、2 つのシステムで同じ拡張 INF を共有できますか?

はい。  複数のシステムで同じ設定を使用する場合、またはより広範なデバイス間で設定をカスタマイズする場合は、1 つの拡張 INF で十分です。  これを行うには、適用可能な 4 部構成のハードウェア ID を拡張 INF に追加します。 詳細については、「拡張 INF ファイルの使用」を参照してください。

## <a name="related-pages"></a>関連するページ

### <a name="hardware-dev-center"></a>ハードウェア デベロッパー センター

* [ハードウェアの申請](hardware-certification-submissions.md)

* [ドライバーのフライティング](driver-flighting.md)

* [配送先住所ラベルでドライバーの配布を管理する](driver-flighting.md)

* [Windows Update への公開](publish-a-driver-to-windows-update.md)

### <a name="windows-drivers"></a>Windows ドライバー

* [ユニバーサル INF ファイルの使用](https://docs.microsoft.com/windows-hardware/drivers/install/using-a-universal-inf-file)

* [ユニバーサル ドライバーの概要](https://docs.microsoft.com/windows-hardware/drivers/develop/getting-started-with-universal-drivers)

* [コンポーネント INF ファイルの使用](https://docs.microsoft.com/windows-hardware/drivers/install/using-a-component-inf-file)

* [Windows によるドライバーのランキング方法](https://docs.microsoft.com/windows-hardware/drivers/install/how-setup-ranks-drivers--windows-vista-and-later-)
