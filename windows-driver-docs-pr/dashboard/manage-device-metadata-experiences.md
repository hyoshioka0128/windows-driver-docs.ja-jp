---
title: デバイス メタデータ エクスペリエンスの管理
description: デバイス メタデータ エクスペリエンスの管理
ms.assetid: aede9597-4b67-4c1a-8ae4-924d39c88b53
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c6e9dab46eef01a358b95133672e6cb10008eeb
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "63334955"
---
# <a name="manage-device-metadata-experiences"></a>デバイス メタデータ エクスペリエンスの管理

デバイス メタデータ エクスペリエンスを作成して提出した後は、ダッシュボードで確認または編集できます。

## <a name="managing-your-device-metadata-experiences"></a>デバイス メタデータ エクスペリエンスの管理

**[Manage experiences]** (エクスペリエンスの管理) ページでは、選択されたエクスペリエンス内のデバイス メタデータ パッケージの追加、削除、または昇格 (プレビューからリリースへ) を行うことができます。 同じハードウェア ID またはモデル ID のパッケージを、ロケールが異なっていれば、同じエクスペリエンスに追加することもできます。

## <a name="to-filter-your-device-metadata-experiences"></a>デバイス メタデータ エクスペリエンスをフィルター処理するには

1. ハードウェア デベロッパー センターまたは Windows デベロッパー センターから Microsoft アカウントで**ダッシュボード**にサインインします。

2. ウィンドウの左側で **[Device metadata]** (デバイス メタデータ) をクリックし、 **[Manage experiences]** (エクスペリエンスの管理) をクリックします。

3. 自分または自分の会社が作成したすべてのエクスペリエンスが表示されます。 一覧を並べ替えるには、列見出しをクリックします。

4. 一覧の上部にあるフィルターを使うと、目的のエクスペリエンスだけを表示できます。 次の 1 つ以上のパラメーターを入力します。

|パラメーター|説明|
|---|---|
|Experience name (エクスペリエンス名)|一覧から、確認または更新するエクスペリエンスの名前を選びます。|
|Hardware ID(s) (ハードウェア ID)|確認するハードウェア ID を入力します。複数の ID を指定する場合は、各エントリの後にセミコロンを挿入します。 選択されたハードウェア ID を含むエクスペリエンスが表示されます。
|Device category (デバイス カテゴリ)|一覧から、確認するデバイス カテゴリを選びます。|
|Model ID(s) (モデル ID)|確認するモデル ID を入力します。複数の ID を指定する場合は、各エントリの後にセミコロンを挿入します。 選択されたモデル ID を含むエクスペリエンスが表示されます。|

## <a name="to-open-and-view-your-device-metadata-experience"></a>デバイス メタデータ エクスペリエンスを開いて表示するには

1. 詳細を表示するエクスペリエンスをクリックします。

2. **[Experience information]** (エクスペリエンス情報) の下で、以下のような情報を確認します。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>要素</th>
    <th>説明</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Experience type (エクスペリエンスの種類)</p></td>
    <td><p>次のもののメタデータを含む、エクスペリエンス内のパッケージの種類。</p>
    <ul>
    <li><p>デバイスとプリンター</p></li>
    <li><p>Device Stage</p></li>
    </ul></td>
    </tr>
    <tr class="even">
    <td><p>Device category (デバイス カテゴリ)</p></td>
    <td><p>エクスペリエンス内のパッケージのデバイス カテゴリ。</p></td>
    </tr>
    <tr class="odd">
    <td><p>Model ID(s) (モデル ID)</p></td>
    <td><p>エクスペリエンス内のパッケージで定義されているモデル ID。</p></td>
    </tr>
    <tr class="even">
    <td><p>Hardware ID(s) (ハードウェア ID)</p></td>
    <td><p>エクスペリエンス内のパッケージで定義されているハードウェア ID。</p></td>
    </tr>
    <tr class="odd">
    <td><p>Logo submission ID(s) (ロゴの提出 ID)</p></td>
    <td><p>エクスペリエンスにバインドされている提出 ID。</p></td>
    </tr>
    </tbody>
    </table>

