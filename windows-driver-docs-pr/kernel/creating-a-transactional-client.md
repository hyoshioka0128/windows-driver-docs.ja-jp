---
title: トランザクション クライアントの作成
description: トランザクション クライアントの作成
ms.assetid: 75d4758b-dfba-431b-9bfa-9dcb98c2a7cc
keywords:
- トランザクションクライアント WDK KTM
- トランザクションクライアント WDK KTM、トランザクションクライアントの作成
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b282e284ea68e6ea4667fc4e4b4939cf34178e27
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828466"
---
# <a name="creating-a-transactional-client"></a>トランザクション クライアントの作成


トランザクション[*クライアント*](transaction-processing-terms.md#ktm-term-transactional-client)は、リソースマネージャーのエクスポートされたインターフェイスを使用して、リソースマネージャーがサポートするリソース (データベースなど) にアクセスするトランザクション処理システム (TPS) コンポーネントです。

通常、クライアントはトランザクションを作成し、一連のデータベース操作を実行した後、トランザクションをコミットして操作を永続的にします。 クライアントでエラーが発生した場合は、トランザクションをロールバックして、トランザクションをコミットする代わりにトランザクションの操作を削除できます。

通常、カーネルモードの KTM を使用するトランザクションクライアントは、トランザクションごとに次のタスクを実行する必要があります。

1.  トランザクションオブジェクトを作成します。

    [**Zwcreatetransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreatetransaction)を呼び出すと、トランザクションオブジェクトが作成され、オブジェクトハンドルが提供され、クライアントがリソースマネージャーに渡してトランザクションを識別できるオブジェクト識別子 (GUID) が割り当てられます。

2.  トランザクションオブジェクトの識別子を取得します。

    クライアントは、 [**Zwqueryinformationtransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntqueryinformationtransaction)を呼び出して、オブジェクト識別子を取得できます。

3.  トランザクションオブジェクトの識別子をリソースマネージャーに渡します。

    クライアントは、通常、リソースマネージャーのエクスポートされたインターフェイスを呼び出して、リソースマネージャーへの通信パスを開き、パスをトランザクションに関連付けます。 たとえば、リソースマネージャーは、「 [TPS コンポーネント](understanding-tps-components.md)について」トピックで説明されているような*createdataobject*ルーチンを提供する場合があります。

4.  トランザクションに含まれる操作を実行します。

    通常、クライアントはリソースマネージャーのインターフェイスを呼び出して、リソースマネージャーのリソースにアクセスします。 たとえば、データベースマネージャーのクライアントは、データベースの読み取りと書き込みを行うことができます。

5.  トランザクションをコミットまたはロールバックします。

    すべてのリソース操作が成功した場合、クライアントは[**Zwcommittransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommittransaction)を呼び出して操作を永続的にする必要があります。 操作が失敗した場合、クライアントは**Zwcommittransaction**ではなく[**ZwRollbackTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbacktransaction)を呼び出す必要があります。 たとえば、データベースマネージャーのクライアントが、一連の書き込み操作のいずれかが失敗したと判断した場合、クライアントは**ZwRollbackTransaction**を呼び出す必要があります。これにより、書き込み操作がすべて永続的になることはありません。

    クライアントは、 **Zwcommittransaction**と**ZwRollbackTransaction**を同期的または非同期的に呼び出すことができます。 クライアントがこれらのルーチンを同期的に呼び出す場合は、コミットまたはロールバックの操作が完了するまで、ルーチンは戻りません。

    トランザクションをコミットおよびロールバックする方法の詳細については、「[トランザクション操作の処理](handling-transaction-operations.md)」を参照してください。

6.  トランザクションオブジェクトハンドルを閉じます。

    クライアントがトランザクションの処理を完了したら、 [**Zwclose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)を呼び出してトランザクションオブジェクトのハンドルを閉じる必要があります。

TP には、複数のリソースマネージャーを含めることができます。 2つのリソースマネージャーがサポートする2つのデータベースなど、クライアントのトランザクションに複数のリソースに対する操作が含まれている場合、クライアントは通常、次の処理を実行します。

1.  トランザクションごとに1つのトランザクションオブジェクトを作成します。

2.  各リソースマネージャーにトランザクションオブジェクトの識別子を渡します。

3.  各リソースマネージャーのインターフェイスを呼び出すことにより、各データベースに対して操作を実行します。

4.  すべての操作がエラーなしで完了した場合はトランザクションをコミットし、エラーが検出された場合はトランザクションをロールバックします。

TP に*上位のトランザクションマネージャー*が含まれている場合、トランザクションクライアントは通常、KTM を呼び出しません。 上位トランザクションマネージャーとそのクライアントの詳細については、「[上位トランザクションマネージャーの作成](creating-a-superior-transaction-manager.md)」を参照してください。

トランザクションクライアントは、 [**Zwsetinformationtransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntsetinformationtransaction)を呼び出して、トランザクション固有の情報を設定できます。 たとえば、クライアントは、トランザクションのタイムアウト値を設定したり、わかりやすい文字列を指定したりすることができます。 クライアントは、 [**Zwqueryinformationtransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntqueryinformationtransaction)を呼び出して、トランザクションに関する情報を取得できます。 たとえば、クライアントはこのルーチンを呼び出して、トランザクションがコミットまたはロールバックされたかどうかを判断できます。

 

 




