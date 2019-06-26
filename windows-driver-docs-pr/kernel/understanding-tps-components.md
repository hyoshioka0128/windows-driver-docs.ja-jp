---
title: TPS コンポーネントの概要
description: TPS コンポーネントの概要
ms.assetid: 4bc962fa-8c05-4b0f-b634-9c0f435907b7
keywords:
- トランザクション処理システム WDK KTM、コンポーネント
- TP WDK KTM、コンポーネント
- トランザクション処理システム WDK KTM、シナリオ
- TP WDK KTM、シナリオ
- リソース マネージャーでの TP の WDK KTM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ed116920d1437ee962b9ca306b675bfeb204475
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382949"
---
# <a name="understanding-tps-components"></a>TPS コンポーネントの概要


すべて[*トランザクション処理システム*](transaction-processing-terms.md#ktm-term-transaction-processing-system) (TP) カーネル トランザクション マネージャー (KTM) を使用して、 [Common Log File System](using-common-log-file-system.md) (CLFS) は、次を含める必要があります重要なコンポーネント:

-   A [*トランザクション マネージャー* ](transaction-processing-terms.md#ktm-term-transaction-manager) (KTM)

    KTM では、各トランザクションの状態を追跡し、システム障害後の回復操作を調整します。

-   1 つまたは複数[*リソース マネージャー*](transaction-processing-terms.md#ktm-term-resource-manager)

    指定すると、リソース マネージャーは、各トランザクションに関連付けられているデータを管理します。

-   1 つまたは複数の CLFS [*ログ ストリーム*](transaction-processing-terms.md#ktm-term-log-stream)

    トランザクション マネージャーとリソース マネージャーは、コミット、ロールバック、または、トランザクションの復旧に使用できる情報を記録 CLFS ログ ストリームを使用します。

-   1 つまたは複数[*トランザクション クライアント*](transaction-processing-terms.md#ktm-term-transactional-client)

    通常、トランザクションを作成し、トランザクションのコンテキスト内でのデータに対して操作を実行して、トランザクションのコミットまたはロールバックのいずれかの操作を開始しする、TP の各トランザクションのクライアントことができますと。

ここで紹介する、[単純な TP](#simple-tps) 1 つのリソース マネージャーを使ってより複雑な TP を格納している[複数のリソース マネージャー](#multiple-resource-managers-in-a-tps)、およびいくつか[TP の他のシナリオ](#other-tps-scenarios)。

[KTM を使用して](using-ktm.md)セクション KTM を使用して、TP コンポーネントを作成する方法の詳細について説明します。

### <a name="simple-tps"></a>単純な TP

単純な TP KTM、1 つのリソース マネージャーでは、CLFS から構成されます。 トランザクションのクライアントは、リソース マネージャーを提供するインターフェイスによって、リソース マネージャーと通信できます。

たとえば、データベース管理システムを作成するとします。 システムのクライアントが読み取りおよび書き込み、オブジェクトの操作を実行するデータベース オブジェクトを識別するハンドルを開くと、オブジェクト ハンドルを終了して、データベースにアクセスします。

容器から読み取りのセットをクリックし、書き込み操作をアトミックにように、システムの他のユーザーは、最終的な結果のみを参照してください。 クライアント トランザクションにデータベース操作のセットをバインドできるようにする TP を設計することで、その目的を達成できます。

システムでは、読み取りおよび書き込みのクライアントから要求への応答に、データベース内のデータを管理するリソース マネージャーを含める必要があります。 このリソース マネージャーは、クライアント トランザクションを関連付ける一連の読み取りと書き込み操作をできるようにするアプリケーション プログラミング インターフェイス (API) をエクスポートできました。

リソース マネージャーが読み込まれるときにする必要があります自体が登録 KTM を呼び出して[ **ZwCreateTransactionManager** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcreatetransactionmanager)と[ **ZwCreateResourceManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcreateresourcemanager). 次に、リソース マネージャーは、トランザクションに参加できます。

リソース マネージャーでデータ オブジェクトを作成、読み取り、データ オブジェクトに関連付けられているデータを書き込むようクライアントを有効にする関数のセットをサポートして、データ オブジェクトを閉じることがあります。 次の疑似コードは、クライアントからのコード シーケンスの例を示しています。

```cpp
CreateDataObject (IN TransactionID, OUT DataHandle);
ReadData (IN DataHandle, OUT Data);
WriteData (IN DataHandle, IN Data);
WriteData (IN DataHandle, IN Data);
WriteData (IN DataHandle, IN Data);
CloseDataObject (IN DataHandle);
```

呼び出す前に、クライアント、リソース マネージャーの*CreateDataObject* 、日常的なクライアントする必要がありますトランザクション オブジェクトを作成の KTM を呼び出すことによって[ **ZwCreateTransaction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcreatetransaction)ルーチンを呼び出して、トランザクション オブジェクトの識別子を取得および[ **ZwQueryInformationTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntqueryinformationtransaction)します。

クライアントを呼び出すと、リソース マネージャーの*CreateDataObject* 、日常的なクライアントに渡すと、トランザクション オブジェクトの識別子、リソース マネージャー。 リソース マネージャーを呼び出すことができます[ **ZwOpenTransaction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntopentransaction)トランザクション オブジェクト、しを識別するハンドルを取得することができますを呼び出す[ **ZwCreateEnlistment** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcreateenlistment)トランザクションに参加登録します。

この時点では、クライアントは、データ オブジェクトに対する操作の実行を開始できます。 クライアントでは、データ オブジェクトが作成されたときにトランザクション識別子が指定されて、ために、リソース マネージャーは、トランザクションにすべての読み取りおよび書き込み操作を割り当てることができます。

Resource manager では、クライアントが永続的な結果を加えずを指定するデータ操作のすべての結果を記録する必要があります。 通常、リソース マネージャーは、トランザクション ログのストリームを操作の結果を記録するのに CLFS を使用します。

KTM の呼び出し、クライアントは、マネージャーがトランザクションの操作を実行するリソースの呼び出しが完了したら、 [ **ZwCommitTransaction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommittransaction)ルーチン。 この時点では、KTM[通知](transaction-notifications.md)にする必要がありますように操作永続的なリソース マネージャー。 リソース マネージャーではログ ストリームから操作の結果が、データの永続的なストレージ メディアに移動します。 リソース マネージャーは、最後に、 [ **ZwCommitComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommitcomplete)コミット操作が完了した KTM を通知するためにします。

Resource manager へのクライアントの呼び出しのいずれかのエラーを報告する場合の対処*ReadData*または*WriteData*でしょうか。 クライアントが呼び出すことができます[ **ZwRollbackTransaction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrollbacktransaction)トランザクションをロールバックします。 その呼び出しの結果としては、KTM は、元の状態にデータを復元する必要がありますが、リソース マネージャーで通知します。 次に、クライアントでは、同じ操作用の新しいトランザクションを作成できますかまたは続行することも可能です。

次の疑似コードは、クライアントのトランザクション操作のより詳細なシーケンスの例を示します。

```cpp
    ZwCreateTransaction (&TransactionHandle, ...);
    ZwQueryInformationTransaction (TransactionHandle, ...);
    CreateDataObject (TransactionID, &DataHandle);
    Status = ReadData (DataHandle, &Data1);
    if (Status == Error) goto ErrorRollback;
    Status = WriteData (DataHandle, Data2);
    if (Status == Error) goto ErrorRollback;
    Status = WriteData (DataHandle, Data3);
    if (Status == Error) goto ErrorRollback;
    Status = WriteData (DataHandle, Data4);
    if (Status == Error) goto ErrorRollback;
    ZwCommitTransaction (TransactionHandle, ...);
    goto Leave;
ErrorRollback:
    ZwRollbackTransaction (TransactionHandle, ...);
Leave:
    ZwClose (TransactionHandle);
    return;
```

コミットまたはロールバック前に、トランザクションを作成した後、システムがクラッシュした場合はどうなりますか 呼び出す必要があります、リソース マネージャーが読み込まれるたびに[ **ZwRecoverTransactionManager** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrecovertransactionmanager)と[ **ZwRecoverResourceManager** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrecoverresourcemanager). 呼び出す**ZwRecoverTransactionManager**をそのログ ストリームを開いて、トランザクション履歴を読み取る KTM をによりします。 呼び出す**ZwRecoverResourceManager** KTM に参加しているトランザクションが、クラッシュ前に進行中のリソース マネージャーに通知すると、トランザクション リソース マネージャーが回復する必要がありますしたがってとします。

トランザクションのクライアントが呼び出された場合[ **ZwCommitTransaction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommittransaction)クラッシュの前にトランザクションがトランザクションのコミット操作の処理を開始した、リソース マネージャーは、復元できる必要があります、クラッシュする直前にポイントするトランザクションの状態。 クライアントが、クラッシュ前にトランザクションをコミットする準備完了でない場合、リソース マネージャーは、データを破棄し、トランザクションをロールバックします。

トランザクションのクライアントを記述する方法の詳細については、次を参照してください。[トランザクションのクライアントを作成する](creating-a-transactional-client.md)します。

リソース マネージャーを作成する方法の詳細については、次を参照してください。[リソース マネージャーを作成する](creating-a-resource-manager.md)します。

### <a name="multiple-resource-managers-in-a-tps"></a>複数のリソース マネージャーで、TP

ここで、TP により、両方のデータベースの変更が成功する場合にのみ、トランザクションが成功するようにクライアントは、単一のトランザクション内で 2 つの独立したデータベース内の情報を変更することをとします。

この場合、データベースごとに 2 つのリソース マネージャー、TP ことができます。 各リソース マネージャーは、クライアントは、リソース マネージャーのデータベースへのアクセスに使用できる API をエクスポートできます。

次の疑似コードは、クライアントが 2 つのリソース マネージャーをサポートする 2 つのデータベースでの操作を含む 1 つのトランザクションを作成する方法を示しています。

この例では、クライアントは、最初のデータベースからデータを読み取るし、2 番目のデータベースに書き込みます。 次に、クライアントは、2 番目のデータベースからデータを読み取るし、最初のデータベースに書き込みます。 (最初のリソース マネージャーで始まる関数をエクスポートする**Rm1**、実行して、2 番目のリソース マネージャーで始まる関数をエクスポートする**Rm2**)。

```cpp
    ZwCreateTransaction (&TransactionHandle, ...);
    ZwQueryInformationTransaction (TransactionHandle, ...);
    Rm1CreateDataObject (TransactionID, &Rm1DataHandle);
    Rm2CreateDataObject (TransactionID, &Rm2DataHandle);
    Status = Rm1ReadData (Rm1DataHandle, &Rm1Data);
    if (Status == Error) goto ErrorRollback;
    Status = Rm2WriteData (Rm2DataHandle, Rm1Data);
    if (Status == Error) goto ErrorRollback;
    Status = Rm2ReadData (Rm2DataHandle, &Rm2Data);
    if (Status == Error) goto ErrorRollback;
    Status = Rm1WriteData (Rm1DataHandle, Rm2Data);
    if (Status == Error) goto ErrorRollback;
    ZwCommitTransaction (TransactionHandle, ...);
    goto Leave;
ErrorRollback:
    ZwRollbackTransaction (TransactionHandle, ...);
Leave:
    ZwClose (TransactionHandle);
    return;
```

両方のリソース マネージャーを呼び出すことができますので、両方のリソース マネージャーに、クライアントが同じトランザクションの識別子を渡すと、 [ **ZwOpenTransaction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntopentransaction)と[ **ZwCreateEnlistment** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcreateenlistment)トランザクションに参加します。 クライアントが最終的に呼び出すと[ **ZwCommitTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommittransaction)、KTM[通知](transaction-notifications.md)操作恒久的なと、各マネージャーを作成する必要があること、各リソース マネージャーresource manager の呼び出し[ **ZwCommitComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommitcomplete)が完了するとします。

### <a name="other-tps-scenarios"></a>その他の TP のシナリオ

KTM では、他の TP のシナリオをサポートします。 たとえば、次のシナリオでは、コンポーネントが含まれる、TP について説明します。

-   複数のデータベースを管理する 1 つのリソース マネージャー。

    Resource manager の API には、クライアントを開き、一度に 1 つ以上のデータベースへのアクセスが有効にする可能性があり、クライアントは、単一のトランザクションで複数のデータベースへのアクセスを組み合わせることができました。

-   1 つのリソース マネージャー api を呼び出すと、クライアントと最初のリソース マネージャーは、Api を使用した追加のリソース マネージャー。

    クライアントは、最初のリソース マネージャーとのみ通信します。 リソース マネージャーがクライアントからの要求を処理するとき、クライアントの要求を処理する、必要に応じて、追加のリソース マネージャーにアクセスできます。 たとえば、リソース マネージャーは、クライアントで使用可能でない 2 つ目のリソース マネージャーからのバックアップやデータの検証操作を必要とするクライアントからアクセス可能なデータベースを管理します。

-   KTM を使用してリソース マネージャーの追加のセットで、既存のクライアントと、KTM を使用して resource manager が統合されています。

    ここでは、通常は変更する必要が既存の resource manager になるように、[優先的なトランザクション マネージャー](creating-a-superior-transaction-manager.md) KTM と通信します。

 

 




