---
title: デバイス メタデータ エクスペリエンスを申請する際のエラーと解決方法
description: デバイス メタデータ エクスペリエンスを申請する際のエラーと解決方法
ms.assetid: 793b4c92-96e8-4b3e-a7de-d00e953c983a
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83b8d0122497f7c429d922cd0f58b604e7799244
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57348959"
---
# <a name="errors-and-solutions-when-submitting-device-metadata-experiences"></a>デバイス メタデータ エクスペリエンスを申請する際のエラーと解決方法


デバイス メタデータ エクスペリエンスの検証/発行依頼を送信すると、エクスペリエンスのリリースに影響するエラーが発生する場合があります。

## <a name="span-idcommonerrorsspanspan-idcommonerrorsspanspan-idcommonerrorsspancommon-errors"></a><span id="Common_errors"></span><span id="common_errors"></span><span id="COMMON_ERRORS"></span>一般的なエラー


ここでは、最も一般的なエラーをアルファベット順に掲載し、可能であれば解決策も紹介しています。

### <a name="span-idtosolvecommonerrorsspanspan-idtosolvecommonerrorsspanspan-idtosolvecommonerrorsspanto-solve-common-errors"></a><span id="To_solve_common_errors"></span><span id="to_solve_common_errors"></span><span id="TO_SOLVE_COMMON_ERRORS"></span>一般的なエラーを解決するには

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>エラー</th>
<th>推奨される解決策</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>[CategoryName] Category id is incorrect in Behavior.xml. (Behavior.xml の [カテゴリ名] カテゴリ ID が正しくありません。)  Correct Category id is [CategoryId] (正しいカテゴリ ID は [カテゴリ ID] です)</p></td>
<td><p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="even">
<td><p>[CategoryName] Guid [CategoryId] is required for your device in Behavior.xml. (Behavior.xml のデバイスに [カテゴリ名] Guid [カテゴリ ID] が必要です。)</p></td>
<td><p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="odd">
<td><p>[FolderName] folder is missing. ([フォルダー名] フォルダーが欠落しています。)</p></td>
<td><p>いずれかのフォルダーが欠落しています。</p>
<p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="even">
<td><p>[FolderName] folder name is required in &lt;PackageStructure&gt; element in PackageInfo.xml. (PackageInfo.xml の &lt;PackageStructure&gt; 要素に [フォルダー名] フォルダー名が必要です。)</p></td>
<td><p>PackageInfo.xml には、正しいフォルダー名参照を含める必要があります。</p>
<p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="odd">
<td><p>[ImageType] Image - [FileName] size for [SplitType] split is invalid. ([分割タイプ] 分割の対象となる [画像の種類] 画像 - [ファイル名] のサイズが無効です。)  Valid size(s) are: [ListOfAllowedSizes] (有効なサイズ: [許容サイズのリスト])</p></td>
<td><p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="even">
<td><p>[ImageType] Image - [FileName] size is invalid. ([画像の種類] 画像 - [ファイル名] のサイズが無効です。)  Valid size(s) are: [ListOfAllowedSizes] (有効なサイズ: [許容サイズのリスト])</p></td>
<td><p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="odd">
<td><p>[TaskGroupName] Guid [TaskGroupGuid] is not referenced for the task [TaskId] in Behavior.xml (Behavior.xml で、タスク [タスク ID] の [タスク グループ名] Guid [タスク グループの GUID] が参照されていません)</p></td>
<td><p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="even">
<td><p>[TaskName] Task - [TaskId] is required for your device within the System Settings category in Behavior.xml. (Behavior.xml の System Settings カテゴリ内のデバイスに、[タスク名] タスク - [タスク ID] が必要です。)</p></td>
<td><p>Action Center タスクと System Settings タスクは、該当デバイスの Device Stage の System Settings カテゴリ下に存在する必要があります。</p>
<p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="odd">
<td><p>[TaskName] Task - [TaskId] should reference taskGroupGuid [TaskGroupGuid] for your device in Behavior.xml. (Behavior.xml では、[タスク名] タスク - [タスク ID] が、デバイスの taskGroupGuid [タスク グループの GUID] を参照する必要があります。)</p></td>
<td><p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="even">
<td><p>[TaskName] task [TaskId] is required to exist at root for your device in Behavior.xml. (Behavior.xml では、[タスク名] タスク [タスク ID] が、デバイスのルートに存在する必要があります。)</p></td>
<td><p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="odd">
<td><p>\DeviceStage\Device[Locale]\ and \DeviceStage\Device\ folders should have same files. (\DeviceStage\Device[Locale]\ and \DeviceStage\Device\ フォルダーに同じファイルが存在する必要があります。)</p></td>
<td><p>このパッケージが既定のロケールに設定されている場合、ロケールのディレクトリと全言語共通のディレクトリには、同じファイルが存在している必要があります。</p>
<p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="even">
<td><p>A .cab submission needs to contain either Hardware and/or Model information. (.cab 提出には、ハードウェアかモデル、またはその両方の情報が含まれている必要があります。)  Please correct the .cab or modify the existing .cabs. (この .cab または既にある .cab を修正してください。)</p></td>
<td><p>パッケージには、ハードウェア ID またはモデル ID が少なくとも 1 つ存在している必要があります。</p>
<p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="odd">
<td><p>A Hardware ID in this .cab is in conflict and the .cab cannot be uploaded. (この .cab 内のハードウェア ID が競合しており、.cab をアップロードできません。)  Please ensure no other experience you have created uses this Hardware ID. (これまでに作成した他のエクスペリエンスにこのハードウェア ID が使われていないか確認してください。)</p></td>
<td><p>ご使用のハードウェア ID は、別のエクスペリエンスで過去に使われたことがあります。 ダッシュボードの <strong>[Device metadata]</strong> (デバイス メタデータ) で、<strong>[Manage experiences]</strong> (エクスペリエンスの管理) ページを開いてください。 フィルターにハードウェア ID を入力して、他のエクスペリエンスを検索します。 競合があれば解決してください。</p>
<p>詳しくは、「<a href="https://docs.microsoft.com/windows-hardware/drivers/dashboard/device-metadata-business-rules" data-raw-source="[Device Metadata Business Rules](https://docs.microsoft.com/windows-hardware/drivers/dashboard/device-metadata-business-rules)">デバイス メタデータのビジネス規則</a>」をご覧ください。</p></td>
</tr>
<tr class="even">
<td><p>A Hardware ID in this. cab is in use by another company and the .cab cannot be uploaded. (この .cab 内のハードウェア ID は別の会社によって使われているため、.cab をアップロードできません。)  Please verify this Hardware ID. (このハードウェア ID を確認してください。)</p></td>
<td><p>パッケージに追加したハードウェア ID が、別の会社によって使われています。 別の会社のハードウェア ID を提出することはできません。 ハードウェア ID のスペルに誤りがないか確認してください。 それでもエラー メッセージが表示される場合は、ダッシュボード サポートにメール (sysdev@microsoft.com) で解決策をお問い合わせください。</p></td>
</tr>
<tr class="odd">
<td><p>A live submission already exists for this locale in this experience. (このエクスペリエンスには、このロケールのライブ提出が既に存在します。)</p></td>
<td><p>ロケールの既存のライブ パッケージを削除してから、同じロケールの新しいパッケージをアップロードしてください。</p></td>
</tr>
<tr class="even">
<td><p>A live submission already exists with default locale set to true in this experience. (このエクスペリエンスには、既定のロケールが true に設定されたライブ提出が既に存在します。)</p></td>
<td><p>既定のパッケージとして設定できるライブ パッケージは、エクスペリエンス内で 1 つだけです。</p>
<p>詳しくは、「<a href="https://docs.microsoft.com/windows-hardware/drivers/dashboard/device-metadata-business-rules" data-raw-source="[Device Metadata Business Rules](https://docs.microsoft.com/windows-hardware/drivers/dashboard/device-metadata-business-rules)">デバイス メタデータのビジネス規則</a>」をご覧ください。</p></td>
</tr>
<tr class="odd">
<td><p>A logo submission for a MultiPurpose device does not match the submission category. (MultiPurpose デバイスのロゴ提出が、提出カテゴリと一致しません。)</p></td>
<td><p>ロゴ提出にリストされているデバイス カテゴリが、デバイス メタデータ パッケージのプライマリ デバイス カテゴリと一致しません。 この問題を解決するには、次の手順を実行します。</p>
<ul>
<li><p>ロゴ提出のデバイス カテゴリを修正します。</p></li>
<li><p>新しいエクスペリエンスを作成し、正しいロゴ提出にバインドします。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>A Model ID in this cab is in conflict and the .cab cannot be uploaded. (この cab 内のモデル ID が競合しており、cab をアップロードできません。)  Please ensure no other experience you have created uses this Model ID. (これまでに作成した他のエクスペリエンスにこのモデル ID が使われていないか確認してください。)</p></td>
<td><p>ご使用のモデル ID は、別のエクスペリエンスで過去に使われたことがあります。 ダッシュボードの <strong>[Device metadata]</strong> (デバイス メタデータ) で、<strong>[Manage experiences]</strong> (エクスペリエンスの管理) ページを開いてください。 フィルターにモデル ID を入力して、他のエクスペリエンスを検索します。 競合があれば解決してください。</p>
<p>詳しくは、「<a href="https://docs.microsoft.com/windows-hardware/drivers/dashboard/device-metadata-business-rules" data-raw-source="[Device Metadata Business Rules](https://docs.microsoft.com/windows-hardware/drivers/dashboard/device-metadata-business-rules)">デバイス メタデータのビジネス規則</a>」をご覧ください。</p></td>
</tr>
<tr class="odd">
<td><p>A Model ID in this cab is in use by another company and the cab cannot be uploaded. (この cab 内のモデル ID は別の会社によって使われているため、cab をアップロードできません。)  Please verify this Model ID. (このモデル ID を確認してください。)</p></td>
<td><p>パッケージに追加したモデル ID が、別の会社によって使われています。 別の会社のモデル ID を提出することはできません。 モデル ID のスペルに誤りがないか確認してください。 それでもエラー メッセージが表示される場合は、ダッシュボード サポートにメール (sysdev@microsoft.com) で解決策をお問い合わせください。</p></td>
</tr>
<tr class="even">
<td><p>A non-preview live package cannot be promoted to live. (プレビュー以外のライブ パッケージをライブに昇格することはできません。)</p></td>
<td><p>ライブ パッケージのステータスを Live (ライブ) に昇格することはできません。</p></td>
</tr>
<tr class="odd">
<td><p>A package with a status of error cannot be promoted to live. (エラー ステータスのパッケージをライブに昇格することはできません。)</p></td>
<td><p>エラーのあるパッケージを Live (ライブ) ステータスに昇格することはできません。</p></td>
</tr>
<tr class="even">
<td><p>A preview submission already exists for this locale in this experience. (このエクスペリエンスには、このロケールのプレビュー提出が既に存在します。)</p></td>
<td><p>この問題を解決するには、次の操作を試します。</p>
<ul>
<li><p>ロケールの既存のプレビュー パッケージを削除してから、同じロケールの新しいプレビュー パッケージをアップロードします。</p></li>
<li><p>ロケールの現在のプレビュー パッケージを Release (リリース) ステータスに昇格してから、同じロケールの新しいプレビュー パッケージをアップロードします。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>A preview submission already exists with default locale set to true in this experience. (このエクスペリエンスには、既定のロケールが true に設定されたプレビュー提出が既に存在します。)</p></td>
<td><p>既定のパッケージとして設定できるプレビュー パッケージは、エクスペリエンス内で 1 つだけです。</p>
<p>詳しくは、「<a href="https://docs.microsoft.com/windows-hardware/drivers/dashboard/device-metadata-business-rules" data-raw-source="[Device Metadata Business Rules](https://docs.microsoft.com/windows-hardware/drivers/dashboard/device-metadata-business-rules)">デバイス メタデータのビジネス規則</a>」をご覧ください。</p></td>
</tr>
<tr class="even">
<td><p>All device metadata .cab files in an experience must support the same Hardware IDs. (1 つのエクスペリエンスに含まれるすべてのデバイス メタデータ .cab ファイルは、同じハードウェア ID をサポートする必要があります。)  Please correct the .cab. (.cab を修正してください。)</p></td>
<td><p>このパッケージのモデル ID のリストが、エクスペリエンス内の他のパッケージのモデル ID のリストと一致しません。 パッケージ内のモデル ID のリストを修正してから、もう一度パッケージをアップロードしてください。</p>
<p>詳しくは、「<a href="https://docs.microsoft.com/windows-hardware/drivers/dashboard/device-metadata-business-rules" data-raw-source="[Device Metadata Business Rules](https://docs.microsoft.com/windows-hardware/drivers/dashboard/device-metadata-business-rules)">デバイス メタデータのビジネス規則</a>」をご覧ください。</p></td>
</tr>
<tr class="odd">
<td><p>Allowed Domain should not be empty for task [TaskID] in Tasks.xml. (Tasks.xml のタスク [タスク ID] の許容ドメインを空にすることは避けてください。)</p></td>
<td><p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="even">
<td><p>An unexpected file was found:'[ExtraFile]'. (予期しないファイルが見つかりました:'[想定外のファイル]'。) Please ensure you follow the architecture or reference all root files in PackageInfo.xml. (アーキテクチャに従うか、PackageInfo.xml 内のすべてのルート ファイルを参照してください。)</p></td>
<td><p>パッケージのルートに余分なファイルが存在します。</p>
<p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="odd">
<td><p>An unexpected folder was found: ‘[ExtraFolder]'. (予期しないフォルダーが見つかりました: ‘[ExtraFolder]'。) Please ensure you follow the architecture or reference all root folders in PackageInfo.xml. (アーキテクチャに従うか、PackageInfo.xml 内のすべてのルート フォルダーを参照してください。)</p></td>
<td><p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="even">
<td><p>CommandLine URL should not be null for task [TaskID] in Tasks.xml. (Tasks.xml のタスク [タスク ID] のコマンド ライン URL を null にすることは避けてください。)</p></td>
<td><p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="odd">
<td><p>Device Category not found in DeviceInfo.xml. (DeviceInfo.xml にデバイス カテゴリが見つかりません。)</p></td>
<td><p>定義済みのオプションのいずれかに該当するプライマリ デバイス カテゴリを設定する必要があります。</p>
<p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="even">
<td><p>Device folder not found in \DeviceStage\ folder (\DeviceStage\ フォルダーにデバイス フォルダーが見つかりません)</p></td>
<td><p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="odd">
<td><p>Device icon information not found in DeviceInfo.xml (DeviceInfo.xml にデバイス アイコン情報が見つかりません)</p></td>
<td><p>DeviceInfo.xml ファイルにデバイス アイコンを含める場合は、デバイス アイコン情報も含める必要があります。 Device Stage パッケージには、デバイス アイコンが必須です。</p>
<p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="even">
<td><p>Device Metadata Category for this submission needs to match the existing experience category. (この提出のデバイス メタデータ カテゴリは、既にあるエクスペリエンス カテゴリと一致する必要があります。)</p></td>
<td><p>このパッケージのデバイスのカテゴリは、このエクスペリエンスの他のパッケージ内のカテゴリと一致しません。 デバイス カテゴリを修正して、もう一度パッケージを提出してください。</p></td>
</tr>
<tr class="odd">
<td><p>Device Metadata Submission Type for this submission needs to match the existing experience category. (この提出のデバイス メタデータの提出の種類は、既にあるエクスペリエンス カテゴリと一致する必要があります。)</p></td>
<td><p>デバイス メタデータの提出の種類が、Device Stage または Devices and Printers (デバイスとプリンター) として定義されています。 Device Stage エクスペリエンスに含めることができるのは、Device Stage パッケージだけです。 同様に、Devices and Printers (デバイスとプリンター) エクスペリエンスに含めることができるのは、Devices and Printers (デバイスとプリンター) パッケージだけです。</p></td>
</tr>
<tr class="even">
<td><p>Device Stage inbox submissions are not allowed for the computer device class. (コンピューター デバイス クラスには、Device Stage インボックス提出は許可されません。)</p></td>
<td><p>パッケージとエクスペリエンスが、Device Stage とコンピューター デバイスを対象としている場合、既にロゴの認定を取得しているか、ロゴの認定を 90 日以内に取得する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>Device Stage is not supported for this device. (このデバイスでは、Device Stage はサポートされません。)</p></td>
<td><p>選択したデバイス カテゴリは、Device Stage ではサポートされていません。</p></td>
</tr>
<tr class="even">
<td><p>Device Stage metadata cannot be submitted for your device [DeviceCategory] (デバイス [デバイス カテゴリ] では、Device Stage メタデータは提出できません。)</p></td>
<td><p>Device Stage 提出は、次のデバイスでのみ許可されます。</p>
<ul>
<li><p>ポータブル メディア プレーヤー</p></li>
<li><p>デジタル スチル カメラ</p></li>
<li><p>携帯電話</p></li>
<li><p>プリンター、FAX 機器</p></li>
<li><p>スキャナー</p></li>
<li><p>コンピューター システム</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Device Stage requires either Marketing Bullets or Status Items to be present in Behavior.xml. (Device Stage では、Marketing Bullets または Status Items が Behavior.xml に存在する必要があります。)</p></td>
<td><p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="even">
<td><p>Device Stage requires LaunchDeviceStageFromExplorer to be set to true for your device in WindowsInfo.xml. (Device Stage では、WindowsInfo.xml で、デバイスの LaunchDeviceStageFromExplorer を true に設定する必要があります。)</p></td>
<td><p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="odd">
<td><p>Device Stage requires LaunchDeviceStageOnDeviceConnect to be set to True for your device in WindowsInfo.xml (Device Stage では、WindowsInfo.xml で、デバイスの LaunchDeviceStageOnDeviceConnect を True に設定する必要があります)</p></td>
<td><p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="even">
<td><p>Device Stage requires ShowDeviceInDisconnectedState to be set to True for your device in WindowsInfo.xml. (Device Stage では、WindowsInfo.xml で、デバイスの ShowDeviceInDisconnectedState を True に設定する必要があります。)</p></td>
<td><p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="odd">
<td><p>Devices and Printers requires LaunchDeviceStageFromExplorer to be set to False for your device in WindowsInfo.xml. (Devices and Printers では、WindowsInfo.xml で、デバイスの LaunchDeviceStageFromExplorer を False に設定する必要があります。)</p></td>
<td><p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="even">
<td><p>Devices and Printers requires LaunchDeviceStageOnDeviceConnect to be set to False for your device in WindowsInfo.xml. (Devices and Printers では、WindowsInfo.xml で、デバイスの LaunchDeviceStageOnDeviceConnect を False に設定する必要があります。)</p></td>
<td><p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="odd">
<td><p>Error in xml file [FileName] : [Error] (XML ファイル [ファイル名] にエラーがあります: [エラー])</p></td>
<td><p>指定された .xml ファイルは、少なくとも 1 つのエラーが存在するため、処理に失敗しました。 ファイルがその対応するスキーマに準拠していることと、名前空間が正しいことを確認してください。</p>
<p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="even">
<td><p>File [FileName] is different in \DeviceStage\Device[Locale]\ and \DeviceStage\Device\ folders. (ファイル [ファイル名] が \DeviceStage\Device[Locale]\ フォルダーと \DeviceStage\Device\ フォルダーとで異なります。)</p></td>
<td><p>このパッケージが既定のロケールとして設定されている場合、ロケールのディレクトリと全言語共通のディレクトリには、同じファイルが存在している必要があります。</p>
<p>次のいずれかのエラーが発生しました。</p>
<ul>
<li><p>同じ名前のファイルが両方のディレクトリに存在するが、実際にはファイルが異なる。</p></li>
<li><p>指定されたファイルが 1 つのディレクトリにしか存在しない。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>File Name PackageInfo.xml is expected in &lt;PackageStructure&gt; element in PackageInfo.xml. (PackageInfo.xml の &lt;PackageStructure&gt; 要素には、ファイル名 PackageInfo.xml が必要です。)</p></td>
<td><p>対象パッケージの PackageInfo.xml ファイルが正しく作成されていません。 パッケージ内の各ルート オブジェクトは、PackageInfo.xml ファイルで &lt;PackageStructure&gt; ノードを使って参照されている必要があります。</p>
<p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="even">
<td><p>Filename [FileReference] is incorrect in &lt;PackageStructure&gt; element in PackageInfo.xml. (PackageInfo.xml の &lt;PackageStructure&gt; 要素のファイル名 [ファイル参照] が正しくありません。) 正しいファイル名: PackageInfo.xml</p></td>
<td><p>PackageInfo.xml ファイル内で &lt;PackageStructure&gt; ノードを使って参照されたファイル名のスペルに誤りがあります。 エラーを修正して、もう一度パッケージを提出してください。</p>
<p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="odd">
<td><p>For Printing and Scanning Devices, LaunchDeviceStageOnDeviceConnect needs to be set to False in WindowsInfo.xml. (Printing and Scanning Devices では、WindowsInfo.xml で、LaunchDeviceStageOnDeviceConnect を False に設定する必要があります。)</p></td>
<td><p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="even">
<td><p>HardwareIDs in this submission: [list of Hardware ID(s)] are not owned by your company. (この提出のハードウェア ID [ハードウェア ID のリスト] を会社は所有していません。)</p></td>
<td><p>個々の SIG によると、リストされているハードウェア ID には、会社によって所有されていない VID が使われています。 この点に誤りがあれば、ダッシュボード サポートまでメール (sysdev@microsoft.com) でご連絡ください。</p></td>
</tr>
<tr class="odd">
<td><p>Hardware IDs in this submission: [list of Hardware ID(s)] do not match the expected list of Hardware IDs from SMBIOS. (この提出のハードウェア ID [ハードウェア ID のリスト] は、SMBIOS に基づくハードウェア ID のリストと一致しません。)</p></td>
<td><p>提出したハードウェア ID は、SMBIOSFields.xml ファイルと共に提出した SMBIOS 情報から生成されていません。</p>
<p>次のいずれかの解決策を試してください。</p>
<ul>
<li><p>ハードウェア ID をもう一度生成し、正しいハードウェア ID をパッケージに含める。</p></li>
<li><p>使用するフィールドを SMBIOSFields.xml ファイルに追加して、正しいハードウェア ID を生成する。</p></li>
</ul>
<p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="even">
<td><p>Hardware IDs in this submission: [list of Hardware ID(s)] fail the Inbox Driver Distribution Agreement (IDDA) list validation. (この提出のハードウェア ID [ハードウェア ID のリスト] は、Inbox Driver Distribution Agreement (IDDA) リストの検証に失敗します。)</p></td>
<td><p>パッケージに追加したハードウェア ID は、Microsoft との Inbox Driver Distribution Agreement (IDDA) にリストされていません。 これらのハードウェア ID を削除し、もう一度提出してください。</p></td>
</tr>
<tr class="odd">
<td><p>Invalid scheme [Scheme] in Allowed Domain for task [TaskID] in Tasks.xml (Tasks.xml のタスク [タスク ID] に対し、Allowed Domain のスキーム [スキーム] が無効です)</p></td>
<td><p>URL は HTTP または HTTPs で始まる必要があります。</p>
<p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="even">
<td><p>Locale not found or is incorrect in PackageInfo.xml (PackageInfo.xml にロケールが見つからないか、誤りがあります)</p></td>
<td><p>PackageInfo.xml ファイルには、RFC 4646 に準拠した、正しい書式の locale タグが存在する必要があります。</p>
<p>ロケールを修正してから、もう一度パッケージを提出してください。</p></td>
</tr>
<tr class="odd">
<td><p>Missing resource reference for [Id] in Resource.xml file in \DeviceStage\Task[TaskID][Locale] folder (\DeviceStage\Task[タスク ID][ロケール] フォルダーの Resource.xml ファイルに、[ID] のリソース参照が存在しません)</p></td>
<td><p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="even">
<td><p>Model IDs are not allowed for [Device Class] submissions. ([デバイス クラス] の提出では、モデル ID は許可されません。)</p></td>
<td><p>このタイプのデバイス クラスでは、デバイス メタデータを提出するときに、モデル ID を使うことはできません。 必ずデバイスのハードウェア ID を使うようにしてください。 コンピューター デバイスのハードウェア ID を検索するには、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="odd">
<td><p>Model Name not found in DeviceInfo.xml (DeviceInfo.xml にモデル名が見つかりません)</p></td>
<td><p>DeviceInfo.xml ファイルが正しく作成されていません。</p>
<p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="even">
<td><p>No preview key can be found for this organization. (この組織のプレビュー キーが見つかりません。)</p></td>
<td><p>プレビュー パッケージをアップロードする前に PreviewKey を設定しておく必要があります。</p>
<p>詳しくは、「<a href="https://docs.microsoft.com/windows-hardware/drivers/dashboard/device-metadata-business-rules" data-raw-source="[Device Metadata Business Rules](https://docs.microsoft.com/windows-hardware/drivers/dashboard/device-metadata-business-rules)">デバイス メタデータのビジネス規則</a>」をご覧ください。</p></td>
</tr>
<tr class="odd">
<td><p>PackageStructure node in PackageInfo.xml is invalid. (PackageInfo.xml の PackageStructure ノードが無効です。)</p></td>
<td><p>PackageInfo.xml ファイルが正しいことを確認してください。</p>
<p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="even">
<td><p>Task [TaskGUID] is required for your device in Behavior.xml. (Behavior.xml のデバイスにタスク [タスクの GUID] が必要です。)</p></td>
<td><p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="odd">
<td><p>Task [TaskID] should not use taskGroupGuid [TaskGroupGuid] (タスク [タスク ID] に taskGroupGuid [タスク グループの GUID] を使うことは避けてください)</p></td>
<td><p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="even">
<td><p>TaskGroupGuid [TaskGroupGuid] should not be used by your device for task [TaskId] (デバイスのタスク [タスク ID] に TaskGroupGuid [タスク グループの GUID] を使うことは避けてください)</p></td>
<td><p>デバイスには該当しない予約済みの GUID を使おうとしています。</p>
<p>次のいずれかの解決策を試してください。</p>
<ul>
<li><p>デバイスでサポートできないタスクの GUID を使わない。</p></li>
<li><p>タスクを作成する場合は、そのタスク用の新しい GUID を生成する。</p></li>
</ul>
<p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="odd">
<td><p>TaskGroupGuid incorrect for taskId [TaskId] in Behavior.xml (Behavior.xml 内のタスク ID [タスク ID] の TaskGroupGuid に誤りがあります)</p></td>
<td><p>タスクの GUID を修正してから、もう一度パッケージを提出してください。</p>
<p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="even">
<td><p>The [FileName] icon file in [FolderName] folder is missing image <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">MissingImageSize</a>. ([フォルダー名] フォルダー内の [ファイル名] アイコン ファイルには、MissingImageSize の画像が存在しません。)</p></td>
<td><p>画像サイズが存在することを確認してください。 存在しない場合は、画像サイズをアイコンに追加してから、もう一度パッケージを提出してください。</p>
<div class="alert">
<strong>注:</strong><br/><p>256x256 の画像レイヤーは、PNG 圧縮形式であることが必要です。 このサイズに BMP 形式は利用できません。 このサイズが BMP 形式で存在する場合は、同じサイズの画像を PNG 形式で作成し、アイコンに追加してから、もう一度パッケージを提出してください。</p>
</div>
<div>