3. **[Metadata packages]** (メタデータ パッケージ) で個々のパッケージを展開し、詳細を表示します。 ライブ パッケージや公開の準備ができたパッケージをダウンロードすることもできます。

    >[!NOTE]
    >メタデータ パッケージにエラーがある場合は、ここに表示されます。

4. この一覧は、次のいずれかの列見出しをクリックして並べ替えることができます。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>列見出し</th>
    <th>説明</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>名前</p></td>
    <td><p>エクスペリエンス内のパッケージは、フレンドリ名があればその名前、またはファイル名に基づいて一覧表示されます。</p></td>
    </tr>
    <tr class="even">
    <td><p>Submission date (提出日)</p></td>
    <td><p>個別の各パッケージを提出した日付が表示されます。</p></td>
    </tr>
    <tr class="odd">
    <td><p>Preview</p></td>
    <td><p>パッケージがプレビュー状態で、リリースされていない場合、このチェック ボックスはオンになっています。</p></td>
    </tr>
    <tr class="even">
    <td><p>ロケール</p></td>
    <td><p>ここには、パッケージが対象としている国または地域が一覧表示されます。</p></td>
    </tr>
    <tr class="odd">
    <td><p>Default</p></td>
    <td><p><strong>[Yes]</strong> (はい) の場合は、既定のパッケージとして指定されたパッケージであることを示しています。</p></td>
    </tr>
    <tr class="even">
    <td><p>状況</p></td>
    <td><p>この値は、選択されたパッケージの現在の状態を示しており、次のいずれかです。</p>
    <ul>
    <li><p>保留中:パッケージはアップロードされ、現在は検証中です。</p></li>
    <li><p>[To Be Published] (公開準備済み):パッケージは検証され、メタデータ サーバーに送信されるのを待機しています。 パッケージの検証済みコピーをダウンロードできます。パッケージは 24 時間以内にライブになり、ユーザーが利用できるようになります。</p></li>
    <li><p>[Live] (ライブ):パッケージは、ユーザーがダウンロードできる状態になっています。</p></li>
    <li><p>エラー:検証中に 1 つ以上のエラーが見つかりました。 詳しい情報については、セクションを展開してください。</p></li>
    </ul></td>
    </tr>
    </tbody>
    </table>

## <a name="to-modify-your-device-metadata-experience"></a>デバイス メタデータ エクスペリエンスを変更するには

1. プレビュー パッケージをリリースするには、パッケージを選んで、 **[Release]** (リリース) をクリックします。

    >[!NOTE]
    >リリースされたファイルをユーザーがダウンロードできるようになるまでに、最大で 48 時間かかる場合があります。

2. エクスペリエンスからパッケージを削除するには、パッケージを選んで、 **[Delete]** (削除) をクリックします。

   >[!NOTE]
   >削除できるのは、 **[Live]** (ライブ) または **[Error]** (エラー) 状態のパッケージだけです。

3. 既存のパッケージを更新するには、パッケージを選んで **[Delete]** (削除) をクリックしてから、新しいパッケージを作成し、アップロードします。

    新しいパッケージの作成について詳しくは、[Windows Driver Kit (WDK) ](https://docs.microsoft.com/windows-hardware/drivers/devtest/device-metadata-authoring-wizard-portal) の「[Device Metadata Authoring (デバイス メタデータの作成) ウィザード](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)」をご覧ください。

4. 新しいパッケージを追加するには、 **[Add more metadata]** (メタデータの追加) で追加するファイルを参照し、必要に応じてフレンドリ名を作成して、 **[Submit]** (送信) をクリックします。

    >[!NOTE]
    >エクスペリエンスには、合計で 50 のパッケージを追加できます。

## <a name="related-topics"></a>関連トピック

- [デバイス メタデータ エクスペリエンスの作成](create-a-device-metadata-experience.md)

- [バルク メタデータ パッケージの提出](submit-a-bulk-metadata-package.md)

- [プレビュー パッケージの作成](creating-a-preview-package.md)

- [デバイス メタデータ エクスペリエンスを申請する際のエラーと解決方法](errors-and-solutions-when-submitting-device-metadata-experiences.md)

- [デバイス メタデータのビジネス規則](device-metadata-business-rules.md)
