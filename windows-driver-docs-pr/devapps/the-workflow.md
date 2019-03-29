---
title: UWP デバイス アプリを構築する
description: デバイス製造元は、デバイスのコンパニオンとして機能する UWP デバイス アプリを作成できます。
ms.assetid: DB88876E-3C92-40E9-A2E2-19493F3357B5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 213869001380bd45adae241e6f26d31ef7266e28
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349737"
---
# <a name="building-uwp-device-apps"></a>UWP デバイス アプリを構築する


デバイス製造元は、デバイスのコンパニオンとして機能する UWP デバイス アプリを作成できます。 このトピックでは、UWP デバイスのアプリ、1 つは、構築するための基本的な手順を送信する必要あります、Microsoft Store のダッシュ ボードと、Windows デベロッパー センター ハードウェア ダッシュ ボードには、アプリとデバイスのメタデータそれぞれ順のコンポーネントについて説明します。 各手順の詳細については、次を参照してください。[ステップ バイ ステップの UWP デバイスのアプリをビルド](build-a-uwp-device-app-step-by-step.md)します。

## <a name="span-idthebuildingblocksspanspan-idthebuildingblocksspanspan-idthebuildingblocksspanthe-building-blocks"></a><span id="The_building_blocks"></span><span id="the_building_blocks"></span><span id="THE_BUILDING_BLOCKS"></span>構成要素


最も基本的なレベルで、 *UWP デバイス アプリ*デバイス メタデータを使用して、特定のデバイスに関連付けられている UWP アプリです。 UWP デバイスのアプリに 4 つのコンポーネントがあります。 デバイス、アプリ、デバイス メタデータ パッケージ、およびデバイス ドライバー。 デバイス Api (USB、HID、Bluetooth GATT、および Bluetooth RFCOMM) プロトコルを使用して周辺機器のデバイスにアクセスするデバイスのメタデータを使用する必要はありません。 などの特殊な機能を有効にするデバイスのメタデータを使用する必要は[自動インストール](auto-install-for-uwp-device-apps.md)、[自動再生](autoplay-for-uwp-device-apps.md)、および[デバイスの更新](device-sync-and-update-for-uwp-device-apps.md)します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><strong>デバイス</strong></td>
<td align="left">これは、物理デバイスです。 <em>周辺機器</em>は外部 PC エンクロージャにします。 <em>社内デバイス</em>デバイス内に存在または PC のエンクロージャは統合です。</td>
</tr>
<tr class="even">
<td align="left"><strong>アプリ</strong></td>
<td align="left">UWP デバイスのアプリとは、デバイスの一意の機能にアクセスするユーザーを有効にすると、デバイスのカスタマイズされたユーザー エクスペリエンスを提供する UWP アプリです。 デバイス アプリには、という名前のファイルが含まれています<strong>StoreManifest.xml</strong>エクスペリエンスの id を指定する。 <em>ID エクスペリエンス</em>デバイス メタデータ パッケージを一意に識別する GUID です。</td>
</tr>
<tr class="odd">
<td align="left"><strong>デバイス メタデータ</strong></td>
<td align="left">これは、Windows 7 を既に作成した可能性がありますデバイス メタデータ パッケージの拡張バージョンです。 Windows 8.1 のでは、デバイスのメタデータは、デバイスとアプリ間のリンクを作成します。 そのリンクがエクスペリエンス ID で識別されます。 デバイス メタデータ パッケージを指定します (ローカライズ可能なモデル名、説明、およびリアルなアイコンなど)、PC 用の UI コンテンツだけでなく<a href="autoplay-for-uwp-device-apps.md" data-raw-source="[AutoPlay](autoplay-for-uwp-device-apps.md)">自動再生</a>構成し、どのアプリがデバイスにアクセスする権限。 Windows では、Windows メタデータ Internet Service (WMIS) からデバイスのメタデータが自動的にダウンロードします。</td>
</tr>
<tr class="even">
<td align="left"><strong>ドライバー</strong></td>
<td align="left">すべての UWP デバイス アプリは、デバイスにアクセスするドライバーを直接に使用します。 たとえば、Windows ランタイムのデバイス プロトコル Api、Windows 8.1 で導入されたは使用インボックス ドライバーを使用、アプリが USB、HID、および Bluetooth 経由で通信できるようにします。 これらの Api で使用されるドライバーに関する詳細については、次を参照してください。<a href="step-1--create-a-uwp-device-app.md" data-raw-source="[Step 1: Create a UWP device app](step-1--create-a-uwp-device-app.md)">手順 1。UWP デバイスのアプリ作成</a>です。
<div class="alert">
<strong>重要な</strong>カスタム ドライバーを使用してデバイスのアクセスには、Microsoft からの承認が必要です。 詳細については、次を参照してください。 <a href="https://go.microsoft.com/fwlink/p/?LinkId=306693" data-raw-source="[UWP device app Design Guide for Specialized Devices Internal to the PC](https://go.microsoft.com/fwlink/p/?LinkId=306693)">UWP デバイス アプリ、PC にデバイスの内部の特殊化の設計ガイド</a>します。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

