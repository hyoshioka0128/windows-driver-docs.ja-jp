---
title: 通信モデル、同期、および中止
description: このセクションでは、WDI 通信モデル、同期、および中止について説明します。
ms.assetid: 575D1314-8726-49C1-AE6C-C171FE1CD2AD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61c1afebe5f124a97184814f870374981c7fde41
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324418"
---
# <a name="communication-model-synchronization-and-abort"></a>通信モデル、同期、および中止


大まかに言えば、このドキュメントには 2 種類のオブジェクトを定義します。

1.  Wi-fi デバイスを表すアダプター。
2.  アダプターで別の MAC および PHY エンティティを表すポート。

これらのオブジェクトの詳細については、次を参照してください。 [Wi-fi デバイス モデルとオブジェクト](wdi-objects.md)します。
一連の許容される操作は、のコマンドは、これらの各オブジェクトに対して定義されます。 コマンドは、さらに、プロパティとタスクに分類されます。

プロパティ コマンドは、単純なコマンド (信号の強度を取得する現在 BSS リストの取得し、パケット フィルターを設定です)。 時間の短時間で完了され、実装するために複雑ではありません。

タスクのコマンドは、完了までに数秒を受け取る可能性のある複雑な操作です。 たとえば、Wi-fi のスキャン操作は、このモデルでのタスクとして分類されます。

IHV コンポーネントに対して発行されたすべてのコマンドは、非同期的に実行できます。

## <a name="sequence-of-messages"></a>メッセージのシーケンス


コマンドの種類ごとにメッセージのシーケンスは、次の図に表示されます。

図 1 は、コマンドのタスク シーケンスを示します。

![wdi コマンド タスク フロー](images/wdi-command-task-flow.png)

図 2 は、コマンドのプロパティの流れを示します。

![wdi プロパティ コマンド フロー](images/wdi-property-command-flow.png)

図 3 は、の流れを示しています。

![wdi を示す値のフロー](images/wdi-indication-flow.png)

## <a name="synchronization"></a>同期


IHV コンポーネントの実装をシンプルにするには、モデルは、次の同期規則を定義します。

1.  コマンドは、手順 1. と 3. を図 1 と図 2 の間で常にシリアル化されます。 たとえば、新しいコマンドが発行されないアダプターに表示されるまで手順 3 でアダプターから。 これは、すべてのプロパティが相互にシリアル化されることも意味します。
2.  タスクのすべてのコマンドは、手順 1. ~ 4. に図 1 の間でシリアル化されます。 たとえば、アダプターでは、一度に 1 つのみのタスクが実行されます。 ただし、タスクが開始されると (図 1 の手順 3) アダプターは、プロパティ コマンド要求を取得することがあります。 タスクの次のコマンドが送信される前に、手順 3. と手順 4 の両方を完了する必要があります。
3.  プロパティの set コマンドは次の 2 つの種類 – タスクの開始後に送信できると、保留中のタスクでシリアル化する必要があります。
4.  データ パスは、ドキュメントの後半で説明されている特定の場合を除いてコマンド パスをシリアル化されません。
5.  同期スコープは、アダプター レベルのスコープです。
6.  開始されるタスクのサブセットを中止できます。 これは、優先度の高いタスク (A) を受信した場合は、低い優先順位タスク (B) の未処理、B 中止されることが、ホストによってを意味します。 優先順位付けの決定の合理化はこのドキュメントの範囲外はユーザー シナリオによって異なります。
7.  タスク コマンドでは、手順 4 は、手順 3. が完了する前に取得できます。 手順 4 が指定されている場合は、手順 3. はフェールバックできません。

## <a name="abort"></a>中止


開始された後、ほとんどのタスクを中止できます。 中止の目的は、アダプターは、完了を示す値 (図 1 ステップ 4) を送信することによってすばやくタスクの終了をトリガーします。 中止は、手順 3. ~ 4. に図 1 の間のウィンドウでのみ許可されます。 Abort を受信するには、アダプターが 50 ミリ秒内でタスクを完了する必要があります。 中止された後に受信すると、ほとんどのコマンド アダプターが、コマンドが開始する前に、状態にロールバックする必要はありません。 競合状態は、中止コマンドが発行されると、ホストのコンポーネントに到着する入力候補の間存在します。 この場合、IHV コンポーネントは、abort を既に完了しているタスクを受信する場合は、これ以上の操作は必要ありません IHV コンポーネントから中止操作を処理します。 タスクの中止は、IHV コンポーネントが、できるだけ早くのタスクをクリーンアップする必要がありますをシグナルだけです。 Abort が発行されている場合、コマンドの完了セマンティクスは変更されません。 Abort プロパティ コマンド、およびタスクの完了の表示、両方の完了は、すべてのケースで適切に通知する必要があります。

中止されることはできませんので、短い時間で完了するには、プロパティが予想されます。

タスクのコマンドでは、中止の特定のコマンドを対象とするホストを許可する一意の識別子があります。

 

 





