---
title: パートナーとのドライバーの共有
description: パートナーとドライバーを共有するには、ハードウェア提出を作成し、以下の手順に従います。
ms.assetid: BB69EF13-9271-4B17-BB42-A503BCDB0DE1
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ffe84c58046ef7358cca109ab5da5e7bf47e6cc9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518632"
---
# <a name="share-a-driver-with-a-partner"></a>パートナーとのドライバーの共有


パートナーとドライバーを共有するには、[ハードウェア提出を作成](create-a-new-hardware-submission.md)し、以下の手順に従います。

**注**  共有ドライバーは、それを最初に作成した組織によってのみ共有できます。 共有ドライバーを受け取った組織がドライバーを再び共有することはできません。

 

1. 共有するドライバーが含まれている[ハードウェア提出を検索します](manage-your-hardware-submissions.md)。

2. ハードウェア提出の **[配布]** セクションに移動し、**[新しい出荷ラベル]** を選択します。

   ![新しい出荷ラベルのボタンを示すスクリーンショット](images/publish-new-shipping-label.png)

3. 出荷ラベル ページで、**[詳細]** セクションに移動し、**[出荷ラベル名]** フィールドに出荷ラベルの名前を入力します。 この名前はプライベートで、パートナーが表示することはできません。 この名前を使用すると、出荷ラベルを整理して検索できます。

   ![ラベル名とプロパティを示すスクリーンショット](images/publish-label-name-share-new.png)

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
   <td><p><strong>Destination (宛先)</strong></p></td>
   <td><p>パートナーとドライバーを共有するには、<strong>[他のパートナーに送信する]</strong> を選択します。 Windows Update の出荷ラベルを作成する場合は、「<a href="publish-a-driver-to-windows-update.md" data-raw-source="[Publish a driver to Windows Update](publish-a-driver-to-windows-update.md)">Windows Update にドライバーを公開する</a>」をご覧ください。</p></td>
   </tr>
   <tr class="even">
   <td><p><strong>Who is publishing? (公開元)</strong></p></td>
   <td><p>パートナーの会社名を検索し、選択します。</p></td>
   </tr>
   <tr class="odd">
   <td><p><strong>Required CHID targeting by receiver (受信側で必要な CHID ターゲット)</strong></p></td>
   <td><p>このオプションは、ドライバーに基づいて作成したすべての公開要求に CHID を適用することをパートナーに強制します。 これにより、多くのパートナー企業とハードウェア ID を共有する場合に、ユーザーを保護することができます。</p></td>
   </tr>
   </tbody>
   </table>

     

5. **[ターゲット]** セクションで、共有するドライバー パッケージを選択します。

   ![公開のターゲット設定を示すスクリーンショット](images/publish-targeting-new.png)

6. ドライバー パッケージを選択すると、**[PNP を選択]** が使用可能になります。 共有するハードウェア ID を選択します。 パートナーは、公開を作成する際に選択したハードウェア ID 値のみを使用できます。 ハードウェア ID の一覧の上にある検索ボックスを使って、特定のハードウェア ID またはオペレーティング システムを検索できます。

   -   一覧内のすべてのハードウェア ID を対象にするには、**[すべて公開]** を選択します。

   -   特定のハードウェア ID を対象にするには、必要な各ハードウェア ID を検索し、**[公開]** を選択します。

   -   すべてのハードウェア ID を対象としていた場合に、それらを削除する場合は、**[すべて期限を終了する]** を選択します。

   -   特定のハードウェア ID のターゲット設定を削除する場合は、各ハードウェア ID を検索し、**[期限を終了する]** を選択します。

7. ドライバーを共有するには、**[公開]** を選択します。 出荷ラベルを今すぐ公開しない場合は、**[保存]** を選択できます。 出荷ラベルを後で公開するには、出荷ラベルを開いて **[公開]** を選択するか、ハードウェア提出ページから **[保留中の出荷ラベルをすべて公開]** を選択します。 **[保留中の出荷ラベルをすべて公開**] を選択すると、公開されていない出荷ラベルがすべて公開されることに注意してください。

 

 