## <a name="span-iddevelopmentworkflowspanspan-iddevelopmentworkflowspanspan-iddevelopmentworkflowspandevelopment-workflow"></a><span id="Development_workflow"></span><span id="development_workflow"></span><span id="DEVELOPMENT_WORKFLOW"></span>開発ワークフロー


既にデバイスを作成して、ハードウェア ダッシュ ボードに必要なドライバーを送信したと仮定すると、UWP デバイス アプリを作成する手順は 6 つがあります。 各手順の詳細については、リンクをクリックします。

![デバイス アプリの開発ワークフロー](images/device-app-workflow.png)

[ステップ 1: アプリを作成する](step-1--create-a-uwp-device-app.md)します。 Microsoft Store アプリを関連付ける、アプリを開発してテストします。

[手順 2:デバイス メタデータを作成する](step-2--create-device-metadata.md)します。 デバイス メタデータの作成ウィザードを使用してアプリをデバイスに関連付ける、デバイス メタデータ パッケージを作成し、(元のエクスペリエンスの ID を指定) StoreManifest.xml ファイルを作成します。

[手順 3:エクスペリエンス ID をアプリに追加](step-3--add-an-experience-id-to-the-app.md)します。 StoreManifest.xml ファイルをアプリに組み込みます。

**注**  アプリ特権のあるアプリは、自動インストールが構成されていない場合は、手順 3. は必要ありません。

 

[手順 4:デバイス メタデータを (ローカル) をテストする](step-4--test-device-metadata.md)します。 デバイス メタデータの作成ウィザードを使用して、検証し、デバイス メタデータをローカル開発用ワークステーションに展開します。

[手順 5:Microsoft Store のダッシュ ボードにアプリを送信](step-5--submit-the-app.md)します。 販売の詳細を確認し、アプリがある UWP デバイスのアプリのテスト担当者にことを示すダッシュ ボードを使用します。

