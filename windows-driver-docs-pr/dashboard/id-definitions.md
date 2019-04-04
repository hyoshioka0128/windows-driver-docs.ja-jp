---
title: Windows パートナー センターの ID 定義
description: Windows パートナー センターの ID 定義
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71e176d4a0e6238885e1659df95b75c7d54fca60
ms.sourcegitcommit: a678a339f09fbd56a3a6124c0fe86194fedb2ed0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/07/2019
ms.locfileid: "57560591"
---
# <a name="dashboard-id-definitions"></a>ダッシュボード ID 定義

このトピックでは、パートナー センター申請に関連付けられる ID 番号を定義します。

Windows ハードウェア デベロッパー センター内では、各ドライバーの申請は次の 3 つの ID に関連付けられます: プライベート ID、共有 ID、申請 ID。 これらの 3 つの ID の関係を以下に示します。

![3 種類の ID の関係を示すスクリーンショット](images/id_relationship.png)

パートナー センターでは、製品のドライバー詳細ページにこれらの各 ID が一覧表示されます。

![3 種類の ID の関係を示すスクリーンショット](images/id_driver_details.png)

## <a name="id-definitions"></a>ID の定義

<table>
<thead>
<tr class="header">
<th>ID 名</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>共有製品 ID</p></td>
<td><p>この識別子は、ドライバーにアクセスできるすべてのアカウント間で共有されます。 共有製品 ID を使うと、特定の提出に関して連絡し、複数の組織間で提出の更新を追跡することが簡単になります。 ほとんどの場合、追跡して他のユーザーと共有する ID はこの ID です。</p></td>
</tr>
<tr class="even">
<td><p>プライベート製品 ID</p></td>
<td><p>プライベート製品 ID は、新製品が作成されるたびに生成される最上位の識別子です。 この ID は、特定の製品を個人的に参照し、その URL を予測する場合に最も役立ちます。
&gt; [!NOTE] &gt; 他のユーザーとドライバーを共有するときは、新しいプライベート製品 ID が割り当てられます。 製品に関して連絡する場合は、共有製品 ID を使います。
</p>
</td>
</tr>
<tr class="odd">
<td><p>提出 ID</p></td>
<td><p>この識別子は、製品にアップロードした個々のパッケージを表します。 最初の提出と、すべての提出の更新それぞれに一意の識別子があります。 この ID は、製品内で Driver Update Acceptable (DUA) プロセスを使って更新を追跡する場合に最も役立ちます。 詳しくは、<a href="https://msdn.microsoft.com/windows/hardware/drivers/dashboard/manage-your-hardware-submissions" data-raw-source="[Manage your hardware submissions](https://msdn.microsoft.com/windows/hardware/drivers/dashboard/manage-your-hardware-submissions)">ハードウェア提出の管理に関するページ</a>をご覧ください。 </p></td>
</tr>
</tbody>
</table>

配送先住所ラベルには、2 つの追加 ID も含まれています。

|ID 名 | 説明|
|--- | ---|
|配送先住所ラベル ID | この識別子は、内部追跡に使われ、製品に割り当てられた配送先住所ラベルに割り当てられます。 ほとんどの場合、配送先住所ラベル ID を知る必要はありません。|
|プロモーション要求 ID | 配送先住所ラベルに Microsoft による手動レビューが必要な場合、プロモーション要求 ID が付与されます。 これは、ドライバー配送ルームにおける一意の配送先住所ラベルを表します。 サポートに関するすべての問い合わせにこの ID を含める必要があります。|

## <a name="related-topics"></a>関連トピック

* [ハードウェア申請の管理](https://msdn.microsoft.com/windows/hardware/drivers/dashboard/manage-your-hardware-submissions)

* [配送先住所ラベルでドライバーの配布を管理する](https://msdn.microsoft.com/windows/hardware/drivers/dashboard/manage-driver-distribution-by-submission)
