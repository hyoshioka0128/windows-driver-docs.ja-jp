---
title: 複数の Windows バージョンで Microsoft によって署名されたドライバーを取得する
description: 複数のバージョンの Windows で Microsoft によって署名されたドライバーを取得する方法
ms.assetid: 519384F5-986C-4109-8C91-4352DEFF46F9
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67d1b2c8e08ee33c672b45cb49f5fd46be7d999a
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "63335162"
---
# <a name="get-drivers-signed-by-microsoft-for-multiple-windows-versions"></a>複数の Windows バージョンで Microsoft によって署名されたドライバーを取得する

## <a name="how-to-submit-to-the-dashboard"></a>ダッシュボードに提出する方法

このトピックでは、ドライバーなどをダッシュボードに提出し、複数のバージョンの Windows に適用する方法について説明します。 また、Microsoft が署名した後に申請を取得する方法と、Microsoft の署名を検証する方法についても説明します。

ダッシュボード申請を Windows 10 以前のバージョンの Windows に適用するには、次の 2 つの方法があります。

1. Windows 10 に対する申請をテストする場合は Hardware Lab Kit (HCK) を使い、Windows 10 より古いバージョンの Windows に対してテストする場合はハードウェア認定キット (HLK) を使います。 次に、[マージした HLK/HCK テスト結果](https://msdn.microsoft.com/library/windows/hardware/dn939938.aspx)すべてを含むダッシュボード申請を作成します。 申請処理中は、このトピックの後半に示すように、Windows Vista と Windows XP の無料の署名を取得するためにオプトインすることができます。 Windows Server 2008 についてオプトインするには、[Windows Logo Kit (WLK)](https://www.microsoft.com/download/details.aspx?id=39359) 申請の申請 ID を指定します。 この方法でのみ、申請をすべての Windows バージョンに適用できます。
2. HLK と HCK でテストする代わりに、ドライバーに自分で[クロス署名](https://msdn.microsoft.com/library/windows/hardware/dn170454.aspx)し、Windows 10 でも動作するようにダッシュボードに[構成証明署名](attestation-signing-a-kernel-driver-for-public-release.md)を申請することもできます。 この方法のほうが複雑ですが、有効な選択肢です。 とはいえ、この方法で署名された申請は Windows Server 2016 では機能しないことに注意してください。 ドライバーに構成証明署名する方法について詳しくは、「[一般リリースのためのカーネル ドライバーへの構成証明署名](attestation-signing-a-kernel-driver-for-public-release.md)」をご覧ください。
    > [!IMPORTANT]
    > パートナー センターからドライバーの署名を入手できるようになるまで、[ハードウェア デベロッパー センター (Sysdev)](dashboard-services.md) でドライバーに構成証明署名する必要があります。

このトピックでは、コンテキストとしてダッシュボードに関する背景情報について説明し、HLK/HCK を使うための手順を説明します。

ダッシュボードには、申請の署名に関連して 2 つのオプションがあります。どちらの方法でも、Microsoft が署名したドライバーを得ることができます。 ハードウェアの互換性オプションは、貴社が一層の努力をして [Windows ハードウェアの互換性プログラム](https://msdn.microsoft.com/library/windows/hardware/dn922588.aspx)要件を満たしたことを意味します。 これにより、Microsoft SmartScreen での好評価や、認定製品一覧にリストされるなどのビジネス上の利点を得ることができます。

背景には、検討すべきコード署名操作として次の 2 つの操作があります。

- 1 つめの操作は、ダッシュボードに対して組織を識別するコード署名です。 これは、提出しようとしているパッケージの署名で、ダッシュボードがパートナーに求める要件の 1 つです。この要件によって、ダッシュボードは、組織に属さない悪意のある人が、あなたの資格情報を使って申請を行わないようにすることができます (悪意のある人があなたの資格情報を使うと、あなたの評判が傷つけられる可能性があります)。
- もう 1 つの操作は、申請の個々のファイル (ドライバーなど) に Microsoft が実際に署名する操作です。

ダッシュボードで申請機能にアクセスするには、会社にバインドされた EV 証明書が必要です。

[ハードウェア デベロッパー センター (Sysdev)](dashboard-services.md) 内で、組織の識別に使う証明書を確認するには、組織のアカウントの管理者としてログインする必要があります。 **[管理]** &gt; **[Upload a new digital certificate]** (新しいデジタル証明書をアップロード) の順にクリックします。

パートナー センター内で、組織の識別に使う証明書を確認する場合は、「[コード署名証明書の更新](https://msdn.microsoft.com/library/windows/hardware/mt786467)」をご覧ください。

パートナー センターにサインインし、申請に署名する準備ができると、標準的なコード署名証明書か EV コード署名証明書のどちらかを使うことができます。このことは、Windows 10 だけでなくすべてのオペレーティング システム バージョンに当てはまります。

これは、[ポリシーに最近加えられた変更](http://blogs.msdn.com/b/windows_hardware_certification/archive/2015/10/20/update-on-sysdev-ev-certificate-requirement.aspx)です。 組織のアカウントにバインドされている EV 証明書があれば、準備はできています。つまり、パッケージを申請するときにも、標準的な SHA-2 証明書を使い続けることができます。

## <a name="how-to-submit-hlk-test-results"></a>HLK テストの結果を提出する方法

HLK テストの結果をダッシュボードに提出する方法を次に示します。 実行したテストの内容とテスト結果を個別に確認できる複数のタブがあります。 ダッシュボードの目的として、HLK プロジェクトの最も興味深い部分は、 **[パッケージ]** タブです。

![hlk パッケージ](images/hlkpackage.png)

開くには、プロジェクトのファイル パスをクリックします。 この場合は、申請はドライバー 1 つです。

![ドライバー](images/capture.png)

では、申請パッケージをはじめから作成しましょう。 HLK で **[Add Driver Folder]** (ドライバー フォルダーの追加) をクリックします。

![ドライバー フォルダーの追加](images/adddriverfolder.png)

ここで、はじめて、申請でサポートする OS のバージョンを宣言できるようになります。 この場合、申請は Windows 10 x64 とそれ以前の各種バージョンの Windows でテストされました。

![OS 条件指定](images/osqualifications.png)

また、ロケールの宣言を行う必要があります。 たとえば、ドライバーの設計とアーキテクチャに応じて、異なるロケールで異なる文字列を表示するように選択することができます。 その場合は、ロケールごとに別のコンパイルされたバイナリを用意します。 このように、1 つのデバイスに対して、ロケールごとにさまざまなドライバーを用意することができます。

![ロケール](images/locales.png)

シンボルを追加するには、ドライバー フォルダーを右クリックします。

![シンボルの追加](images/addsymbols.png)

**[Add Supplemental Folder]** (補助的なフォルダーの追加) をクリックして、申請で重要だがまだ申請そのものに含まれていないその他のファイルを申請します。 パッケージに必要なすべてのコンテンツを追加できます。 この方法で、ドライバー申請の readme ファイルなど、申請のための重要なその他の項目をダッシュボードに追加できます。

![補助的なフォルダーの追加](images/addsupplementalfolder.png)

準備ができたら、 **[Create Package]** (パッケージの作成) をクリックします。

![パッケージの作成](images/createpackage.png)

次の手順で、パッケージの署名に使う証明書を指定します。これは、このトピックの冒頭で説明した 2 つのコード署名操作の 1 つめの操作です。 **[Use a certificate file]** (証明書ファイルを使用する) をクリックして USB ドライブなどに保存されている証明書を指定するか、 **[Use the certificate store]** (証明書ストアを使用する) をクリックしてローカル コンピューターの証明書ストアにインポートした証明書を指定できます。

![証明書ストアを使用する](images/usecertstore.png)

**[OK]** をクリックした後にパッケージの名前を指定すると、パッケージが作られ署名されて、成功したというメッセージが表示されます (申請に使っているコンピューターに証明書があると仮定しています)。

[パッケージ] の **[Signability]** (署名) に緑色のチェック マークが表示されます。

![署名](images/signability.png)

次の手順は、パートナー センター ダッシュ ボードで行います。 サインインし、「[新しいハードウェア提出の作成](create-a-new-hardware-submission.md)」の手順に従って HLK パッケージをアップロードします。

## <a name="how-to-retrieve-a-submission-after-microsoft-signs-it"></a>Microsoft の署名後に申請を取得する方法

パートナー センターに提出した HLK または HCK 提出の場合:

- 署名されたファイルをダウンロードするドライバーが含まれている[ハードウェア提出を検索します](manage-your-hardware-submissions.md)。 ID を選択してドライバーの詳細を開きます。 そのページで、ダウンロードするドライバーが含まれているパッケージのパッケージ タブを展開し、[署名済みファイルのダウンロード] をクリックします。

ハードウェア デベロッパー センター (Sysdev) に提出した WLK 提出、システム提出、または構成証明署名済みドライバーの場合:

- **[ハードウェアの互換性]** &gt; **[送信の管理]** &gt; の順に選択したときに、 **[Summary and Tasks]** (概要とタスク) タブの [状態] が **[承認済み]** になっていた場合は、申請を取得する準備ができています。 画面の右下隅の **[ダウンロード]** の下の **[Signed driver package]** (署名済みドライバー パッケージ) をクリックします。 Microsoft では、署名済みの申請を含むインメモリ zip ファイルをストリーム配信します。

申請フォルダーにはパッケージ ファイルが含まれます。 これらのファイルは、Microsoft によって署名されています。 パートナーは、返されたペイロードに署名する必要はありません。 Microsoft は、常に、承認済みの申請に .cat ファイルを添付して返します。 パートナーが独自の .cat ファイルを含めた場合は、 Microsoft はこれを破棄し、Microsoft の署名済み .cat ファイルを返します。

以前は、Microsoft は .cat ファイルのみに署名していました。 Windows 10 以降、Microsoft は返すペイロードに含まれるすべてのポータブル実行可能ファイルに署名するようになりました。 たとえば、ここでは、.dll ファイルも Microsoft によって署名されています。

![Microsoft によって署名されたファイル](images/filessignedbymicrosoft.png)

## <a name="how-to-validate-the-microsoft-signature"></a>Microsoft 署名を検証する方法

次のような場合、申請の Microsoft 署名を検証したいと考えることがあります。

1. ドライバーが Microsoft によって署名されているかどうか不明で、確認したい場合。
2. 2 つのドライバーがあり、どちらが構成証明によって署名されているか、どちらが HLK/HCK の結果をダッシュボードに申請した後に署名されたか判断する必要がある場合。

Microsoft 署名を検証するには、Microsoft が申請の署名に使う証明書の拡張キー使用法 (EKU) を確認します。 EKU を確認するには、.cat ファイルを右クリックし、 **[プロパティ]** をクリックします。 **[デジタル署名]** タブをクリックして、証明書の名前、 **[詳細]** の順にクリックします。

![EKU の詳細](images/ekudetails.png)

証明書の **[詳細]** タブで、 **[拡張キー使用法]** をクリックします。 証明書の EKU と対応する OID の値が表示されます。 ここでは、 **[Windows Hardware Driver Verification OID]** (Windows ハードウェア ドライバーの検証 OID) の末尾が 5 ですが、これはドライバーが構成証明で署名されていないことを意味します。

![認定](images/certified.png)

ドライバーが構成証明で署名されている場合は、OID の末尾は 1 になります。

![構成証明署名済み](images/attested.png)

## <a name="related-topics"></a>関連トピック

- [新しいハードウェア申請を作成する](create-a-new-hardware-submission.md)

- [パートナー センターでハードウェア申請を管理する](manage-your-hardware-submissions.md)

- [ドライバーのフライティング](driver-flighting.md)