**注**  アプリ特権のあるアプリは、自動インストールが構成されていない場合は、手順 6 の後に Microsoft Store のダッシュ ボードにアプリを送信することができます。 詳細については、次を参照してください。[アプリ送信のシーケンスを特権](#priv-sequence)します。

 

[手順 6:Windows デベロッパー センター ハードウェア ダッシュ ボードに、デバイス メタデータの提出](step-6--submit-device-metadata.md)します。 デバイス メタデータ パッケージを手動で送信するか、ハードウェア ダッシュ ボードに送信できる一括送信パッケージを作成するデバイス メタデータの作成ウィザードを使用します。

## <a name="span-idstandardsubmissionsequencespanspan-idstandardsubmissionsequencespanspan-idstandardsubmissionsequencespanstandard-submission-sequence"></a><span id="Standard_submission_sequence"></span><span id="standard_submission_sequence"></span><span id="STANDARD_SUBMISSION_SEQUENCE"></span>標準的な送信シーケンス


最初に送信する、さまざまなダッシュ ボードへのアプリとデバイスのメタデータを特定の順序でイベントが発生する必要があります。 次の表では、該当する場合、デバイス ドライバーを送信するときにも示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Sequence</th>
<th align="left">説明</th>
<th align="left">続行する前にしています.</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">1</td>
<td align="left"><strong>デバイス ドライバーを提出</strong>ハードウェア ダッシュ ボードにします。</td>
<td align="left">ドライバーが Windows Update から入手可能になるまで待ちます。</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left"><strong>アプリの提出</strong>Microsoft Store のダッシュ ボードにします。</td>
<td align="left">同意と Microsoft Store でアプリがライブになるまで待機します。</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left"><strong>デバイス メタデータの提出</strong>ハードウェア ダッシュ ボードにします。 アプリは、メタデータは、ハードウェア ダッシュ ボードの検証を渡すことができます前に Microsoft Store にする必要があります。</td>
<td align="left">同意と配布の 10 日間待機します。</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left"><strong>終了日:</strong>ユーザーは、Microsoft Store のデバイスのアプリのすべての機能を利用できます。 デバイス アプリの機能などのことに注意してください。<a href="auto-install-for-uwp-device-apps.md" data-raw-source="[automatic installation](auto-install-for-uwp-device-apps.md)">自動インストール</a>、<a href="autoplay-for-uwp-device-apps.md" data-raw-source="[AutoPlay](autoplay-for-uwp-device-apps.md)">自動再生</a>、および<a href="device-sync-and-update-for-uwp-device-apps.md" data-raw-source="[device update](device-sync-and-update-for-uwp-device-apps.md)">デバイスの更新</a>まで、ユーザーが PC にデバイスのメタデータと、アプリが動作しません。 アプリは、microsoft が指定されていないドライバーを必要とする場合は、そのドライバーをアプリが動作するために必要があります。</td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

## <a name="span-idpriv-sequencespanspan-idpriv-sequencespanprivileged-app-submission-sequence"></a><span id="priv-sequence"></span><span id="PRIV-SEQUENCE"></span>特権のあるアプリ送信シーケンス


場合によっては、UWP デバイス アプリはライブである Microsoft Store デバイス メタデータを送信する前にする必要はありません。 ときに、UWP デバイス アプリ。

-   特権のあるアプリとして指定されます。
-   自動インストールが構成されていません

アプリに関する true の場合は、Microsoft Store のダッシュ ボードに UWP デバイス アプリを送信する前にハードウェア ダッシュ ボードに、デバイス メタデータを送信できます。 このような場合はエクスペリエンス ID をアプリに追加する必要はありません。デバイスのメタデータでの特権を持つアプリとしてアプリを指定することは、特権を有効にするのに十分です。

**注**  プリンターやカメラ用の UWP デバイス アプリを自動的にインストールします。 したがって、この種の UWP デバイス アプリでは、標準の送信順序に従う必要があり、デバイス メタデータを送信する前に、Microsoft Store に送信します。

 

## <a name="span-idwindowsstoredeviceapplimitsspanspan-idwindowsstoredeviceapplimitsspanspan-idwindowsstoredeviceapplimitsspanuwp-device-app-limits"></a><span id="Windows_Store_device_app_limits"></span><span id="windows_store_device_app_limits"></span><span id="WINDOWS_STORE_DEVICE_APP_LIMITS"></span>UWP デバイス アプリの制限


デバイスの製造元が、自動インストールとアプリの特権のためにデバイス メタデータで指定できる UWP アプリの数には制限があります。 たとえば、周辺機器製造元 (IHV) は、自動インストールが構成されたアプリと、特権アプリとして指定されたアプリを、それぞれ最大 1 つずつ提出できます。 IHV は、両方の制限を満たす 1 つのアプリか、それぞれいずれかの制限を満たす 2 つのアプリを提出できます。

**重要な**  デバイスの製造元は、Microsoft Store に送信できる UWP デバイス アプリの合計数に制限はありません。 これらの制限が 1 つのデバイス メタデータ パッケージにのみ適用されます。

 

移動体通信事業者と OEM では、デバイス メタデータに指定できるアプリの数の制限が異なります。 詳しくは、OEM が Microsoft OEM の担当者にお問い合わせください。

各デバイス メタデータ パッケージでは、次の制限が適用されます。

| Developer       | 自動インストール アプリの制限 | 特権アプリの制限 |
|-----------------|----------------------------------|----------------------|
| IHV             | 1                                | 1                    |
| 移動体通信事業者 | 1                                | 8                    |
| OEM             | Microsoft に問い合わせる                | Microsoft に問い合わせる    |

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[UWP デバイス アプリのビルド手順](build-a-uwp-device-app-step-by-step.md)

[UWP デバイス アプリの自動インストール](auto-install-for-uwp-device-apps.md)

[UWP デバイス アプリの自動再生](autoplay-for-uwp-device-apps.md)

[UWP デバイス アプリによるデバイスの同期と更新](device-sync-and-update-for-uwp-device-apps.md)

[内部デバイス用の UWP デバイス アプリ](uwp-device-apps-for-specialized-devices.md)

 

 