</div>
<p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="odd">
<td><p>The [FileName] icon file in [FolderName] folder is missing image [MissingImageSize]. ([フォルダー名] フォルダー内の [ファイル名] アイコン ファイルには、[欠落している画像サイズ] の画像が存在しません。)</p></td>
<td><p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="even">
<td><p>The cab Friendly Name is not unique to the Experience. (cab のフレンドリ名がエクスペリエンスに対して一意ではありません。)  Please choose another name. (別の名前を選んでください。)</p></td>
<td><p>エクスペリエンスに新しいフレンドリ名を付けて、もう一度提出してください。</p></td>
</tr>
<tr class="odd">
<td><p>The CommandLine argument should point to a valid URL beginning with HTTP or HTTPS for task [TaskID] in Tasks.xml. (CommandLine 引数は、Tasks.xml 内のタスク [タスク ID] の、HTTP または HTTPS で始まる有効な URL を指す必要があります。)</p></td>
<td><p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="even">
<td><p>The device category reported in your Device Metadata package and Logo Submission don't match. (デバイス メタデータ パッケージとロゴ提出とで、報告されたデバイス カテゴリが一致しません。) パッケージ内のデバイス カテゴリに誤りがある場合は、修正してからもう一度アップロードしてください。 If the device category in Logo Submission is incorrect, please fix in Submission Manager and try uploading your package again: [list of links per offending logo submission to SubmissionManager] (ロゴ提出のデバイス カテゴリに誤りがある場合は、Submission Manager で修正し、もう一度パッケージをアップロードしてください: [問題が生じているロゴ提出ごとの SubmissionManager へのリンク])</p></td>
<td><p>申請が受理されるためには、バインドされているロゴ提出とデバイス メタデータ間でデバイス カテゴリが一致している必要があります。 すべてのロゴ提出のデバイス カテゴリが一致していることと、そのデバイス カテゴリが、パッケージのデバイス カテゴリと一致していることを確認してください。</p>
<p>提示されているリンクは Submission Manager へのリンクです。カテゴリに誤りがある場合は、このリンクをたどってロゴ提出のデバイス カテゴリを変更することができます。</p>
<p>問題がすべて解決されたら、もう一度パッケージを提出します。</p></td>
</tr>
<tr class="odd">
<td><p>The Device Metadata Category for this submission does not exist. (この提出にはデバイス メタデータ カテゴリが存在しません。)</p></td>
<td><p>有効ではないデバイス メタデータ カテゴリが使われました。 Windows ハードウェア認定キット (HCK) に記載されている定義済みのデバイス メタデータ カテゴリから選んでください。</p></td>
</tr>
<tr class="even">
<td><p>The Experience name already exists for this organization. (この組織のエクスペリエンス名は既に存在します。)</p></td>
<td><p>名前の異なるエクスペリエンスを新たに作成してください。</p></td>
</tr>
<tr class="odd">
<td><p>The provided Logo submissions do not share Hardware IDs or Model IDs with the Device Metadata submission. (指定されたロゴ提出は、ハードウェア ID またはモデル ID がデバイス メタデータ提出と共有されていません。)</p></td>
<td><p>バインドされたロゴ提出は、エクスペリエンスのデバイス メタデータ パッケージ内のハードウェア ID を含んでいる必要があります。</p></td>
</tr>
<tr class="even">
<td><p>The reference in PackageInfo.xml, DeviceInformation, was not found in the package. (PackageInfo.xml 内で参照されている DeviceInformation がパッケージに見つかりません。)</p></td>
<td><p>DeviceInformation フォルダーの参照が PackageInfo.xml ファイルから欠落しています。</p>
<p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="odd">
<td><p>PackageInfo.xml 内で参照されている DeviceStage がパッケージに見つかりません。</p></td>
<td><p>PackageInfo.xml ファイルの &lt;PackageStructure&gt; 要素内の参照が、正しく綴られていないか、パッケージのルートに置かれていません。 該当する参照を削除するか、正しいファイルまたはディレクトリを追加してください。</p>
<p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="even">
<td><p>The reference in PackageInfo.xml, WindowsInformation, was not found in the package. (PackageInfo.xml 内で参照されている WindowsInformation がパッケージに見つかりません。)</p></td>
<td><p>WindowsInformation フォルダーの参照が PackageInfo.xml ファイルから欠落しています。</p>
<p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="odd">
<td><p>The submission contains [list of Hardware ID(s) and/or Model ID(s)] that are not covered via a logo submission. (ロゴ提出ではカバーされない [ハードウェア ID またはモデル ID のリスト] が提出に含まれています。)</p></td>
<td><p>ロゴ提出でカバーされないハードウェア ID またはモデル ID がパッケージに含まれています。</p>
<p>次のいずれかの解決策を試してください。</p>
<ul>
<li><p>デバイス メタデータ パッケージ内のハードウェア ID またはモデル ID を修正します。</p></li>
<li><p>新しいエクスペリエンスを作成し、関連するロゴ提出にのみバインドします。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>The system manufacturer for this computer submission does not match the organization of the submitting user. (このコンピューター提出のシステム製造元は、提出ユーザーの組織と一致しません。)</p></td>
<td><p>提出した SMBIOSFields.xml ファイルのシステム製造元が、Microsoft の記録にある製造元と一致しません。</p>
<p>次のいずれかの解決策を試してください。</p>
<ul>
<li><p>システム製造元の名前を修正し、もう一度パッケージを提出します。</p></li>
<li><p>システム製造元フィールドが正しいにもかかわらず、ファイルが不合格となる場合は、ダッシュボード サポートまでメール (sysdev@microsoft.com) でお問い合わせください。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>The TaskID [TaskID] cannot be used with multiple TaskGroups. (タスク ID [タスク ID] を複数のタスク グループで使うことはできません。)</p></td>
<td><p>Device Stage パッケージに、別のタスク グループで使われているタスク ID が存在します。 タスク ID は、タスク グループごとに一意で、なおかつタスクごとに一意である必要があります。</p>
<p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="even">
<td><p>This preview key has been rejected. (このプレビュー キーは却下されました。) Please choose another value. (別の値を選んでください。)</p></td>
<td><p>ダッシュボードを使って設定した PreviewKey は受理されません。 新しい PreviewKey を提出してください。</p></td>
</tr>
<tr class="odd">
<td><p>Unexpected file found in [FolderName] folder- [ExtraFile] ([フォルダー名] フォルダーに予期しないファイルが見つかりました: [想定外のファイル])</p></td>
<td><p>パッケージの構造に問題があります。</p>
<p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="even">
<td><p>Unexpected file found in [Path] folder – [ExtraFile] ([パス] フォルダーに予期しないファイルが見つかりました: [想定外のファイル])</p></td>
<td><p>パッケージの構造に問題があります。</p>
<p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="odd">
<td><p>Unexpected file found in the [locale] subfolder of task [TaskGroupGuid] folder – [FileName] (タスク [タスク グループの GUID] フォルダーの [ロケール] サブフォルダーに予期しないファイルが見つかりました: [ファイル名])</p></td>
<td><p>指定されたファイルを削除してから、もう一度パッケージを提出してください。</p>
<p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="even">
<td><p>Unexpected folder found in [FolderName] folder- [ExtraFolder] (予期しないフォルダーが [フォルダー名] フォルダーに見つかりました: [想定外のフォルダー])</p></td>
<td><p>パッケージの構造に問題があります。</p>
<div class="alert">
<strong>注:</strong><br/><p>DeviceInfo.xml ファイル内のデバイス カテゴリが正しく設定されていないと、このエラーが発生する場合があります。</p>
</div>
<div>

