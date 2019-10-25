---
title: TPS コンポーネントの概要
description: TPS コンポーネントの概要
ms.assetid: 4bc962fa-8c05-4b0f-b634-9c0f435907b7
keywords:
- トランザクション処理システム WDK KTM、コンポーネント
- TPS WDK KTM、コンポーネント
- トランザクション処理システム WDK KTM、シナリオ
- TPS WDK KTM、シナリオ
- リソースマネージャー WDK KTM、TP 内
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b95cb452906859bedf6bee584e41a97e6de1a892
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836096"
---
# <a name="understanding-tps-components"></a>TPS コンポーネントの概要


カーネルトランザクションマネージャー (KTM) と[共通ログファイルシステム](using-common-log-file-system.md)(CLFS) を使用する[*トランザクション処理システム*](transaction-processing-terms.md#ktm-term-transaction-processing-system)(TPS) には、次の重要なコンポーネントが含まれている必要があります。

-   [*トランザクションマネージャー*](transaction-processing-terms.md#ktm-term-transaction-manager) (KTM)

    KTM は、各トランザクションの状態を追跡し、システムのクラッシュ後の復旧操作を調整します。

-   1つまたは複数の[*リソースマネージャー*](transaction-processing-terms.md#ktm-term-resource-manager)

    提供するリソースマネージャーは、各トランザクションに関連付けられているデータを管理します。

-   1つ以上の CLFS [*ログストリーム*](transaction-processing-terms.md#ktm-term-log-stream)

    トランザクションマネージャーとリソースマネージャーは、CLFS ログストリームを使用して、トランザクションのコミット、ロールバック、または復旧に使用できる情報を記録します。

-   1つ以上の[*トランザクションクライアント*](transaction-processing-terms.md#ktm-term-transactional-client)

    通常、TP の各トランザクションクライアントは、トランザクションを作成し、トランザクションのコンテキスト内でデータに対して操作を実行してから、トランザクションのコミットまたはロールバック操作を開始できます。

このトピックでは、1つのリソースマネージャーを使用した[単純な tps](#simple-tps) 、[複数のリソース](#multiple-resource-managers-in-a-tps)マネージャーを含むより複雑な tp、および[その他の tp シナリオ](#other-tps-scenarios)について説明します。

Ktm の[使用](using-ktm.md)に関するセクションでは、ktm を使用して tp コンポーネントを作成する方法について詳しく説明します。

### <a name="simple-tps"></a>単純な TPS

単純な TPS は、KTM、1つの resource manager、CLFS で構成されます。 トランザクションクライアントは、リソースマネージャーによって提供されるインターフェイスによって、リソースマネージャーと通信できます。

たとえば、データベース管理システムを作成するとします。 データベースオブジェクトへのハンドルを開き、オブジェクトに対して読み取りおよび書き込み操作を実行し、オブジェクトハンドルを閉じることで、システムのクライアントがデータベースにアクセスできるようにします。

ここで、読み取り操作と書き込み操作のセットをアトミックに実行して、システムの他のユーザーが最終的な結果のみを表示するようにするとします。 この目的を実現するには、クライアントがデータベース操作のセットをトランザクションにバインドできるようにする TP を設計します。

システムには、クライアントからの読み取りおよび書き込み要求に応答して、データベース内のデータを管理するリソースマネージャーを含める必要があります。 このリソースマネージャーは、クライアントが読み取りおよび書き込み操作のセットにトランザクションを関連付けることができるようにするアプリケーションプログラミングインターフェイス (API) をエクスポートできます。

リソースマネージャーが読み込まれるときに、 [**Zwcreatetransactionmanager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreatetransactionmanager)および[**Zwcreateresourcemanager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreateresourcemanager)を呼び出して、それ自体を KTM に登録する必要があります。 次に、リソースマネージャーをトランザクションに参加させることができます。

リソースマネージャーでは、クライアントがデータオブジェクトの作成、データオブジェクトに関連付けられたデータの読み取りと書き込み、およびデータオブジェクトの終了を可能にする一連の関数をサポートする必要がある場合があります。 次の擬似コードは、クライアントからのコードシーケンスの例を示しています。

```cpp
CreateDataObject (IN TransactionID, OUT DataHandle);
ReadData (IN DataHandle, OUT Data);
WriteData (IN DataHandle, IN Data);
WriteData (IN DataHandle, IN Data);
WriteData (IN DataHandle, IN Data);
CloseDataObject (IN DataHandle);
```

クライアントは、リソースマネージャーの*Createdataobject*ルーチンを呼び出すことができるようにするために、KTM の[**Zwcreatetransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreatetransaction)ルーチンを呼び出してトランザクションオブジェクトを作成し、を呼び出し[**てトランザクションオブジェクトの識別子を取得する必要があります。ZwQueryInformationTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntqueryinformationtransaction)。

クライアントがリソースマネージャーの*Createdataobject*ルーチンを呼び出すと、クライアントは、トランザクションオブジェクトの識別子をリソースマネージャーに渡します。 リソースマネージャーは、 [**Zwopentransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntopentransaction)を呼び出してトランザクションオブジェクトへのハンドルを取得し、 [**Zwopentransaction リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreateenlistment)を呼び出してトランザクションへの参加を登録できます。

この時点で、クライアントはデータオブジェクトに対する操作の実行を開始できます。 クライアントは、データオブジェクトの作成時にトランザクション識別子を提供したため、リソースマネージャーは、すべての読み取り操作と書き込み操作をトランザクションに割り当てることができます。

リソースマネージャーは、結果を永続的に作成せずに、クライアントが指定したデータ操作のすべての結果を記録する必要があります。 通常、リソースマネージャーは CLFS を使用して、操作の結果をトランザクションログストリームに記録します。

クライアントは、トランザクション操作を実行するためにリソースマネージャーの呼び出しを完了すると、KTM の[**Zwcommittransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommittransaction)ルーチンを呼び出します。 この時点で、KTM は、操作を永続的にする必要があることをリソースマネージャーに[通知](transaction-notifications.md)します。 次に、リソースマネージャーは、操作の結果をログストリームからデータの永続的なストレージメディアに移動します。 最後に、リソースマネージャーは[**Zwcommitcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitcomplete)を呼び出して、コミット操作が完了したことを KTM に通知します。

リソースマネージャーがクライアントの*ReadData*または*writedata*の呼び出しのいずれかでエラーを報告するとどうなりますか。 クライアントは[**ZwRollbackTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbacktransaction)を呼び出して、トランザクションをロールバックできます。 この呼び出しの結果として、KTM は、データを元の状態に復元する必要があることをリソースマネージャーに通知します。 次に、クライアントは、同じ操作に対して新しいトランザクションを作成することも、続行しないように選択することもできます。

次の擬似コードは、クライアントのトランザクション操作のより詳細なシーケンスの例を示しています。

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

トランザクションが作成されてからコミットまたはロールバックされる前に、システムがクラッシュした場合はどうなりますか? リソースマネージャーが読み込まれるたびに、 [**zwを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecovertransactionmanager)呼び出す必要があり[**ます。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecoverresourcemanager) **Zw回復 transactionmanager**を呼び出すと、KTM はログストリームを開き、トランザクション履歴を読み取ります。 **Zw回復マネージャー**を呼び出すと、KTM は、クラッシュ前に進行中だったすべての参加済みトランザクションとリソースマネージャーが復旧する必要があるトランザクションをリソースマネージャーに通知します。

トランザクションクライアントが、クラッシュ前のトランザクションに対して[**Zwcommittransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommittransaction)を呼び出し、トランザクションのコミット操作の処理を開始した場合、リソースマネージャーは、トランザクションの状態を、クラッシュ. クライアントがクラッシュする前にトランザクションをコミットする準備ができていなかった場合、リソースマネージャーはデータを破棄し、トランザクションをロールバックできます。

トランザクションクライアントを作成する方法の詳細については、「[トランザクションクライアントの作成](creating-a-transactional-client.md)」を参照してください。

リソースマネージャーの作成方法の詳細については、「[リソースマネージャーの作成](creating-a-resource-manager.md)」を参照してください。

### <a name="multiple-resource-managers-in-a-tps"></a>TP 内の複数のリソースマネージャー

ここで、TP によって、クライアントが1つのトランザクション内の2つの異なるデータベース内の情報を変更できるようになったので、両方のデータベースの変更が成功した場合にのみトランザクションが成功するとします。

この場合、TP は、データベースごとに1つずつ、2つのリソースマネージャーを持つことができます。 各リソースマネージャーは、クライアントがリソースマネージャーのデータベースにアクセスするために使用できる API をエクスポートできます。

次の擬似コードは、2つのリソースマネージャーがサポートする2つのデータベースに対する操作を含む1つのトランザクションをクライアントが作成する方法を示しています。

この例では、クライアントは最初のデータベースからデータを読み取り、2番目のデータベースに書き込みます。 次に、クライアントは2番目のデータベースからデータを読み取り、最初のデータベースに書き込みます。 (最初の resource manager は、 **Rm1**で始まる関数をエクスポートします。2つ目の resource manager は、 **Rm2**で始まる関数をエクスポートします)。

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

クライアントは両方のリソースマネージャーに同じトランザクション識別子を渡すため、両方のリソースマネージャーが[**Zwopentransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntopentransaction)と[**zwopentransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreateenlistment)を呼び出して、トランザクションに参加できます。 クライアントが最終的に[**Zwcommittransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommittransaction)を呼び出すと、KTM は、マネージャーが操作を永続的にする必要があることを各リソースマネージャーに[通知](transaction-notifications.md)します。各リソースマネージャーは、完了したときに[**zwcommittransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitcomplete)を呼び出します。

### <a name="other-tps-scenarios"></a>その他の TP のシナリオ

KTM では、他の TP シナリオがサポートされています。 たとえば、次のシナリオでは、TP に含まれる可能性のあるコンポーネントについて説明します。

-   複数のデータベースを管理する1つのリソースマネージャー。

    リソースマネージャーの API を使用すると、クライアントが一度に複数のデータベースを開いてアクセスできるようになり、クライアントは1つのトランザクションで複数のデータベースへのアクセスを組み合わせることができます。

-   1つのリソースマネージャー。クライアントが呼び出す API と、最初のリソースマネージャーが呼び出す Api を含む追加のリソースマネージャー。

    クライアントは、最初のリソースマネージャーとのみ通信します。 リソースマネージャーは、クライアントからの要求を処理するときに、必要に応じて、クライアントの要求を処理するために、追加のリソースマネージャーにアクセスできます。 たとえば、リソースマネージャーは、クライアントからアクセスできるデータベースを管理します。このデータベースは、クライアントが使用できない2番目のリソースマネージャーからバックアップまたはデータの検証操作を行う必要があります。

-   Ktm を使用しない既存のクライアントとリソースマネージャーが、KTM を使用する追加のリソースマネージャーのセットと統合されている。

    この場合、通常は、既存の resource manager を変更して、KTM と通信する[上位のトランザクションマネージャー](creating-a-superior-transaction-manager.md)になるようにする必要があります。

 

 




