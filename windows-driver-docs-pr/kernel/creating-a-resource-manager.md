---
title: リソース マネージャーの作成
description: リソース マネージャーの作成
ms.assetid: b2841d56-650a-487c-a002-2521cd1b461b
keywords:
- リソースマネージャー WDK KTM、リソースマネージャーの作成
- WDK KTM の参加、読み取り専用の参加
- 読み取り専用の参加リスト WDK KTM
- リソースマネージャー WDK KTM、揮発性リソースマネージャー
- 揮発性リソースマネージャー WDK KTM
- リソースマネージャー WDK KTM、TP への追加
- トランザクション処理システム WDK KTM、リソースマネージャーの追加
- TP WDK KTM、リソースマネージャーの追加
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d152ede92254bf463182300c9a9c2f6c167b6669
ms.sourcegitcommit: e1cfed28850a8208ea27e7a6a336de88c48e9948
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78402430"
---
# <a name="creating-a-resource-manager"></a>リソース マネージャーの作成


[*リソースマネージャー*](transaction-processing-terms.md#ktm-term-resource-manager)は、各トランザクションのデータを管理し、トランザクションの操作をログに記録します。 トランザクション処理システム (TPS) に複数のリソースマネージャーがある場合、各リソースマネージャーは各トランザクションのコミット、ロールバック、および復旧操作に参加できます。

各リソースマネージャーは、トランザクションクライアントが、リソースマネージャーが管理するデータベースやその他のリソースにアクセスするために使用できるインターフェイスをエクスポートする必要があります。

通常、カーネルモードのリソースマネージャーは、次のタスクを一覧の順序で実行する必要があります。

1.  ログストリームを作成します。

    リソースマネージャーは、[共通ログファイルシステム](using-common-log-file-system.md)(CLFS) またはその他のログ記録機能を使用して、ログストリームを維持できます。 [**ClfsCreateLogFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfscreatelogfile)を呼び出すと、CLFS ログストリームが作成されます。 リソースマネージャーは、トランザクションのコミット、ロールバック、または復旧に必要な情報を記録するために、ログストリームを使用する必要があります。 また、KTM はログストリームを使用して、トランザクションの復旧に必要となる可能性がある内部状態の変更を記録します。

2.  トランザクションマネージャーオブジェクトを作成します。

    [**Zwcreatetransactionmanager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreatetransactionmanager)を呼び出すと、トランザクションマネージャーオブジェクトが作成され、resource manager によって指定された追加の CLFS log ストリームに接続されます。

3.  トランザクションマネージャーの状態を回復します。

    [**Zwを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecovertransactionmanager)呼び出すと、トランザクションマネージャーオブジェクトのログストリーム (KTM によって管理される) が読み取られ、すべてのトランザクションが完了する前に tp がシャットダウンされたかどうかが判断されます (たとえば、システムがクラッシュした場合など)。 KTM は、ログストリーム内の情報に基づいて内部状態を復元します。

4.  Resource manager オブジェクトを作成します。

    [**Zwcreateresourcemanager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreateresourcemanager)を呼び出すと、resource manager オブジェクトが作成され、以前に作成したトランザクションマネージャーオブジェクトに関連付けられます。

5.  Resource manager の状態を復旧します。

    [**Zw回復マネージャー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecoverresourcemanager)を呼び出すと、KTM によって RESOURCE manager トランザクションが送信され、前回リソースマネージャーがシャットダウンしたときに進行中だったすべてのトランザクションについて通知\_復旧するように通知され\_ます。 リソースマネージャーがこれらの通知に応答する方法については、「[復旧操作の処理](handling-recovery-operations.md)」を参照してください。

6.  クライアントからトランザクションを受信します。

    通常、クライアントはトランザクションオブジェクトを作成し、リソースマネージャーのクライアントインターフェイスを使用して、トランザクションオブジェクトの GUID をリソースマネージャーに渡します。 たとえば、リソースマネージャーは、「 [TPS コンポーネント](understanding-tps-components.md)について」トピックで説明されているような*createdataobject*ルーチンを提供する場合があります。

7.  各トランザクションに参加します。

    [**Zwopentransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntopentransaction)を呼び出すと、トランザクションオブジェクトへのハンドルが開き、 [**Zwopentransaction リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreateenlistment)を呼び出すと、トランザクションの参加リストが作成されます。 この参加により、リソースマネージャーは、指定された一連の[トランザクション通知](transaction-notifications.md)を受け取ることができます。

8.  トランザクション通知の受信を有効にします。

    リソースマネージャーは[**Zwgetnotificationresourcemanager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntgetnotificationresourcemanager)を呼び出して通知を同期的に取得できます。または、 [**Tmenablecallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-tmenablecallbacks)を呼び出して、通知が使用可能になるたびに KTM が呼び出す*ResourceManagerNotification*コールバックルーチンを登録できます。

9.  クライアントからのサービスリソースへのアクセス要求ですが、変更は永続的ではありません。

    クライアントは、トランザクションオブジェクトを作成した後、リソースマネージャーのリソースにアクセスするために、resource manager のインターフェイスを呼び出します。 たとえば、データベースのリソースマネージャーは、データベースに対する読み取りと書き込みの要求を受け取る場合があります。

    リソースマネージャーは、トランザクションの操作がコミット、ロールバック、または復旧されるという通知を受信するまで、読み取り操作と書き込み操作の結果を[CLFS ログストリーム](using-log-streams-with-ktm.md)またはその他のログ機能に記録する必要があります。

10. クライアント操作をコミットまたはロールバックします。

    最終的に、リソースマネージャーは、クライアントが実行した操作のコミットまたはロールバックを開始する通知を受け取ります。 応答として、リソースマネージャーは、クライアント操作を永続的にするか破棄するかのどちらかにする必要があります。 コミットとロールバックの通知を処理する方法の詳細については、「[トランザクション操作の処理](handling-transaction-operations.md)」を参照してください。

    場合によっては、リソースマネージャーが、コミットまたはロールバックの通知を迅速に提供するように、KTM に強制することが必要になることがあります。これは、リソースマネージャーが、デバイスが突然削除されたと判断したためです。 このような場合、リソースマネージャーは[**TmRequestOutcomeEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-tmrequestoutcomeenlistment)を呼び出すことができます。

11. 参加リストオブジェクトハンドルを閉じます。

    リソースマネージャーがトランザクションの処理を完了したら、 [**Zwclose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)を呼び出して、参加オブジェクトのハンドルを閉じる必要があります。

12. Resource manager オブジェクトハンドルとトランザクションマネージャーオブジェクトハンドルを閉じます。

    リソースマネージャーがアンロードされる前に、 [**Zwclose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)を呼び出して、resource manager オブジェクトのハンドルとトランザクションマネージャーオブジェクトのハンドルを閉じる必要があります。

手順 1. ~ 5. は、resource manager の初期化コードで実行する必要があります。 たとえば、リソースマネージャーがカーネルモードドライバーの場合、初期化コードはドライバーの[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンです。

手順 6 ~ 11 は、通常、トランザクションクライアントからの要求に応答するコードで実行されます。

手順12は、カーネルモードドライバーの[*アンロード*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)ルーチンなど、リソースマネージャーの最終的なクリーンアップコードで実行する必要があります。

## <a href="" id="kernel-creating-a-read-only-enlistment"></a>読み取り専用の参加リストの作成


読み取り専用の*参加リスト*は、KTM からの通知を受け取らない参加リストです。 リソースマネージャーは、 [**ZwReadOnlyEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntreadonlyenlistment)を呼び出すことによって、任意の参加を読み取り専用にすることができます。 この呼び出しにより、KTM はリソースマネージャーへの通知の配信を停止します。

リソースマネージャーが[**Zwcreateenlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreateenlistment)を呼び出した後は、通常、 [**ZwZwReadOnlyEnlistment complete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntpreparecomplete)を呼び出した時点まで、いつでも呼び出しを行うことができます。

リソースマネージャーで**ZwReadOnlyEnlistment**を呼び出す必要がある理由は2つあります。

-   リソースマネージャーがトランザクションに参加しています。トランザクションを受信する前に、コミット通知\_通知\_トランザクションを受け取ると、リソースマネージャーは、トランザクションのコミット操作に参加する必要がなくなったと判断します。

    たとえば、リソースマネージャーがトランザクションを受信して、通知を準備\_通知\_場合、トランザクションの操作によってリソースマネージャーのデータベースが変更されていないと判断されることがあります。 リソースマネージャーは、 **ZwZwReadOnlyEnlistment complete**の代わりにを呼び出して、トランザクションから自身を削除できます。

-   リソースマネージャーは、どのトランザクションのコミット操作にも参加しません。

    たとえば、リソースマネージャーが、格納されているデータベースを変更せずに、クライアントが送信するデータを監視する場合があります。 この場合、リソースマネージャーは、 **Zwcreateenlistment**を呼び出した直後に**ZwReadOnlyEnlistment**を呼び出す可能性があります。 また、このトピックの次のセクションで説明するように、このようなリソースマネージャーを*揮発性*にすることもできます。

リソースマネージャーは**ZwReadOnlyEnlistment**を呼び出した後、 [**zwclose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)を呼び出して参加ハンドルを閉じることができます。

## <a href="" id="kernel-creating-a-volatile-resource-manager"></a>揮発性リソースマネージャーの作成


*揮発性リソースマネージャー*は、持続性のあるデータを保持しないリソースマネージャーです。 たとえば、リソースマネージャーによって永続的に格納データベースが変更されない場合、クライアントから送信されるデータを監視するための揮発性リソースマネージャーを作成することができます。 通常、揮発性リソースマネージャーはトランザクションの利用状況をログに記録しないため、復旧操作やロールバック操作を実行できません。

Volatile リソースマネージャーは、 [**Zwcreateresourcemanager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreateresourcemanager)を呼び出すときに、RESOURCE\_MANAGER\_volatile フラグを設定する必要があります。 このフラグが設定されている場合、KTM は、関連付けられているトランザクションマネージャーオブジェクトのログストリーム内のリソースマネージャーに関する情報をログに記録しません。

リソースマネージャーは、 [**Zwcreatetransactionmanager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreatetransactionmanager)を呼び出すときに、トランザクション\_マネージャー\_VOLATILE フラグを設定することもできます。 このフラグが設定されている場合、KTM はトランザクションマネージャーオブジェクトのログストリームを作成しません。 さらに、トランザクションマネージャーオブジェクトに接続されている追加のリソースマネージャーも揮発性である必要があります。また、RESOURCE\_MANAGER\_VOLATILE フラグを設定する必要があります。

## <a name="adding-a-resource-manager-to-an-existing-tps"></a>既存の TP へのリソースマネージャーの追加


既存の TP にリソースマネージャーを追加する必要がある場合は、次の2つの選択肢があります。

-   新しいリソースマネージャーは、 [**Zwcreatetransactionmanager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreatetransactionmanager)を呼び出して、独自のトランザクションマネージャーオブジェクトを作成します。

    リソースマネージャーが TP 内の他のリソースマネージャーと通信しない場合は、このオプションを使用します。

-   新しいリソースマネージャーが[**Zwopentransactionmanager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntopentransactionmanager)を呼び出して、既存のトランザクションマネージャーオブジェクトに接続します。

    リソースマネージャーが TP 内の他のリソースマネージャーと通信する必要がある場合は、このオプションを使用します。 **Zwcreatetransactionmanager**を呼び出すリソースマネージャーは、トランザクションマネージャーオブジェクトの GUID、ログストリーム名、またはオブジェクト名を共有して、他のリソースマネージャーが**Zwcreatetransactionmanager**を呼び出せるようにする必要があります。 これらの他のリソースマネージャーは、 [**Zwqueryinformationtransactionmanager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntqueryinformationtransactionmanager)を呼び出して、トランザクションマネージャーオブジェクトに関する追加情報を取得できます。

リソースマネージャーを TP に追加した後、リソースマネージャーを認識しているクライアントは、リソースマネージャーのクライアントインターフェイスを呼び出すことができます。

 

 




