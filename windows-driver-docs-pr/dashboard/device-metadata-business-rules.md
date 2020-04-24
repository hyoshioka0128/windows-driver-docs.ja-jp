---
title: デバイス メタデータのビジネス規則
description: デバイス メタデータのビジネス規則
ms.assetid: 19a0ced7-bb31-4899-abb4-2de803f179a6
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da04406434d834d2daf2a7528ec1557152e50703
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "67364473"
---
# <a name="device-metadata-business-rules"></a>デバイス メタデータのビジネス規則


ダッシュボードを使ってデバイス メタデータ パッケージを提出する際は、次の点に配慮してください。

-   適切なデバイスのパッケージをダウンロードできるようにする。

-   関連するハードウェア ID とモデル ID で適切なパッケージをはっきりと識別できるようにし、矛盾が生じないようにする。

-   プレビュー パッケージがリリース パッケージとしてダウンロードされないようにする。

## <a name="span-idin_this_topicspanspan-idin_this_topicspanspan-idin_this_topicspanin-this-topic"></a><span id="In_this_topic"></span><span id="in_this_topic"></span><span id="IN_THIS_TOPIC"></span>このトピックの内容


[デバイス メタデータ提出の一般規則](#devicemetadatabusrules-submission)

[デバイス メタデータの種類](#device-metadata-types)

[エクスペリエンスの規則](#experience-rules)

[固有の Device Stage メタデータの申請](#bkmk-unique)

### <a name="span-iddevicemetadatabusrules-submissionspanspan-iddevicemetadatabusrules-submissionspanspan-iddevicemetadatabusrules-submissionspangeneral-rules-for-submitting-device-metadata"></a><span id="DeviceMetadataBusRules-submission"></span><span id="devicemetadatabusrules-submission"></span><span id="DEVICEMETADATABUSRULES-SUBMISSION"></span>デバイス メタデータ申請の一般規則

ダッシュボードを介してパッケージを提出するときは、次の一般規則が適用されます。

すべてのパッケージは、悪意のあるソフトウェアが含まれていないようにする必要があります。

各デバイス メタデータ パッケージは、自分の会社の Microsoft Authenticode 証明書で署名する必要があります。

会社で作成した各エクスペリエンスの名前は、その会社内で一意であることが必要です。

パッケージのフレンドリ名が、そのパッケージを含んでいるエクスペリエンス内で重複しないようにする必要があります。

パッケージの元のファイル名に重複がないようにする必要があります。

すべてのパッケージ内のすべてのハードウェアに、一意の ID が割り当てられている必要があります。 たとえ自社または他社が作成した別のエクスペリエンスであっても、同じハードウェア ID を使うことはできません。

すべてのパッケージ内のすべてのモデルに、一意の ID が割り当てられている必要があります。 たとえ自社または他社が作成した別のエクスペリエンスであっても、同じモデル ID を使うことはできません。

デバイス メタデータの提出には、対象デバイスの有効なロゴ提出のリンクを含める必要があります。 有効なロゴ提出にはそれぞれ、デバイス メタデータの提出にリストされているプライマリ デバイス カテゴリが含まれている必要があります。

既にあるエクスペリエンスのパッケージを更新するときは、まず、そのパッケージを削除してから新しいパッケージを作成し、新しいパッケージを既存のエクスペリエンスにアップロードしてください。

1 つのパッケージに含めることのできる ID は 1,000 個までです。 これにはハードウェア ID とモデル ID が含まれます。

### <a name="span-iddevice-metadata-typesspanspan-iddevice-metadata-typesspanspan-iddevice-metadata-typesspandevice-metadata-types"></a><span id="Device-metadata-types"></span><span id="device-metadata-types"></span><span id="DEVICE-METADATA-TYPES"></span>デバイス メタデータの種類

デバイス メタデータ パッケージは、その種類に応じた規則に従う必要があります。 また、Device Stage メタデータ内の各デバイス カテゴリにも、それぞれ固有の規則が存在します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>メタデータの種類</th>
<th>適用対象</th>
<th>要件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>[デバイスとプリンター] フォルダー</p></td>
<td><ul>
<li><p>すべてのデバイス</p></li>
<li><p>UWP デバイス アプリを持つデバイス</p></li>
<li><p>特権アプリを持つデバイス</p></li>
</ul></td>
<td><p>関連する Windows® ロゴ提出を持たないインボックス ドライバー、またはデバイス エクスペリエンスに関連付けられている Windows ロゴ提出を持つカスタム ドライバーがデバイスに使われていること。</p></td>
</tr>
<tr class="even">
<td><p>Device Stage</p></td>
<td><ul>
<li><p>デジタル スチル カメラ</p>
<ul>
<li><p>Imaging.Camera</p></li>
</ul></li>
<li><p>ポータブル メディア プレーヤー</p>
<p>Multimedia.PMP</p></li>
<li><p>携帯電話</p>
<ul>
<li><p>Communication.Phone.Cell</p></li>
</ul></li>
<li><p>プリンター、FAX 機器、スキャナー</p>
<ul>
<li><p>PrintFax</p></li>
<li><p>PrintFax.Fax</p></li>
<li><p>PrintFax.MFP</p></li>
<li><p>PrintFax.Printer</p></li>
<li><p>PrintFax.Printer.Inkjet</p></li>
<li><p>PrintFax.Printer.Laser</p></li>
<li><p>PrintFax.Printer.3D</p></li>
<li><p>Imaging.Scanner</p></li>
</ul></li>
<li><p>コンピューター</p>
<ul>
<li><p>Computer.AllInOne</p></li>
<li><p>Computer.Desktop</p></li>
<li><p>Computer.Desktop.LowProfile</p></li>
<li><p>Computer.Desktop.Pizzabox</p></li>
<li><p>Computer.Laptop</p></li>
<li><p>Computer.Lunchbox</p></li>
<li><p>Computer.Netbook</p></li>
<li><p>Computer.Notebook</p></li>
<li><p>Computer.Notebook.Sub</p></li>
<li><p>Computer.Portable</p></li>
<li><p>Computer.Rackmount</p></li>
<li><p>Computer.Sealed</p></li>
<li><p>Computer.Server</p></li>
<li><p>Computer.SpaceSaving</p></li>
<li><p>Computer.Tablet</p></li>
<li><p>Computer.ThinClient</p></li>
<li><p>Computer.Tower</p></li>
<li><p>Computer.Tower.Mini</p></li>
</ul></li>
<li><p>キーボードとマウス</p>
<ul>
<li><p>Input.Keyboard</p></li>
<li><p>Input.Mouse</p></li>
<li><p>Input.Trackball</p></li>
</ul></li>
<li><p>スマートカード</p>
<ul>
<li><p>PersonalIdentity.Smartcard</p></li>
<li><p>Media.Smartcard</p></li>
</ul></li>
<li><p>モバイル ブロードバンド デバイス</p>
<ul>
<li><p>Network.MobileBroadband</p></li>
</ul></li>
<li><p>Web カメラ</p>
<ul>
<li><p>Imaging.Webcam</p></li>
</ul></li>
<li><p>ポータブル全般</p>
<ul>
<li><p>Other.Portable</p></li>
</ul></li>
</ul></td>
<td><p>デバイスごとに Windows ロゴ提出が必要です。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idexperience-rulesspanspan-idexperience-rulesspanspan-idexperience-rulesspanexperience-rules"></a><span id="Experience-rules"></span><span id="experience-rules"></span><span id="EXPERIENCE-RULES"></span>エクスペリエンスの規則

-   単一のエクスペリエンスに含まれるすべてのデバイス メタデータ パッケージは、同じハードウェア ID とモデル ID をサポートする必要があります。

-   エクスペリエンス内のパッケージで、特定のロケール、プレビュー ステータス、Windows オペレーティング システムを組み合わせる際は、エクスペリエンス内のパッケージごとに、その組み合わせが一意であることが必要です。 たとえば、エクスペリエンスには、ロケール A に関して、Windows オペレーティング システムごとに 1 つのリリース パッケージとプレビュー パッケージを含めることができます。 その同じエクスペリエンスに、ロケール A でなおかつ同じ Windows オペレーティング システムを対象とした他のリリース パッケージやプレビュー パッケージを含めることはできません。

-   エクスペリエンスに含めることのできる既定のプレビュー ロケール パッケージと既定のリリース パッケージは、Windows オペレーティング システム バージョンごとに、それぞれ 1 つだけです。

### <a name="span-idbkmk-uniquespanunique-device-stage-metadata-submissions"></a><span id="bkmk-unique"></span>固有の Device Stage メタデータの申請

PC メタデータ パッケージを提出する方法については、「[PC デバイス マニフェスト パッケージの提出](https://docs.microsoft.com/windows-hardware/drivers/dashboard/)」をご覧ください。

モバイル ブロードバンド メタデータ パッケージを提出する方法については、「[モバイル ブロードバンド デバイス マニフェスト パッケージの提出](https://docs.microsoft.com/windows-hardware/drivers/dashboard/)」をご覧ください。

複数ロケールのメタデータ パッケージを提出する方法については、「[複数ロケールのデバイス マニフェスト パッケージの提出](https://docs.microsoft.com/windows-hardware/drivers/dashboard/)」をご覧ください。

### <a name="span-idwindows_store_device_app_limitsspanspan-idwindows_store_device_app_limitsspanspan-idwindows_store_device_app_limitsspanuwp-device-app-limits"></a><span id="Windows_Store_device_app_limits"></span><span id="windows_store_device_app_limits"></span><span id="WINDOWS_STORE_DEVICE_APP_LIMITS"></span>UWP デバイス アプリの制限

デバイスの製造元が、自動インストールとアプリの特権のためにデバイス メタデータで指定できる UWP アプリの数には制限があります。 たとえば、周辺機器製造元 (IHV) は、自動インストールが構成されたアプリと、特権アプリとして指定されたアプリを、それぞれ最大 1 つずつ提出できます。 IHV は、両方の制限を満たす 1 つのアプリか、それぞれいずれかの制限を満たす 2 つのアプリを提出できます。

**重要**  デバイスの製造元が Microsoft Store に申請できる UWP デバイス アプリの合計数に制限はありません。これらの制限は、単一のデバイス メタデータ パッケージに対してのみ適用されます。

 

移動体通信事業者と OEM では、デバイス メタデータに指定できるアプリの数の制限が異なります。 詳しくは、OEM が Microsoft OEM の担当者にお問い合わせください。

各デバイス メタデータ パッケージでは、次の制限が適用されます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>Developer</th>
<th>自動インストール アプリの制限</th>
<th>特権アプリの制限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IHV</p></td>
<td><p>1</p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p>移動体通信事業者</p></td>
<td><p>1</p></td>
<td><p>8</p></td>
</tr>
<tr class="odd">
<td><p>OEM</p></td>
<td><p>Microsoft に問い合わせる</p></td>
<td><p>Microsoft に問い合わせる</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


- [デバイス メタデータ エクスペリエンスの作成](https://docs.microsoft.com/windows-hardware/drivers/dashboard/)

- [デバイス メタデータ エクスペリエンスを管理する](https://docs.microsoft.com/windows-hardware/drivers/dashboard/)

- [デバイス メタデータ パッケージを申請する (ダッシュボード ヘルプ)](https://docs.microsoft.com/windows-hardware/drivers/dashboard/)

 

 






