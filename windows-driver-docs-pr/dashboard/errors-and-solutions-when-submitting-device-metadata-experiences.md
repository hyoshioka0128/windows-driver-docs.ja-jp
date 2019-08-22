---
title: デバイス メタデータ エクスペリエンスを申請する際のエラーと解決方法
description: デバイス メタデータ エクスペリエンスを申請する際のエラーと解決方法
ms.assetid: 793b4c92-96e8-4b3e-a7de-d00e953c983a
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19542734f4689dc23db5f87f211aadb34b15e7ef
ms.sourcegitcommit: 8486945726d87cf983a7035360059d9f9ab765a7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2019
ms.locfileid: "68808266"
---
# <a name="errors-and-solutions-when-submitting-device-metadata-experiences"></a>デバイス メタデータ エクスペリエンスを申請する際のエラーと解決方法

デバイス メタデータ エクスペリエンスの検証/発行依頼を送信すると、エクスペリエンスのリリースに影響するエラーが発生する場合があります。

## <a name="common-errors"></a>一般的なエラー

ここでは、最も一般的なエラーをアルファベット順に掲載し、可能であれば解決策も紹介しています。

### <a name="to-solve-common-errors"></a>一般的なエラーを解決するには

|エラー|推奨される解決策|
|----|----|
|:::no-loc text="\[CategoryName] Category id is incorrect in Behavior.xml. Correct Category id is \[CategoryId]"::: | 詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。 |
|:::no-loc text="\[CategoryName] Guid \[CategoryId] is required for your device in Behavior.xml.":::|詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="\[FolderName] folder is missing.":::|いずれかのフォルダーが欠落しています。 詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="\[FolderName] folder name is required in <PackageStructure> element in PackageInfo.xml.":::|PackageInfo.xml には、正しいフォルダー名参照を含める必要があります。 詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="\[ImageType] Image – \[FileName] size for \[SplitType] split is invalid. Valid size(s) are: \[ListOfAllowedSizes]":::|詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="\[ImageType] Image – \[FileName] size is invalid. Valid size(s) are: \[ListOfAllowedSizes]":::|詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="\[TaskGroupName] Guid \[TaskGroupGuid] is not referenced for the task \[TaskId] in Behavior.xml":::|詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="\[TaskName] Task – \[TaskId] is required for your device within the System Settings category in Behavior.xml.":::|Action Center タスクと System Settings タスクは、該当デバイスの Device Stage の System Settings カテゴリ下に存在する必要があります。 詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="\[TaskName] Task – \[TaskId] should reference taskGroupGuid \[TaskGroupGuid] for your device in Behavior.xml.":::|詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="\[TaskName] task \[TaskId] is required to exist at root for your device in Behavior.xml.":::|詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="\DeviceStage\Device\[Locale]\ and \DeviceStage\Device\ folders should have same files.":::|このパッケージが既定のロケールに設定されている場合、ロケールのディレクトリと全言語共通のディレクトリには、同じファイルが存在している必要があります。 詳細については、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページを参照してください。|
|:::no-loc text="A .cab submission needs to contain either Hardware and/or Model information. Please correct the .cab or modify the existing .cabs.":::|パッケージには、ハードウェア ID またはモデル ID が少なくとも 1 つ存在している必要があります。 詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="A Hardware ID in this .cab is in conflict and the .cab cannot be uploaded. Please ensure no other experience you have created uses this Hardware ID.":::|ご使用のハードウェア ID は、別のエクスペリエンスで過去に使われたことがあります。 ダッシュボードの **[Device metadata]** (デバイス メタデータ) で、 **[Manage experiences]** (エクスペリエンスの管理) ページを開いてください。 フィルターにハードウェア ID を入力して、他のエクスペリエンスを検索します。 競合があれば解決してください。 詳しくは、「[デバイス メタデータのビジネス規則](https://docs.microsoft.com/windows-hardware/drivers/dashboard/device-metadata-business-rules)」をご覧ください。|
|:::no-loc text="A Hardware ID in this. cab is in use by another company and the .cab cannot be uploaded. Please verify this Hardware ID.":::|パッケージに追加したハードウェア ID が、別の会社によって使われています。 別の会社のハードウェア ID を提出することはできません。 ハードウェア ID のスペルに誤りがないか確認してください。 それでもエラー メッセージが表示される場合は、ダッシュボード サポートにお問い合わせください。|
|:::no-loc text="A live submission already exists for this locale in this experience.":::|ロケールの既存のライブ パッケージを削除してから、同じロケールの新しいパッケージをアップロードしてください。|
|:::no-loc text="A live submission already exists with default locale set to true in this experience.":::|既定のパッケージとして設定できるライブ パッケージは、エクスペリエンス内で 1 つだけです。 詳しくは、「[デバイス メタデータのビジネス規則](https://docs.microsoft.com/windows-hardware/drivers/dashboard/device-metadata-business-rules)」をご覧ください。|
|:::no-loc text="A logo submission for a MultiPurpose device does not match the submission category.":::|ロゴ提出にリストされているデバイス カテゴリが、デバイス メタデータ パッケージのプライマリ デバイス カテゴリと一致しません。 この問題を解決するには、次の手順を実行します。<br/> \- ロゴ提出のデバイス カテゴリを修正します。<br/>\- 新しいエクスペリエンスを作成し、正しいロゴ提出にバインドします。|
|:::no-loc text="A Model ID in this cab is in conflict and the cab cannot be uploaded. Please ensure no other experience you have created uses this Model ID.":::|ご使用のモデル ID は、別のエクスペリエンスで過去に使われたことがあります。 ダッシュボードの **[Device metadata]** (デバイス メタデータ) で、 **[Manage experiences]** (エクスペリエンスの管理) ページを開いてください。 フィルターにモデル ID を入力して、他のエクスペリエンスを検索します。 競合があれば解決してください。 詳しくは、「[デバイス メタデータのビジネス規則](https://docs.microsoft.com/windows-hardware/drivers/dashboard/device-metadata-business-rules)」をご覧ください。|
|:::no-loc text="A Model ID in this cab is in use by another company and the cab cannot be uploaded. Please verify this Model ID.":::|パッケージに追加したモデル ID が、別の会社によって使われています。 別の会社のモデル ID を提出することはできません。 モデル ID のスペルに誤りがないか確認してください。 それでもエラー メッセージが表示される場合は、ダッシュボード サポートにメール (sysdev@microsoft.com) で解決策をお問い合わせください。|
|:::no-loc text="A non-preview live package cannot be promoted to live.":::|ライブ パッケージのステータスを Live (ライブ) に昇格することはできません。|
|:::no-loc text="A package with a status of error cannot be promoted to live.":::|エラーのあるパッケージを Live (ライブ) ステータスに昇格することはできません。|
|:::no-loc text="A preview submission already exists for this locale in this experience.":::|この問題を解決するには、次の操作を試します。<br/> \- ロケールの既存のプレビュー パッケージを削除してから、同じロケールの新しいプレビュー パッケージをアップロードします。<br/>\- ロケールの現在のプレビュー パッケージを Release (リリース) ステータスに昇格してから、同じロケールの新しいプレビュー パッケージをアップロードします。|
|:::no-loc text="A preview submission already exists with default locale set to true in this experience.":::|既定のパッケージとして設定できるプレビュー パッケージは、エクスペリエンス内で 1 つだけです。 詳しくは、「[デバイス メタデータのビジネス規則](https://docs.microsoft.com/windows-hardware/drivers/dashboard/device-metadata-business-rules)」をご覧ください。|
|:::no-loc text="All device metadata .cab files in an experience must support the same Hardware IDs. Please correct the .cab.":::|このパッケージのモデル ID のリストが、エクスペリエンス内の他のパッケージのモデル ID のリストと一致しません。 パッケージ内のモデル ID のリストを修正してから、もう一度パッケージをアップロードしてください。 詳しくは、「[デバイス メタデータのビジネス規則](https://docs.microsoft.com/windows-hardware/drivers/dashboard/device-metadata-business-rules)」をご覧ください。|
|:::no-loc text="Allowed Domain should not be empty for task [TaskID] in Tasks.xml.":::|詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="An unexpected file was found:'\[ExtraFile]'. Please ensure you follow the architecture or reference all root files in PackageInfo.xml.":::|パッケージのルートに余分なファイルが存在します。 詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="An unexpected folder was found: ‘\[ExtraFolder]'. Please ensure you follow the architecture or reference all root folders in PackageInfo.xml.":::|詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="CommandLine URL should not be null for task \[TaskID] in Tasks.xml.":::|詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="Device Category not found in DeviceInfo.xml .":::|定義済みのオプションのいずれかに該当するプライマリ デバイス カテゴリを設定する必要があります。 詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="Device folder not found in \DeviceStage\ folder":::|詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="Device icon information not found in DeviceInfo.xml":::|DeviceInfo.xml ファイルにデバイス アイコンを含める場合は、デバイス アイコン情報も含める必要があります。 Device Stage パッケージには、デバイス アイコンが必須です。 詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="Device Metadata Category for this submission needs to match the existing experience category.":::|このパッケージのデバイスのカテゴリは、このエクスペリエンスの他のパッケージ内のカテゴリと一致しません。 デバイス カテゴリを修正して、もう一度パッケージを提出してください。|
|:::no-loc text="Device Metadata Submission Type for this submission needs to match the existing experience category.":::| デバイス メタデータの提出の種類が、Device Stage または Devices and Printers (デバイスとプリンター) として定義されています。 Device Stage エクスペリエンスに含めることができるのは、Device Stage パッケージだけです。 同様に、Devices and Printers (デバイスとプリンター) エクスペリエンスに含めることができるのは、Devices and Printers (デバイスとプリンター) パッケージだけです。|
|:::no-loc text="Device Stage inbox submissions are not allowed for the computer device class.":::|パッケージとエクスペリエンスが、Device Stage とコンピューター デバイスを対象としている場合、既にロゴの認定を取得しているか、ロゴの認定を 90 日以内に取得する必要があります。|
|:::no-loc text="Device Stage is not supported for this device.":::|選択したデバイス カテゴリは、Device Stage ではサポートされていません。|
|:::no-loc text="Device Stage metadata cannot be submitted for your device \[DeviceCategory]":::|Device Stage 提出は、次のデバイスでのみ許可されます。<br/>\- ポータブル メディア プレーヤー<br/>\- デジタル スチル カメラ<br/>\- 携帯電話<br/>\- プリンター、FAX 機器<br/>\- スキャナー<br/>\- コンピューター システム|
|:::no-loc text="Device Stage requires either Marketing Bullets or Status Items to be present in Behavior.xml.":::|詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="Device Stage requires LaunchDeviceStageFromExplorer to be set to true for your device in WindowsInfo.xml.":::|詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="Device Stage requires LaunchDeviceStageOnDeviceConnect to be set to True for your device in WindowsInfo.xml":::|詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="Device Stage requires ShowDeviceInDisconnectedState to be set to True for your device in WindowsInfo.xml.":::|詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="Devices and Printers requires LaunchDeviceStageFromExplorer to be set to False for your device in WindowsInfo.xml.":::|詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="Devices and Printers requires LaunchDeviceStageOnDeviceConnect to be set to False for your device in WindowsInfo.xml.":::|詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="Error in xml file \[FileName] : \[Error]":::|指定された .xml ファイルは、少なくとも 1 つのエラーが存在するため、処理に失敗しました。 ファイルがその対応するスキーマに準拠していることと、名前空間が正しいことを確認してください。 詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="File \[FileName] is different in \DeviceStage\Device\[Locale]\ and \DeviceStage\Device\ folders.":::|このパッケージが既定のロケールとして設定されている場合、ロケールのディレクトリと全言語共通のディレクトリには、同じファイルが存在している必要があります。 次のいずれかのエラーが発生しました。 <br/>\- 同じ名前のファイルが両方のディレクトリに存在するが、実際にはファイルが異なる。<br/>\- 指定されたファイルが 1 つのディレクトリにしか存在しない。|
|:::no-loc text="File Name PackageInfo.xml is expected in &lt;PackageStructure&gt; element in PackageInfo.xml.":::|対象パッケージの PackageInfo.xml ファイルが正しく作成されていません。 パッケージ内の各ルート オブジェクトは、PackageInfo.xml ファイルで <PackageStructure> ノードを使って参照されている必要があります。 詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="Filename \[FileReference] is incorrect in <PackageStructure> element in PackageInfo.xml. Correct filename: PackageInfo.xml":::|PackageInfo.xml ファイル内で <PackageStructure> ノードを使って参照されたファイル名のスペルに誤りがあります。 エラーを修正して、もう一度パッケージを提出してください。 詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="For Printing and Scanning Devices, LaunchDeviceStageOnDeviceConnect needs to be set to False in WindowsInfo.xml.":::|詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="HardwareIDs in this submission: [list of Hardware ID(s)] are not owned by your company.":::|個々の SIG によると、リストされているハードウェア ID には、会社によって所有されていない VID が使われています。 これが正しくない場合は、ダッシュボード サポートにお問い合わせください。|
|:::no-loc text="Hardware IDs in this submission: \[list of Hardware ID(s)] do not match the expected list of Hardware IDs from SMBIOS.":::|提出したハードウェア ID は、SMBIOSFields.xml ファイルと共に提出した SMBIOS 情報から生成されていません。 次のいずれかの解決策を試してください。<br>\- ハードウェア ID をもう一度生成し、正しいハードウェア ID をパッケージに含める。<br/>\- 使用するフィールドを SMBIOSFields.xml ファイルに追加して、正しいハードウェア ID を生成する。<br/>詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="Hardware IDs in this submission: [list of Hardware ID(s)] fail the Inbox Driver Distribution Agreement (IDDA) list validation.":::|パッケージに追加したハードウェア ID は、Microsoft との Inbox Driver Distribution Agreement (IDDA) にリストされていません。 これらのハードウェア ID を削除し、もう一度提出してください。|
|:::no-loc text="Invalid scheme \[Scheme] in Allowed Domain for task \[TaskID] in Tasks.xml":::|URL は HTTP または HTTPs で始まる必要があります。 詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="Locale not found or is incorrect in PackageInfo.xml":::|PackageInfo.xml ファイルには、RFC 4646 に準拠した、正しい書式の locale タグが存在する必要があります。 ロケールを修正してから、もう一度パッケージを提出してください。|
|:::no-loc text="Missing resource reference for \[Id] in Resource.xml file in \DeviceStage\Task\[TaskID]\[Locale] folder":::|詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="Model IDs are not allowed for [Device Class] submissions.":::|このタイプのデバイス クラスでは、デバイス メタデータを提出するときに、モデル ID を使うことはできません。 必ずデバイスのハードウェア ID を使うようにしてください。 コンピューター デバイスのハードウェア ID を検索するには、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="Model Name not found in DeviceInfo.xml":::|DeviceInfo.xml ファイルが正しく作成されていません。 詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="No preview key can be found for this organization.":::|プレビュー パッケージをアップロードする前に PreviewKey を設定しておく必要があります。 詳しくは、「[デバイス メタデータのビジネス規則](https://docs.microsoft.com/windows-hardware/drivers/dashboard/device-metadata-business-rules)」をご覧ください。|
|:::no-loc text="PackageStructure node in PackageInfo.xml is invalid.":::|PackageInfo.xml ファイルが正しいことを確認してください。 詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="Task \[TaskGUID] is required for your device in Behavior.xml.":::|詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="Task \[TaskID] should not use taskGroupGuid \[TaskGroupGuid]":::|詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="TaskGroupGuid \[TaskGroupGuid] should not be used by your device for task \[TaskId]":::|デバイスには該当しない予約済みの GUID を使おうとしています。 次のいずれかの解決策を試してください。<br/>\- デバイスでサポートできないタスクの GUID を使わない。<br/>\- タスクを作成する場合は、そのタスク用の新しい GUID を生成する。<br/>詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="TaskGroupGuid incorrect for taskId \[TaskId] in Behavior.xml":::|タスクの GUID を修正してから、もう一度パッケージを提出してください。 詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="The \[FileName] icon file in \[FolderName] folder is missing image MissingImageSize.":::|画像サイズが存在することを確認してください。 存在しない場合は、画像サイズをアイコンに追加してから、もう一度パッケージを提出してください。<br/><br/>**注** 256x256 の画像レイヤーは、PNG 圧縮形式であることが必要です。 このサイズに BMP 形式は利用できません。 このサイズが BMP 形式で存在する場合は、同じサイズの画像を PNG 形式で作成し、アイコンに追加してから、もう一度パッケージを提出してください。 <br/><br/>詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="The cab Friendly Name is not unique to the Experience. Please choose another name.":::|エクスペリエンスに新しいフレンドリ名を付けて、もう一度提出してください。|
|:::no-loc text="The CommandLine argument should point to a valid URL beginning with HTTP or HTTPS for task \[TaskID] in Tasks.xml.":::|詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="The device category reported in your Device Metadata package and Logo Submission don't match. If the device category in the package is incorrect, please fix and upload again. If the device category in Logo Submission is incorrect, please fix in Submission Manager and try uploading your package again: [list of links per offending logo submission to SubmissionManager]":::|申請が受理されるためには、バインドされているロゴ提出とデバイス メタデータ間でデバイス カテゴリが一致している必要があります。 すべてのロゴ提出のデバイス カテゴリが一致していることと、そのデバイス カテゴリが、パッケージのデバイス カテゴリと一致していることを確認してください。 提示されているリンクは Submission Manager へのリンクです。カテゴリに誤りがある場合は、このリンクをたどってロゴ提出のデバイス カテゴリを変更することができます。 問題がすべて解決されたら、もう一度パッケージを提出します。|
|:::no-loc text="The Device Metadata Category for this submission does not exist.":::|有効ではないデバイス メタデータ カテゴリが使われました。 Windows ハードウェア認定キット (HCK) に記載されている定義済みのデバイス メタデータ カテゴリから選んでください。|
|:::no-loc text="The Experience name already exists for this organization.":::|名前の異なるエクスペリエンスを新たに作成してください。|
|:::no-loc text="The provided Logo submissions do not share Hardware IDs or Model IDs with the Device Metadata submission.":::|バインドされたロゴ提出は、エクスペリエンスのデバイス メタデータ パッケージ内のハードウェア ID を含んでいる必要があります。|
|:::no-loc text="The reference in PackageInfo.xml, DeviceInformation, was not found in the package.":::|DeviceInformation フォルダーの参照が PackageInfo.xml ファイルから欠落しています。 詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="The reference in PackageInfo.xml, DeviceStage, was not found in the package.":::|PackageInfo.xml ファイルの &lt;PackageStructure&gt; 要素内の参照が、正しく綴られていないか、パッケージのルートに置かれていません。 該当する参照を削除するか、正しいファイルまたはディレクトリを追加してください。 <p>詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="The reference in PackageInfo.xml, WindowsInformation, was not found in the package.":::|WindowsInformation フォルダーの参照が PackageInfo.xml ファイルから欠落しています。 詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="The submission contains [list of Hardware ID(s) and/or Model ID(s)] that are not covered via a logo submission.":::|ロゴ提出でカバーされないハードウェア ID またはモデル ID がパッケージに含まれています。 次のいずれかの解決策を試してください。<br/>\- デバイス メタデータ パッケージ内のハードウェア ID またはモデル ID を修正します。<br/>\- 新しいエクスペリエンスを作成し、関連するロゴ提出にのみバインドします。|
|:::no-loc text="The system manufacturer for this computer submission does not match the organization of the submitting user.":::|提出した SMBIOSFields.xml ファイルのシステム製造元が、Microsoft の記録にある製造元と一致しません。 次のいずれかの解決策を試してください。<br/>\- システム製造元の名前を修正し、もう一度パッケージを提出します。<br/>\- システム製造元フィールドが正しいにもかかわらず、ファイルが不合格となる場合は、ダッシュボード サポートまでメール (sysdev@microsoft.com) でお問い合わせください。|
|:::no-loc text="The TaskID \[TaskID] cannot be used with multiple TaskGroups.":::|Device Stage パッケージに、別のタスク グループで使われているタスク ID が存在します。 タスク ID は、タスク グループごとに一意で、なおかつタスクごとに一意である必要があります。 詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="This preview key has been rejected. Please choose another value.":::|ダッシュボードを使って設定した PreviewKey は受理されません。 新しい PreviewKey を提出してください。|
|:::no-loc text="Unexpected file found in \[FolderName] folder- \[ExtraFile]":::|パッケージの構造に問題があります。 詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="Unexpected file found in \[Path] folder – \[ExtraFile]":::|パッケージの構造に問題があります。 詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="Unexpected file found in the \[locale] subfolder of task \[TaskGroupGuid] folder – \[FileName]":::|指定されたファイルを削除してから、もう一度パッケージを提出してください。 詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="Unexpected folder found in \[FolderName] folder- \[ExtraFolder]":::|パッケージの構造に問題があります。 <br/><br/>**注** DeviceInfo.xml ファイル内のデバイス カテゴリが正しく設定されていないと、このエラーが発生する場合があります。 詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="Unexpected folder found in \[Path] folder – \[ExtraFolder]":::|パッケージの構造に問題があります。 詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="URL should not be a localhost for task \[TaskID] in Tasks.xml.":::|詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="URL specified in the commandLine is not valid for task \[TaskID] in Tasks.xml.":::|詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="Valid logo submission(s) are needed for \[SubmissionType] metadata for \[DeviceClass]":::|デジタル スチル カメラとポータブル メディア プレーヤーには、Windows 7 または Windows Vista® のロゴ提出が少なくとも 1 つ必要です。 携帯電話には、Windows 7 のロゴ提出が少なくとも 1 つ必要です。|
|:::no-loc text="You already have a preview submission for this Operating System Version. Remove the current Live submission.":::|昇格しようとしているロケールのプレビュー パッケージには、既にリリース パッケージが存在します。 このプレビュー パッケージを昇格する場合は、まずリリース パッケージを削除してから再試行してください。|
|:::no-loc text="You do not have access to this experience.":::|他社のエクスペリエンスにアクセスしようとしています。|
|:::no-loc text="Your device cannot have the command value set to HostedSiteWithDevice for task \[TaskID] in Tasks.xml.":::|詳しくは、[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658) に関するページをご覧ください。|
|:::no-loc text="Your submission is blocked due to a Dashboard error. Please email Dashboard Support at sysdev@microsoft.com for a resolution.":::|ダッシュボード サポートにお問い合わせください。|

## <a name="related-topics"></a>関連トピック

[デバイス メタデータ エクスペリエンスの作成](https://docs.microsoft.com/windows-hardware/drivers/dashboard/create-a-device-metadata-experience)

[デバイス メタデータ パッケージを申請する (ダッシュボード ヘルプ)](https://docs.microsoft.com/windows-hardware/drivers/dashboard/submit-a-device-metadata-package--dashboard-help-)

[デバイス メタデータのビジネス規則](https://docs.microsoft.com/windows-hardware/drivers/dashboard/device-metadata-business-rules)
