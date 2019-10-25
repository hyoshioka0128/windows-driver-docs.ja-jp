---
title: コミット操作の処理
description: コミット操作の処理
ms.assetid: 4885476e-ce68-4674-b8a5-8a317f33cd5b
keywords:
- トランザクション WDK KTM、トランザクションのコミット
- トランザクションのコミット WDK KTM
- リソースマネージャー WDK KTM、トランザクションのコミット
- 単一フェーズコミット WDK KTM、マルチフェーズコミット WDK KTM
- 事前準備フェーズ WDK KTM
- 準備フェーズ WDK KTM
- コミットフェーズ WDK KTM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b30cd5f4c33a13af27c5d6b511fd70ce37b1eed5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836589"
---
# <a name="handling-commit-operations"></a>コミット操作の処理


コミット操作には、*単一フェーズコミット*と*マルチフェーズコミット*の2種類があります。 1フェーズコミット操作は、リソースマネージャーが応答する必要がある1つの通知で構成されます。また、マルチフェーズコミット操作には、準備手順のための追加の通知が含まれています。

単一フェーズコミット操作は実装が簡単です。 これは、次のいずれかの特性を持つトランザクション処理システム (TPSs) に適しています。

-   1つのリソースマネージャー。

-   複数のリソースマネージャー。ただし、そのうち1つは[読み取り](creating-a-resource-manager.md#kernel-creating-a-read-only-enlistment)専用であり、コミット操作には関与しません。

複数のリソースマネージャーがコミット操作に参加する場合は、マルチフェーズコミット操作が必要です。

### <a name="single-phase-commit-operations"></a>1フェーズコミット操作

TP が単一フェーズコミット操作をサポートするようにする場合は、1つのリソースマネージャーでトランザクションを受け取るために登録する必要があります。1つの\_フェーズで\_参加リストに対するコミット[通知](transaction-notifications.md)を\_\_通知します。 他のすべてのリソースマネージャーは[読み取り](creating-a-resource-manager.md#kernel-creating-a-read-only-enlistment)専用である必要があります。

[上位トランザクションマネージャー](creating-a-superior-transaction-manager.md)を含む tp は、単一フェーズコミットを使用できません。

トランザクションを受け取るようにリソースマネージャーが登録されている場合は、トランザクションクライアントが[**Zwcommittransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommittransaction)を呼び出すと、この種類の通知が送信され、\_\_\_フェーズが\_通知されます。

リソースマネージャーがトランザクションを受信したときに、1つのトランザクションのコミット通知を\_\_\_フェーズに通知\_、トランザクションをコミットするか、単一フェーズコミットを拒否することができます。

トランザクションをコミットするには、リソースマネージャーが次の操作を行う必要があります。

1.  [CLFS ログストリーム](using-log-streams-with-ktm.md)の[CLFS マーシャリング領域](clfs-marshalling-areas.md)など、永続的でないキャッシュ (メモリ内ストレージ) に保持しているすべてのデータをフラッシュします。

    リソースマネージャーは、キャッシュから永続ストレージメディアにデータを移動する必要があります。 たとえば、CLFS を使用しているリソースマネージャーは、 [**Clfsflushbuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsflushbuffers)を呼び出すことができます。

2.  すべてのデータ変更を永続的かつパブリックにします (つまり、リソースマネージャーのスコープ外に表示されます)。

3.  [**Zwcommitcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitcomplete)を呼び出します。

**Zwcommitcomplete**を呼び出した後、リソースマネージャーは[**zwclose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)を呼び出して、参加リストハンドルを閉じる必要があります。

トランザクションの1フェーズコミット操作を拒否するために、リソースマネージャーは[**ZwSinglePhaseReject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntsinglephasereject)を呼び出すことができます。 リソースマネージャーが**ZwSinglePhaseReject**を呼び出すと、KTM は直ちに、単一フェーズからマルチフェーズにコミット操作を変更します。

他のリソースマネージャーが同じトランザクションに参加する場合は、[読み取り](creating-a-resource-manager.md#kernel-creating-a-read-only-enlistment)専用である必要があります。 ただし、トランザクションを受信するために登録する必要があります。\_RM\_DISCONNECTED 通知を通知\_、単一フェーズコミット操作を処理しているリソースマネージャーが、トランザクションがコミットまたはロールバックされたことを示します。

### <a name="multi-phase-commit-operations"></a>複数フェーズのコミット操作

複数フェーズのコミット操作は、次のいずれかのイベントが発生したときに開始されます。

-   トランザクションクライアントが[**Zwcommittransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommittransaction)を呼び出していますが、トランザクションを受信するように登録されているリソースマネージャーがいません\_\_単一の\_フェーズ\_コミット通知を通知します。

-   リソースマネージャーは、トランザクションを受信した後に[**ZwSinglePhaseReject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntsinglephasereject)を呼び出し、\_単一\_フェーズ\_コミット通知を通知\_ます。

-   [上位トランザクションマネージャー](creating-a-superior-transaction-manager.md)が[**Zwpreの参加リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntpreprepareenlistment)を呼び出します。

複数フェーズのコミット操作は、*事前準備*、*準備*、*コミット*という3つの順次フェーズで構成されます。

**準備前段階**

このコミット操作の事前準備フェーズ (*フェーズ 0*とも呼ばれます) は、KTM がトランザクションを送信するときに開始し、すべてのリソースマネージャーに事前準備通知\_通知\_ます。 リソースマネージャーがトランザクションに対して1フェーズコミット操作をサポートしていない場合、または上位トランザクションマネージャーが[**Zwpreの参加リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntpreprepareenlistment)を呼び出す場合、KTM はこの通知を送信します。

各リソースマネージャーがトランザクションを受信し\_事前準備通知に通知\_には、次の操作を行う必要があります。

1.  [CLFS ログストリーム](using-log-streams-with-ktm.md)の[CLFS マーシャリング領域](clfs-marshalling-areas.md)など、永続的でないキャッシュ (メモリ内ストレージ) に保持しているすべてのデータをフラッシュします。

    リソースマネージャーは、キャッシュから永続ストレージメディアにデータを移動する必要があります。 たとえば、CLFS を使用しているリソースマネージャーは、 [**Clfsflushbuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsflushbuffers)を呼び出すことができます。

2.  [**Zwpreプロビジョニング完了**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntprepreparecomplete)を呼び出します。

リソースマネージャーは、 **Zwpreプロビジョニング完了**を呼び出した後も、引き続きクライアント要求を受信してサービスを提供できます。 ただし、リソースマネージャーは、永続的なストレージメディアに直ちに書き込まれるキャッシュパススルー操作として、すべてのデータ変更を処理する必要があります。

トランザクションを処理している間にリソースマネージャーでエラーが発生した場合、\_事前準備通知に通知\_には、 [**ZwRollbackEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbackenlistment)を呼び出してトランザクションをロールバックする必要があります。

**準備フェーズ**

このコミット操作の準備フェーズ (*フェーズ 1*とも呼ばれます) は、KTM がトランザクションを送信するときに開始し、すべてのリソースマネージャーへの通知を準備\_に通知\_通知します。 リソースマネージャーが単一フェーズコミットをサポートしていない場合、または上位トランザクションマネージャーが[**Zwの参加リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntprepareenlistment)を呼び出す場合、KTM は、トランザクション\_後にこの通知を送信して事前準備\_通知します。

各リソースマネージャーがトランザクションを受信し、通知を準備\_通知\_する場合は、次の操作を行う必要があります。

1.  クライアント要求のサービスを停止し、クライアントのエラーとして後続の要求をすべて報告します。

2.  すべてのデータが永続的なストレージに移動されていることを確認します。

3.  [**Zw分離完了**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntpreparecomplete)を呼び出します。

トランザクションを処理している間にリソースマネージャーでエラーが発生した場合は、通知を準備\_通知\_、トランザクションをロールバックするには[**ZwRollbackEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbackenlistment)を呼び出す必要があります。 ただし、リソースマネージャーは、 **Zw/complete**を呼び出した後にトランザクションをロールバックすることはできません。

**コミットフェーズ**

このコミット操作のコミットフェーズ (*フェーズ 2*とも呼ばれます) は、KTM がトランザクションを送信するときに開始し、すべてのリソースマネージャーに\_コミット通知を通知\_ます。 リソースマネージャーが単一フェーズコミットをサポートしていない場合、または上位トランザクションマネージャーが[**Zwcommitenlistment リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitenlistment)を呼び出す場合、KTM は、トランザクション\_後にこの通知を送信して\_準備します。

各リソースマネージャーは、コミット通知\_通知\_トランザクションを受け取ると、次の操作を行う必要があります。

1.  すべてのデータ変更を永続的かつパブリックにします (つまり、他のトランザクションから参照できます)。

    通常、リソースマネージャーは、トランザクションの保存されたデータをログストリームからデータベースの永続的な永続ストレージにコピーすることによって、変更を永続的かつパブリックにします。 ログストリームの使用方法の詳細については、「 [KTM でのログストリームの使用](using-log-streams-with-ktm.md)」を参照してください。

2.  [**Zwcommitcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitcomplete)を呼び出します。

リソースマネージャーは**Zwcommitcomplete**を呼び出した後、 [**zwclose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)を呼び出して参加リストハンドルを閉じる必要があります。

トランザクションを処理している間にリソースマネージャーでエラーが発生した場合、コミット通知\_通知\_は、それ自体をシャットダウンする必要があります。 次にオペレーティングシステムがリソースマネージャーを再読み込みするときに、リソースマネージャーの[復旧プロセス](handling-recovery-operations.md)では、エラーが発生する前に有効であると認識された状態にトランザクションを復元する必要があります。

 

 




