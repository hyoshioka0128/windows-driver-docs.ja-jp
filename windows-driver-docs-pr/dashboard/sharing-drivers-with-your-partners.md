---
title: パートナーとのドライバーの共有
description: パートナーとドライバーを共有するには、ハードウェア提出を作成し、以下の手順に従います。
ms.assetid: BB69EF13-9271-4B17-BB42-A503BCDB0DE1
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b4fe3e6b949d5bc327b8638b9bcf65852a93a7d
ms.sourcegitcommit: a0da18a4c5c636c4980e8ed77c6879e617299580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66373152"
---
# <a name="share-a-driver-with-a-partner"></a>パートナーとのドライバーの共有


パートナーとドライバーを共有するには、[ハードウェア提出を作成](create-a-new-hardware-submission.md)し、以下の手順に従います。

**注**  共有ドライバーは、それを最初に作成した組織によってのみ共有できます。 共有ドライバーを受け取った組織がドライバーを再び共有することはできません。

 

1. 共有するドライバーが含まれている[ハードウェア提出を検索します](manage-your-hardware-submissions.md)。

2. ハードウェア提出の **[配布]** セクションに移動し、 **[新しい出荷ラベル]** を選択します。

   ![新しい出荷ラベルのボタンを示すスクリーンショット](images/publish-new-shipping-label.png)

3. 出荷ラベル ページで、 **[詳細]** セクションに移動し、 **[出荷ラベル名]** フィールドに出荷ラベルの名前を入力します。 この名前はプライベートであり、パートナーによっては表示されません。 この名前を使用すると、出荷ラベルを整理して検索できます。

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

6. ドライバー パッケージを選択した後、**選択 PNPs**グリッドができるようになります。 特定のハードウェア ID、またはオペレーティング システムのハードウェア Id の一覧の上の検索ボックスを使用して検索できます。  パートナーは、任意のパブリケーションを作成するを共有するハードウェア ID の値に制限されます。 

   -   一覧内のすべてのハードウェア Id を対象と選択**共有すべて**します。

   -   特定のハードウェア Id を対象とハードウェア ID が必要なそれぞれの検索し、選択**共有**します。

   -   すべてのハードウェア Id およびそれらを削除する場合を対象とする場合は、選択**Revoke All**します。

   -   特定のハードウェア Id の対象となるを削除する各ハードウェア ID を検索および選択**取り消す**します。

7. 選択**発行**ドライバーの共有の最終処理を最下部にあります。 出荷ラベルを今すぐ公開しない場合は、 **[保存]** を選択できます。 出荷ラベルを後で公開するには、出荷ラベルを開いて **[公開]** を選択するか、ハードウェア提出ページから **[保留中の出荷ラベルをすべて公開]** を選択します。 **[保留中の出荷ラベルをすべて公開**] を選択すると、公開されていない出荷ラベルがすべて公開されることに注意してください。

## <a name="span-idrevokespanrevokerevoke-all"></a><span id="Revoke"></span>Revoke/取り消しすべて。  

共有の出荷ラベルからのハードウェア ID を取り消す、次の操作されます。

1.  受信側で既存の送信 ID は非推奨とされます。

2.  新しいプライベート プロダクト ID および調整されたハードウェア Id を持つ送信 ID は、パートナーと共有されます。  この新しいエンティティが同じ共有製品 ID が必要があります。  選択した場合**Revoke All**し、すべてのハードウェア Id が削除されます。

3.  パートナーが作成しようとしたときに、**新規**ラベルは、Windows 更新プログラムの配布、使用可能なハードウェア Id の一覧が変更を反映してのみ共有したハードウェア Id を一覧表示します。  **Revoke All**の場合も、そのハードウェア ID のグリッドを空にするとします。

> [!NOTE]
> ハードウェア ID を取り消す場合は、パートナーは、Windows Update に、共有の出荷ラベルを公開するが既に、**は削除されません**Windows Update カタログから既存の項目。  これは、そのパートナーでは、その期限が切れるまで公開されたは残ります。
>
> パートナーによって作成された既存の出荷ラベルは、非推奨の出荷ラベルにコンテンツを期限切れにのみ使用できます。
>
> パートナーからは、署名されたドライバーと非推奨の出荷ラベルから DUA シェル パッケージもダウンロードできます。
>
> 共有およびハードウェア ID を取り消し、元の INF を変更しません。
