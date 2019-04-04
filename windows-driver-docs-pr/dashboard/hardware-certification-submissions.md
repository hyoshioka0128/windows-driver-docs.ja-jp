---
title: ハードウェアの提出
description: ハードウェアの提出
ms.assetid: 7EFA9617-CF1D-4259-B0C4-A9DDCF5C3A1F
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1920cbd7bbec599f6d50679a8d994af5bd64bb1
ms.sourcegitcommit: a678a339f09fbd56a3a6124c0fe86194fedb2ed0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/07/2019
ms.locfileid: "57560619"
---
# <a name="hardware-submissions"></a>ハードウェアの提出

Windows ハードウェア互換性プログラム (Windows 10 の場合) と Windows ハードウェア認定プログラム (Windows 8 または 8.1 と以前のオペレーティング システムの場合) では、事前にハードウェアとドライバーを設計、作成、テストしたうえで、最終バージョンをパートナー センターで提出できます。 詳しくは、「[Windows ハードウェア認定](https://go.microsoft.com/fwlink/p/?LinkId=224782)」ページをご覧ください。 Windows 用のハードウェア デバイス、システム、ドライバーが認定されると、互換性リスト、信頼性リスト、ロゴ アートワーク、プロモーション パートナーシップなどの Microsoft マーケティング リソースのサポートが受けられるようになります。

デバイスを開発するには、[Windows Driver Kit (WDK)](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk) をダウンロードします。

デバイスをテストするには、Windows 10 用の [Windows Hardware Lab Kit (Windows HLK)](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit) をダウンロードします。 以前のオペレーティング システムの場合、[Windows ハードウェア認定キット (Windows HCK)](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit) または [Windows Logo Kit (WLK)](https://go.microsoft.com/fwlink/p/?LinkId=219237) をダウンロードします。

製品を開発しテストしたら、ハードウェア提出で結果を提出できます。

> [!NOTE]
> HLK パッケージの一部としてパブリック ドライバー シンボルを含めることを強くお勧めします。 シンボルを含めた場合、[ドライバー信頼性レポート](driver-failure-reporting.md)に返されるデータの質が向上し、外部と共有されることはありません。  パブリック シンボルを作成する方法については、「[パブリック シンボルとプライベート シンボル](../devtest/public-symbols-and-private-symbols.md)」をご覧ください。  「[Step 8: Create a submission package (手順 8: 申請パッケージを作成する)](https://docs.microsoft.com/windows-hardware/test/hlk/getstarted/step-8-create-a-submission-package)」で、パッケージにシンボルを含める方法をご覧ください。 申請内の .pdb ファイルは公開される前に削除されることに注意してください。

- HLK パッケージまたは HCK パッケージを提出するには、「[新しいハードウェア提出の作成](create-a-new-hardware-submission.md)」をご覧ください。

- WLK パッケージを申請する方法については、「[Create a new WLK device certification submission (新しい WLK デバイス認定申請を作成する)](create-a-new-hardware-logo-submission.md)」をご覧ください。

## <a name="drivers-summary-page"></a>[Drivers] (ドライバー) 概要ページ

[Drivers] (ドライバー) 概要ページには、作成または共有しているすべてのハードウェア認定提出の一覧が表示されます。 **[Create new driver]** (新しいドライバーの作成) ボタンを選ぶと、新しいハードウェア提出を作成できます。

![[Drivers] (ドライバー) 概要ページを示すスクリーンショット](images/drivers-summary-page.png)

ハードウェア認定提出の一覧には、各提出に関して次の情報が表示されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>列</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ID</strong></p></td>
<td><p>ドライバーの ID。</p></td>
</tr>
<tr class="even">
<td><p><strong>名前</strong></p></td>
<td><p>提出の作成プロセス中に <strong>[Driver name]</strong> (ドライバー名) で指定した名前。</p></td>
</tr>
<tr class="odd">
<td><p><strong>状態</strong></p></td>
<td><p>提出の現在の状態。 設定可能な値は、次のとおりです。</p>
<ul>
<li>Package acceptance (パッケージの受け入れ): 申請パッケージは、書式設定とコンテンツが適切かどうかを調べる一次審査に合格しました。</li>
<li>Preparation (準備): 今後のレビューと署名のためにパッケージを準備しています。</li>
<li>Validation (検証): ポリシーへの準拠と技術上の正確性を調べるためにパッケージを検証しています。</li>
<li>Manual review (手動による評価): パッケージのコンテンツを自動検証できなかったため、Microsoft の担当者がさらに詳しく調べています。</li>
<li>Catalog creation (カタログの作成): ドライバー用のセキュリティ カタログを作成しています。</li>
<li>Sign (署名): Microsoft の署名をセキュリティ カタログとバイナリに適用しています。</li>
<li>Finalize (最終処理): 完了処理中であり、ドライバーの準備は間もなく整います。</li>
<li>Completed (完了): 申請は完了しました。</li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Certification type (認定の種類)</strong></p></td>
<td><p>提出の認定の種類。 これには、HLK または HCK のいずれかを指定できます。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Created date (作成日)</strong></p></td>
<td><p>ご自身またはドライバーを共有している他のユーザーが、ドライバーをアカウントに追加した日付。</p></td>
</tr>
<tr class="even">
<td><p>[<strong>アクセス許可</strong>]</p></td>
<td><p>提出のためのアクセス許可。 設定可能な値は、次のとおりです。</p>
<ul>
<li>作成者:ドライバーの作成者。 すべてのタスクを完了し、パートナーとドライバーを共有することができます。</li>
<li>発行元:ドライバーはお客様と共有されています。 ドライバーをダウンロードし、Windows Update の出荷ラベルを作成して、DUA パッケージを作成できます。 他の会社とドライバーを共有することはできません。</li>
<li>Read-only (読み取り専用): ドライバーはお客様に代わって Windows Update に申請されました。 ドライバーの詳細を表示し、ドライバーをダウンロードし、お客様に代わって提出された出荷ラベルを表示できます。 出荷ラベルの作成や DUA パッケージの作成を行うことはできません。</li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>ソース</strong></p></td>
<td><p>提出の作成者 (組織名として表示されます)。</p></td>
</tr>
</tbody>
</table>

検索ボックスを使うと、特定の提出または提出セットを検索できます。 **ID**、**Name** (名前)、**State** (状態)、**Certification type** (認定の種類) の各列の値を完全一致または部分一致で検索できます。

## <a name="hardware-submission-page"></a>[Hardware submission] (ハードウェアの提出) ページ

[Hardware submission] (ハードウェアの提出) ページには、特定のハードウェア提出についての情報 (状態、パッケージ、認定情報、出荷ラベルなど) が含まれています。 ハードウェア提出を作成する方法について詳しくは、「[新しいハードウェア提出の作成](create-a-new-hardware-submission.md)」をご覧ください。

![[Hardware submission] (ハードウェアの提出) ページを示すスクリーンショット](images/hardware-submission-page.png)

ページの左側に、最近表示した 10 個の提出の一覧が表示されます。

ページ上部にある進行状況トラッカーで提出の進行状況を監視できます。 すべての手順に緑色のチェック マークが表示されたら、提出は完了となり、会社は通知を受け取ります。

### <a name="packages-and-signing-properties"></a>Packages and signing properties (パッケージと署名のプロパティ)

このセクションでは、パッケージの管理方法が示されます。

新しいパッケージをアップロードするには、**[Upload new]** (新規アップロード) を選びます。

DUA シェル パッケージをダウンロードするには、**[Download DUA shell]** (DUA シェルのダウンロード) を選びます。 DUA を使って提出を更新する方法について詳しくは、「[ハードウェア提出の管理](manage-your-hardware-submissions.md)」をご覧ください。

アップロードされたパッケージの一覧に、この提出のためにアップロードしたパッケージが表示されます。 カーソルでパッケージを展開します。 これにより、提出 ID が表示されるため、**[Download package]** (パッケージのダウンロード) を選んでパッケージをダウンロードできます。

**[Additional certifications]** (その他の認定) には、選んだその他の認定が表示されます。

### <a name="certification"></a>認定

このセクションには、認定情報が表示されます。 このセクションを展開するには、**[See more info]** (詳細情報の表示) を選びます。 指定した認定情報を確認できます。認定情報には以下が含まれます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>フィールド</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Is this a Universal Windows driver? (これはユニバーサル Windows ドライバーですか?)</p></td>
<td><p>ドライバーがユニバーサル Windows プラットフォームの要件を満たしているかどうかを示します。 詳しくは、「<a href="https://docs.microsoft.com/windows-hardware/drivers/develop/getting-started-with-universal-drivers" data-raw-source="[Getting Started with Universal Windows drivers](https://docs.microsoft.com/windows-hardware/drivers/develop/getting-started-with-universal-drivers)">ユニバーサル Windows ドライバーの概要</a>」をご覧ください。</p></td>
</tr>
<tr class="even">
<td><p>What type of device? (デバイスの種類)</p></td>
<td><p>デバイスが次の種類であることを示します。</p>
<ul>
<li><p>内部コンポーネント: システムの一部として PC 内部に接続されるデバイス。</p></li>
<li><p>外部コンポーネント: PC に接続される外部デバイス (周辺機器)。</p></li>
<li><p>その両方: 内部的に (PC 内で) 接続できるほか、外部的にも (周辺機器として) 接続できるデバイス。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Select metadata category (メタデータ カテゴリの選択)</p></td>
<td><p>選択したデバイス メタデータ カテゴリ。</p>
<p>必要に応じて、Sysdev 参照 ID を生成して、デベロッパー センターのハードウェア提出と Sysdev のデバイス メタデータ提出を結び付けることができます。</p></td>
</tr>
<tr class="even">
<td><p>Announcement date (発表日)</p></td>
<td><p>Windows Server Catalog、Windows Certified Product List、ユニバーサル ドライバーの一覧に製品を含める日付。 既定の設定は <strong>[今日]</strong> です。</p></td>
</tr>
<tr class="odd">
<td><p>Marketing names (マーケティング名)</p></td>
<td><p>マーケティング名。 マーケティング名には、製品のエイリアスを指定できます。 必要なだけ多くの名前を指定できます。</p></td>
</tr>
</tbody>
</table>

申請には、申請のコンテンツ全体に基づく宣言属性およびユニバーサル属性が自動的に割り当てられます。  申請を `Declarative=True` または `Universal=True` としてマークする場合、申請内のすべてのファイルと INF は適切な属性に準拠している必要があります。  たとえば、マージされた HLK パッケージには、さまざまな OS 認定のための 2 つのドライバー セットを含めることができます。 1 つのセットが宣言で、もう 1 つのセットが宣言ではない場合は、申請全体を `Declarative=False` としてマークします。 各セットは、2 つの申請に分けて、適切にマークする必要があります。 

発表日を追加または更新する場合、**[Announcement date (UTC)]** (発表日 (UTC)) フィールドで、**[Submit]** (提出) を選びます。

マーケティング名を追加または削除することもできます。 名前を追加するには、**[Marketing name]** (マーケティング名) テキスト ボックスに名前を入力し、**[Add]** (追加) を選びます。 名前を削除するには、削除するマーケティング名の横にある赤い [X] ボタンを選びます。 **[Add multiple names]** (複数の名前の追加) を選んで、一度に複数の名前を追加することもできます。 作業が完了したら、**[Submit]** (提出) を選びます。

### <a name="distribution"></a>配布

このセクションには、この提出の出荷ラベル情報が表示されます。 出荷ラベルの使用方法について詳しくは、「[出荷ラベルによるドライバーの配布の管理](manage-driver-distribution-by-submission.md)」セクションをご覧ください。

新しい出荷ラベルを作成するには、**[New shipping label]** (新しい出荷ラベル) を選びます。

まだ公開されていない出荷ラベルをすべて公開するには、**[Publish all pending]** (保留中の出荷ラベルをすべて公開) を選びます。

出荷ラベルの一覧に、この提出の出荷ラベルが表示されます。 この一覧には作成した出荷ラベルと、パートナーによる共有ドライバーの出荷ラベルが含まれます。 出荷ラベルの詳細を表示するには、出荷ラベル名を選びます。 出荷ラベルの一覧に、各ラベルに関する次の情報が表示されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>フィールド</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>名前</p></td>
<td><p>出荷ラベルの名前。 出荷ラベルの詳細を表示するには、この名前を選びます。</p></td>
</tr>
<tr class="even">
<td><p>作成者</p></td>
<td><p>出荷ラベル作成者の<strong>発行者表示名</strong>。 これにより、どのビジネス パートナーがドライバーを送信したのかを簡単に追跡できます。</p></td>
</tr>
<tr class="odd">
<td><p>宛先</p></td>
<td><p>Windows Update 出荷ラベルの場合、配布先は "Windows Update" です。</p>
<p>共有ドライバーの場合、配布先は出荷ラベルの作成時に <strong>[Who is publishing?]</strong> (公開元はだれですか?) で選んだ会社の<strong>発行者の表示名</strong>です。 これにより、ドライバーを共有したすべての会社を簡単に表示できます。</p></td>
</tr>
<tr class="even">
<td><p>作成日</p></td>
<td><p>出荷ラベルの作成日。</p></td>
</tr>
<tr class="odd">
<td><p>リリース日</p></td>
<td><p>出荷ラベルのリリース日。</p></td>
</tr>
<tr class="even">
<td><p>User created (ユーザーが作成)</p></td>
<td><p>出荷ラベルがお客様の会社で作成された場合、出荷ラベルを作成したユーザーの詳細が表示されます。 これにより、作成に関する質問がある場合はフォローアップできます。 ラベルを作成したのが別の会社である場合、このフィールドは適用されません。</p></td>
</tr>
<tr class="odd">
<td><p>User changed (変更したユーザー)</p></td>
<td><p>出荷ラベルがお客様の会社で作成された場合、出荷ラベルを最後に変更したユーザーの詳細が表示されます。 これにより、変更に関する質問がある場合はフォローアップできます。 ラベルを作成したのが別の会社である場合、このフィールドは適用されません。</p></td>
</tr>
</tbody>
</table>

状態グラフィックには各出荷ラベルの発行状態が表示されます。 緑色のチェック マークはラベルが公開されたことを意味します。 黄色い円はラベルがまだ公開されていないことを意味します。

## <a name="in-this-section"></a>このセクションの内容

- [新しいハードウェア申請を作成する](create-a-new-hardware-submission.md)

- [ハードウェアの申請を管理する](manage-your-hardware-submissions.md)
