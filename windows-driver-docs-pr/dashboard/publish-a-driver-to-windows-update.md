---
title: Windows Update にドライバーを公開する
description: Windows Update にドライバーを公開するには、ハードウェア提出を作成し、次の手順に従います。
ms.assetid: E62AADCF-E481-40CA-98F1-BE4629C3EE35
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6684c1ca80719a6f2ab7de13b678ea0f32b21bfe
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392030"
---
# <a name="publish-a-driver-to-windows-update"></a>Windows Update にドライバーを公開する


Windows Update にドライバーを公開するには、[ハードウェア提出を作成](create-a-new-hardware-submission.md)し、次の手順に従います。

1. 配付するドライバーが含まれている[ハードウェア提出を検索します](manage-your-hardware-submissions.md)。

2. ハードウェア提出の **[配布]** セクションに移動し、 **[新しい出荷ラベル]** を選択します。

   ![新しい出荷ラベルのボタンを示すスクリーンショット](images/publish-new-shipping-label.png)

3. 出荷ラベル ページで、 **[詳細]** セクションに移動し、 **[出荷ラベル名]** フィールドに出荷ラベルの名前を入力します。 この名前を使用すると、出荷ラベルを整理して検索できます。

4. **[プロパティ]** セクションで、次の情報を入力します。

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
   <td><p><strong>Destination (公開先)</strong></p></td>
   <td><p>Windows Update にドライバーを公開するには、<strong>[Windows Update に公開する]</strong> を選択します。 ドライバーをパートナーと共有できるようにする共有出荷ラベルを作成する場合は、「<a href="sharing-drivers-with-your-partners.md" data-raw-source="[Share a driver with a partner](sharing-drivers-with-your-partners.md)">ドライバーをパートナーと共有する</a>」をご覧ください。</p>
   <div class="alert">
   <strong>注</strong>  共有ドライバーは、それを最初に作成した組織によってのみ共有できます。 共有ドライバーを受け取った組織がドライバーを再び共有することはできません。
   </div>
   <div>
     
   </div></td>
   </tr>
   <tr class="even">
   <td><p><strong>Specify the partner (if any) that is allowed visibility into this request (この要求を確認できるパートナーを指定する (パートナーがいる場合))</strong></p></td>
   <td><p>ドライバーや出荷ラベルに対する読み取り専用アクセス許可を持つパートナーを入力します。 このフィールドは、パートナーの代わりにドライバーを公開する場合など、この出荷ラベルの要求をパートナーに通知する必要がある場合に使用します。 詳しくは、<a href="https://docs.microsoft.com/previous-versions/mt786462(v=vs.85)" data-raw-source="[Publish a driver on behalf of a partner](https://docs.microsoft.com/previous-versions/mt786462(v=vs.85))">パートナーの代わりにドライバーを公開する方法に関するページ</a>をご覧ください。</p></td>
   </tr>
   <tr class="odd">
   <td><p><strong>Driver promotions (ドライバーのプロモーション)</strong></p></td>
   <td><p>既定では、Windows Update でのドライバーはオプションとしてマークされます。 これは、デバイスのドライバーが既にインストールされていない場合のみ、ドライバーが配信されることを意味します。 これらのオプションでは、既定の動作を上書きできますが、Microsoft による追加の評価が必要です。</p>
   <p>動的更新で利用できるようにドライバーをプロモートするには、<strong>[Windows のアップグレード中にこのドライバーを自動的に配信しインストールする]</strong> を選択します。</p>
   <p>ドライバーを [重要] にプロモートするには、<strong>[適用可能なすべてのシステムに対してこのドライバーを自動的に配信しインストールする]</strong> を選択します。</p></td>
   </tr>
   </tbody>
   </table>

   ![ラベル名と公開のプロパティを示すスクリーンショット](images/label-name-and-properties-windows-update.png)

5. **[ターゲット]** セクションで、公開するドライバー パッケージを選択します。

6. ドライバー パッケージを選択すると、 **[PNP を選択]** が使用可能になります。 ターゲットにするハードウェア ID を選択します。 ハードウェア ID の一覧の上にある検索ボックスを使って、特定のハードウェア ID またはオペレーティング システムを検索できます。

   一覧内のすべてのハードウェア ID を対象にするには、 **[すべて公開]** を選択します。

   特定のハードウェア ID を対象にするには、必要な各ハードウェア ID を検索し、 **[公開]** を選択します。

   すべてのハードウェア ID を対象としていた場合に、それらを削除する場合は、 **[すべて期限を終了する]** を選択します。

   特定のハードウェア ID のターゲット設定を削除する場合は、各ハードウェア ID を検索し、 **[期限を終了する]** を選択します。

   ![ターゲット セクションと PNP を示すスクリーンショット](images/publish-targeting-windows-update.png)

7. コンピューター ハードウェア ID (CHID) を追加する場合は、テキスト ボックスに各 CHID を入力し、 **[CHID の追加]** を選択します。 複数の CHID を一括して追加するには、各 CHID が改行で区切られていることを確認し、 **[複数の CHID を追加する]** を選択して、テキスト ボックスに CHID を貼り付けます。 テキスト ボックスの下の一覧で、追加したすべての CHID を表示できます。 一覧から CHID を削除するには、 **[削除]** を選択します。

>[!IMPORTANT]
> 次のバージョンの Windows では、CHID はサポートされていません。
> * Windows 8.1 以前のバージョン
> * Windows Server 2012 R2 以前
>
> ドライバーがこれらのオペレーティング システムのいずれかをターゲットとしている場合は、Windows 10 用 (CHID を追加できます) と下位バージョンのオペレーティング用 (CHID は追加できません) の 2 つの配送先住所ラベルを作成します。



8. Windows Update カタログおよび WSUS カタログでの配送先住所ラベルの公開を制限する場合は、 **[Limit Public Disclosure of this Shipping Label information.]\(この配送先住所ラベル情報の公開を制限する\)** ボックスをオフにします。  

   ![公開の制限を示しているスクリーンショット](images/limit-public-disclosure.PNG)

   それでもドライバーは公開されて Windows Update からダウンロードできますが、いずれのパブリック カタログ リストにも表示されません。

9. ドライバーが S モードの Windows 10 をターゲットとしている場合、両方のボックスをオンにして、以下を確認する必要があります。

   * ドライバーが、[S モードの Windows 10 ドライバー要件](https://docs.microsoft.com/windows-hardware/drivers/install/Windows10SDriverRequirements)に記載されているドライバー ポリシーに対応し、それに従っている。
   * ドライバーが S モードの Windows 10 のガイドラインに記載されている追加のコード整合性ポリシーに従っていることを確認する。
   * ドライバーのドライバー パッケージに、マイクロソフト以外の UI やアプリケーションが含まれていない。

   ![Windows 10 S のドライバーを提出するときに選択する必要がある 2 つのチェック ボックスのスクリーンショット](images/win-cloud-checkboxes.png)

10. Windows Update に要求を送信するには、 **[公開]** を選択します。 出荷ラベルを今すぐ公開しない場合は、 **[保存]** を選択できます。 出荷ラベルを後で公開するには、出荷ラベルを開いて **[公開]** を選択するか、ハードウェア提出ページから **[保留中の出荷ラベルをすべて公開]** を選択します。 **[保留中の出荷ラベルをすべて公開**] を選択すると、公開されていない出荷ラベルがすべて公開されることに注意してください。

 

 

