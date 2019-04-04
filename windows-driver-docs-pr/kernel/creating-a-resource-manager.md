---
title: リソース マネージャーの作成
description: リソース マネージャーの作成
ms.assetid: b2841d56-650a-487c-a002-2521cd1b461b
keywords:
- リソース マネージャー WDK KTM、リソース マネージャーの作成
- WDK KTM、読み取り専用の参加リストの登録
- 読み取り専用の参加リスト WDK KTM
- WDK KTM、揮発性リソース マネージャーのリソース マネージャー
- 揮発性リソース マネージャー WDK KTM
- リソース マネージャー、TP への追加の WDK KTM
- トランザクション処理システム リソース マネージャーの追加の WDK KTM
- TP WDK KTM、リソース マネージャーの追加
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06706db926cbc3d7c062f0fabbc8042b1ef1ebe2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530502"
---
# <a name="creating-a-resource-manager"></a>リソース マネージャーの作成


[*リソース マネージャー* ](transaction-processing-terms.md#ktm-term-resource-manager)各トランザクションのデータを維持し、トランザクションの操作を記録します。 トランザクション処理システム (TPS) で、複数のリソース マネージャーにある場合、各リソース マネージャーは、各トランザクションのコミット、ロールバック、および回復操作に参加できます。

各リソース マネージャーは、データベースまたはその他のリソース マネージャーを保持するリソースにアクセスするトランザクションのクライアントが使用できるインターフェイスをエクスポートする必要があります。

通常、カーネル モードのリソース マネージャーでは、一覧の順序で次のタスクを実行する必要があります。

1.  ログ ストリームを作成します。

    リソース マネージャーが使用できる、 [Common Log File System](using-common-log-file-system.md) (CLFS)、またはそのログ ストリームを維持するために他のログ機能。 呼び出し[ **ClfsCreateLogFile** ](https://msdn.microsoft.com/library/windows/hardware/ff540792) CLFS ログのストリームを作成します。 リソース マネージャーは、コミット、ロールバック、またはトランザクションの復旧のために必要なすべての情報を記録するのにログ ストリームを使用する必要があります。 さらに、KTM では、トランザクションを復旧するのにために必要になる可能性がある内部状態変更を記録するのにログ ストリームを使用します。

2.  トランザクション マネージャー オブジェクトを作成します。

    呼び出し[ **ZwCreateTransactionManager** ](https://msdn.microsoft.com/library/windows/hardware/ff566430)トランザクション マネージャー オブジェクトを作成し、リソース マネージャーを指定する追加の CLFS ログ ストリームに、resource manager を接続します。

3.  トランザクション マネージャーの状態を回復します。

    呼び出し[ **ZwRecoverTransactionManager** ](https://msdn.microsoft.com/library/windows/hardware/ff567079)トランザクション マネージャー (KTM を保持) するオブジェクトのログ ストリームを読み取ると、すべてのトランザクションが完了した (前に、TP がシャット ダウンするかどうかを決定します。システムがクラッシュしました) たとえば、原因。 KTM では、ログ ストリームの情報に基づく内部の状態を復元します。

4.  リソース マネージャー オブジェクトを作成します。

    呼び出し[ **ZwCreateResourceManager** ](https://msdn.microsoft.com/library/windows/hardware/ff566427)リソース マネージャー オブジェクトを作成し、以前に作成したトランザクション マネージャー オブジェクトに関連付けます。

5.  リソース マネージャーの状態を回復します。

    呼び出し[ **ZwRecoverResourceManager** ](https://msdn.microsoft.com/library/windows/hardware/ff567078) KTM トランザクション リソース マネージャーを送信すると、\_通知\_トランザクションが進行中の回復の通知最後に、リソース マネージャーがシャット ダウンします。 リソース マネージャーがこれらの通知に応答する方法については、[回復操作の処理](handling-recovery-operations.md)を参照してください。

6.  クライアントからトランザクションを受信します。

    通常、クライアントは、トランザクション オブジェクトを作成し、リソース マネージャーのクライアント インターフェイスを使用して、リソース マネージャーにトランザクション オブジェクトの GUID を渡します。 たとえば、リソース マネージャーを取得、 *CreateDataObject*はのようなルーチンを[TP コンポーネントについて](understanding-tps-components.md)トピックについて説明します。

7.  各トランザクションに参加します。

    呼び出し[ **ZwOpenTransaction** ](https://msdn.microsoft.com/library/windows/hardware/ff567033) 、トランザクション オブジェクトを識別するハンドルとしへの呼び出しを開きます[ **ZwCreateEnlistment** ](https://msdn.microsoft.com/library/windows/hardware/ff566422)を作成します。トランザクションに参加します。 参加リストにより、リソース マネージャーは、指定された一連の受信[トランザクション通知](transaction-notifications.md)します。

8.  トランザクション通知の受信を有効にします。

    リソース マネージャーを呼び出すことができます[ **ZwGetNotificationResourceManager** ](https://msdn.microsoft.com/library/windows/hardware/ff566467)同期的に、通知を取得するか、呼び出すことができます[ **TmEnableCallbacks**](https://msdn.microsoft.com/library/windows/hardware/ff564676)を登録する、 *ResourceManagerNotification* KTM を呼び出すたびに、通知が使用可能なコールバック ルーチン。

9.  サービス リソースへのアクセスをクライアントから要求が、変更しないでください、永続的です。

    クライアントがトランザクション オブジェクトを作成した後は通常、リソース マネージャーのリソースにアクセスするリソース マネージャーのインターフェイスを呼び出します。 たとえば、データベースのリソース マネージャーからの読み取りをデータベースに書き込む要求を受信する可能性があります。

    リソース マネージャーは、読み取りの結果を記録する必要があり、書き込み操作、 [CLFS ログ ストリーム](using-log-streams-with-ktm.md)またはその他のログ機能となる操作のトランザクションのコミットをロールバックし、通知を受信するまで、または回復します。

10. コミットまたはクライアントの操作をロールバックします。

    リソース マネージャーが開始する通知を受け取る最終的には、コミットや、クライアントが実行される操作をロールバックします。 応答では、resource manager は必要があります、永続的なクライアント操作を行うまたはいずれかして破棄します。 コミットとロールバック通知を処理する方法の詳細については、[トランザクション操作の処理](handling-transaction-operations.md)を参照してください。

    場合によっては、リソース マネージャーは、迅速に、リソース マネージャーがデバイスでは、突然削除されたことを確認するため、commit または rollback の通知をおそらく提供 KTM を強制しようとする必要があります。 このような場合は、resource manager を呼び出すことができます[ **TmRequestOutcomeEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff564727)します。

11. 参加リスト オブジェクトのハンドルを閉じます。

    呼び出す必要がありますが、リソース マネージャーは、トランザクションの処理が終了したら、 [ **ZwClose** ](https://msdn.microsoft.com/library/windows/hardware/ff566417)を参加オブジェクトのハンドルを閉じる

12. Resource manager のオブジェクトのハンドルと、トランザクション マネージャー オブジェクトのハンドルを閉じます。

    リソース マネージャーをアンロードする前に呼び出す必要があります[ **ZwClose** ](https://msdn.microsoft.com/library/windows/hardware/ff566417)リソース マネージャー オブジェクトのハンドルと、トランザクション マネージャー オブジェクトのハンドルを閉じます。

リソース マネージャーの初期化コードでは、手順 1. ~ 5. を実行する必要があります。 たとえば、リソース マネージャーが、カーネル モード ドライバーの場合は、初期化コードは、ドライバーの[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチン。

手順 6 ~ 11 は通常、トランザクションのクライアントからの要求に応答するコードで実行されます。

手順 12 は、カーネル モード ドライバーのなどのリソース マネージャーの最終的なクリーンアップ コードで実行する必要があります[*アンロード*](https://msdn.microsoft.com/library/windows/hardware/ff564886)ルーチン。

## <a href="" id="kernel-creating-a-read-only-enlistment"></a> 読み取り専用の参加リストを作成します。


A*読み取り専用の参加*KTM から通知を受信しませんが、参加リストであります。 リソース マネージャーと、任意参加読み取り専用呼び出して[ **ZwReadOnlyEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff567074)します。 この呼び出しにより、KTM をリソース マネージャーへの通知の配信を停止します。

マネージャーが呼び出されて、リソースの後に[ **ZwCreateEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff566422)、呼び出すことができます**ZwReadOnlyEnlistment**を呼び出す場合と通常時点までいつでも[**ZwPrepareComplete**](https://msdn.microsoft.com/library/windows/hardware/ff567037)します。

Resource manager を呼び出すかを 2 つの理由がある**ZwReadOnlyEnlistment**します。

-   リソース マネージャーがされた参加しているトランザクションで、ある時点でトランザクションを受信する前に\_通知\_不要になったことへのトランザクションの参加がコミット通知では、リソース マネージャーを決定します操作をコミットします。

    たとえば、リソース マネージャーがトランザクションを受信すると\_通知\_PREPARE 通知を受け取る可能性がありますを確認し、リソース マネージャーのデータベースを変更されていないトランザクションの操作のことです。 リソース マネージャーを呼び出すことができます**ZwReadOnlyEnlistment**の代わりに**ZwPrepareComplete**自体をトランザクションから削除します。

-   リソース マネージャーは、任意のトランザクションのコミット操作で関与しません。

    たとえば、resource manager は、格納されているデータベースを変更することがなく、クライアントが送信するデータを監視する可能性があります。 この場合は、resource manager を呼び出すことができます**ZwReadOnlyEnlistment**を呼び出した後にすぐに**ZwCreateEnlistment**します。 さらに、そのようなリソース マネージャーを選択する可能性があります*揮発性*、このトピックの次のセクションで説明します。

リソース後マネージャーが呼び出されて**ZwReadOnlyEnlistment**、呼び出すことができます[ **ZwClose** ](https://msdn.microsoft.com/library/windows/hardware/ff566417)登録ハンドルを閉じます。

## <a href="" id="kernel-creating-a-volatile-resource-manager"></a> 揮発性リソース マネージャーの作成


A*揮発性リソース マネージャー*リソース マネージャーであり、永続的なデータを保持しません。 たとえば、リソース マネージャーは、永続的に格納されているデータベースを変更しない場合は、揮発性リソース マネージャーは、クライアントから送信された監視データを作成する場合があります。 揮発性リソース マネージャーは、通常のトランザクション アクティビティを記録しないと、復元またはロールバック操作を実行できません。

揮発性リソース マネージャーは、リソースを設定する必要があります\_MANAGER\_を呼び出すときに、揮発性フラグ[ **ZwCreateResourceManager**](https://msdn.microsoft.com/library/windows/hardware/ff566427)します。 このフラグが設定されている場合、KTM は、関連付けられているトランザクション マネージャー オブジェクトのログ ストリームでは、リソース マネージャーに関する情報を記録しません。

リソース マネージャーがトランザクションを設定できますも\_MANAGER\_を呼び出すときに、揮発性フラグ[ **ZwCreateTransactionManager**](https://msdn.microsoft.com/library/windows/hardware/ff566430)。 このフラグを設定すると、KTM トランザクション マネージャー オブジェクトのログ ストリームは作成されません。 さらに、トランザクション マネージャーのオブジェクトに接続されている任意の他のリソース マネージャする必要がありますもを volatile にして、リソースの設定\_MANAGER\_揮発性のフラグ。

## <a name="adding-a-resource-manager-to-an-existing-tps"></a>既存の TP へのリソース マネージャーの追加


既存の TP に他のリソース マネージャーを追加する場合は、2 つの選択肢があります。

-   新しい resource manager 呼び出し[ **ZwCreateTransactionManager** ](https://msdn.microsoft.com/library/windows/hardware/ff566430)独自のトランザクション マネージャー オブジェクトを作成します。

    リソース マネージャーが、TP では、他のリソース マネージャーと通信できない場合は、この選択を使用します。

-   新しい resource manager 呼び出し[ **ZwOpenTransactionManager** ](https://msdn.microsoft.com/library/windows/hardware/ff567035)既存のトランザクション マネージャー オブジェクトへの接続にします。

    この選択を使用して場合は、リソース マネージャーが、TP では、他のリソース マネージャーと通信する必要があります。 リソース マネージャーを呼び出す**ZwCreateTransactionManager**他のリソース マネージャーを呼び出すことができるように、トランザクション マネージャー オブジェクトの GUID、ログのストリーム名、またはオブジェクト名を共有する必要があります**ZwOpenTransactionManager**. これら他のリソース マネージャーを呼び出すことができます[ **ZwQueryInformationTransactionManager** ](https://msdn.microsoft.com/library/windows/hardware/ff567058)トランザクション マネージャーのオブジェクトに関する追加情報を取得します。

Tp、リソース マネージャーを追加した後、リソース マネージャーの対応するクライアントは、リソース マネージャーのクライアント インターフェイスを呼び出すことができます。

 

 




