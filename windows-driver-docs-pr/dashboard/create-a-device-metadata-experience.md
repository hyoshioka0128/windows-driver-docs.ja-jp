---
title: デバイス メタデータ エクスペリエンスの作成
description: デバイス メタデータ エクスペリエンスの作成
ms.assetid: 964ad06e-0f29-441d-b184-61f80a614914
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eaa44cd33141f2c57e83d430d87a73435d61a3ac
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518777"
---
# <a name="create-a-device-metadata-experience"></a>デバイス メタデータ エクスペリエンスの作成


デバイスを認識しやすくする画像と、その他の機能を提供するデバイス メタデータ ファイル (.devicemetadata-ms または .devicemanifest-ms) を作成したら、それらをエクスペリエンスとして提出する必要があります。

devicemanifest-ms ファイルは .cab ファイルであり、devicemetadata-ms ファイルと、複数ロケール パッケージ、コンピューター パッケージ、モバイル ブロードバンド アカウント エクスペリエンス パッケージの追加情報が含まれます。 すべての devicemanifest-ms パッケージに、追加情報として LocaleInfo.xml ファイルを含める必要があります。 詳しくは、PcMetadataSubmission.xml と MobileBroadbandMetadataSubmission.xml の作成に関するページをご覧ください。

## <a name="span-idcreatingadevicemetadataexperiencepackagespanspan-idcreatingadevicemetadataexperiencepackagespanspan-idcreatingadevicemetadataexperiencepackagespancreating-a-device-metadata-experience-package"></a><span id="Creating_a_device_metadata_experience_package"></span><span id="creating_a_device_metadata_experience_package"></span><span id="CREATING_A_DEVICE_METADATA_EXPERIENCE_PACKAGE"></span>デバイス メタデータ エクスペリエンス パッケージの作成


ロゴ認定のためにファイルを提出する前に、ファイルをエクスペリエンスにパッケージ化する必要があります。 このエクスペリエンスを利用することで、ハードウェア ID とモデル ID のセットが同一でロケールだけが違うデバイスのデバイス メタデータ パッケージをグループ化することもできます。

**デバイス メタデータ エクスペリエンス パッケージを作成するには**

1. このサービスに関連付けられている Microsoft アカウントを使用して、パートナー センターからダッシュボードにサインインします。

2. ウィンドウの左側で **[Device metadata]** (デバイス メタデータ) をクリックし、**[Create experience]** (エクスペリエンスの作成) をクリックします。

3. **[Create experience]** (エクスペリエンスの作成) ページで、次の情報を入力します。

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
   <td><p>Experience name (エクスペリエンス名)</p></td>
   <td><p>自社の他のエクスペリエンス名と重複しない名前を作成します。</p></td>
   </tr>
   <tr class="even">
   <td><p>Package friendly name (パッケージ フレンドリ名)</p></td>
   <td><p>必要に応じて、使いやすく覚えやすい名前を作成します。</p></td>
   </tr>
   <tr class="odd">
   <td><p>ファイル</p></td>
   <td><p>エクスペリエンスに含める最大で 50 のファイルを指定してアップロードします。</p></td>
   </tr>
   <tr class="even">
   <td><p>Preview package (プレビュー パッケージ)</p></td>
   <td><p>選択したすべてのパッケージをプレビュー パッケージとして提出する場合に選びます。 詳しくは、「<a href="https://msdn.microsoft.com/library/windows/hardware/br230780.aspx" data-raw-source="[Creating a Preview Package](https://msdn.microsoft.com/library/windows/hardware/br230780.aspx)">プレビュー パッケージの作成</a>」をご覧ください。</p></td>
   </tr>
   <tr class="odd">
   <td><p>Bind to logo submissions (ロゴの提出にバインドする)</p></td>
   <td><p>インボックス ドライバーだけを使い、ロゴ認定を持たないデバイスを提出する場合は、1 つ目のオプションを選びます。 デバイスに関連付けられているロゴ提出がある場合、デバイスが PC、プリンター、FAX、スキャナーである場合、またはメタデータがモバイル ブロードバンド アカウント識別子のコレクション用である場合は、2 番目のオプションを選びます。</p></td>
   </tr>
   <tr class="even">
   <td><p>Bind to logo submissions: select submissions (ロゴの提出にバインドする: 提出を選択)</p></td>
   <td><p>2 番目のオプションを選び、コンピューター、モバイル ブロードバンド アカウント エクスペリエンス、IDDA リストにあるプリンターまたは FAX のいずれかのメタデータを提出する場合は、ロゴ提出をバインドする必要はありません。</p>
   <p>2 番目のオプションを選び、その他の種類のデバイスのメタデータを提出する場合は、デバイスに適用するロゴ提出を選んでバインドする必要があります。</p></td>
   </tr>
   </tbody>
   </table>

     

4. **[送信]** をクリックします。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[デバイス メタデータ エクスペリエンスを管理する](https://msdn.microsoft.com/library/windows/hardware/br230797.aspx)

[バルク メタデータ パッケージの提出](https://msdn.microsoft.com/library/windows/hardware/hh801895.aspx)

[デバイス メタデータ エクスペリエンスを申請する際のエラーと解決方法](https://msdn.microsoft.com/library/windows/hardware/br230786.aspx)

[デバイス メタデータのビジネス規則](https://msdn.microsoft.com/library/windows/hardware/br230767.aspx)

 

 