</div>
<p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="odd">
<td><p>Unexpected folder found in [Path] folder – [ExtraFolder] (予期しないフォルダーが [パス] フォルダーに存在します: [想定外のフォルダー])</p></td>
<td><p>パッケージの構造に問題があります。</p>
<p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="even">
<td><p>URL should not be a localhost for task [TaskID] in Tasks.xml. (Tasks.xml 内のタスク [タスク ID] の URL を localhost にすることは避けてください。)</p></td>
<td><p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="odd">
<td><p>URL specified in the commandLine is not valid for task [TaskID] in Tasks.xml. (commandLine で指定された URL が、Tasks.xml のタスク [タスク ID] に対して有効ではありません。)</p></td>
<td><p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="even">
<td><p>Valid logo submission(s) are needed for [SubmissionType] metadata for [DeviceClass] ([デバイス クラス] の [提出の種類] メタデータに有効なロゴ提出が必要です)</p></td>
<td><p>デジタル スチル カメラとポータブル メディア プレーヤーには、Windows 7 または Windows Vista® のロゴ提出が少なくとも 1 つ必要です。</p>
<p>携帯電話には、Windows 7 のロゴ提出が少なくとも 1 つ必要です。</p></td>
</tr>
<tr class="odd">
<td><p>You already have a preview submission for this Operating System Version. (このオペレーティング システム バージョンには既にプレビュー提出が存在します。)  Remove the current Live submission. (現在のライブ提出を削除してください。)</p></td>
<td><p>昇格しようとしているロケールのプレビュー パッケージには、既にリリース パッケージが存在します。</p>
<p>このプレビュー パッケージを昇格する場合は、まずリリース パッケージを削除してから再試行してください。</p></td>
</tr>
<tr class="even">
<td><p>You do not have access to this experience. (このエクスペリエンスへのアクセス権がありません。)</p></td>
<td><p>他社のエクスペリエンスにアクセスしようとしています。</p></td>
</tr>
<tr class="odd">
<td><p>Your device cannot have the command value set to HostedSiteWithDevice for task [TaskID] in Tasks.xml. (このデバイスは、Tasks.xml のタスク [タスク ID] のコマンド値を HostedSiteWithDevice に設定することはできません。)</p></td>
<td><p>詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft Device Experience Development Kit</a> に関するページをご覧ください。</p></td>
</tr>
<tr class="even">
<td><p>Your submission is blocked due to a Dashboard error. (ダッシュボードのエラーが原因で提出がブロックされています。)  Please email Dashboard Support at sysdev@microsoft.com for a resolution. (ダッシュボード サポートにメール (sysdev@microsoft.com) で解決策をお問い合わせください。)</p></td>
<td><p>sysdev@microsoft.com のメール ダッシュボード サポート。</p></td>
</tr>
</tbody>
</table>



## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[デバイス メタデータ エクスペリエンスを作成する](https://docs.microsoft.com/windows-hardware/drivers/dashboard/create-a-device-metadata-experience)

[デバイス メタデータ パッケージを申請する (ダッシュボード ヘルプ)](https://docs.microsoft.com/windows-hardware/drivers/dashboard/submit-a-device-metadata-package--dashboard-help-)

[デバイス メタデータのビジネス規則](https://docs.microsoft.com/windows-hardware/drivers/dashboard/device-metadata-business-rules)










