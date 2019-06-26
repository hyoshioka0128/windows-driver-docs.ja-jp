---
title: トランザクション クライアントの作成
description: トランザクション クライアントの作成
ms.assetid: 75d4758b-dfba-431b-9bfa-9dcb98c2a7cc
keywords:
- WDK KTM トランザクションのクライアント
- トランザクション クライアント WDK KTM をトランザクションのクライアントを作成します。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b36e896890e0dfa4158a5bcbe5444fe977f418a2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377174"
---
# <a name="creating-a-transactional-client"></a>トランザクション クライアントの作成


A [*トランザクション クライアント*](transaction-processing-terms.md#ktm-term-transactional-client)はトランザクション データベースなどのリソースにアクセスするリソース マネージャーのエクスポートされたインターフェイスを使用するシステム (TP) コンポーネントを処理するリソース マネージャーサポートされています。

通常、クライアント トランザクションを作成します一連のデータベースの操作を実行します。 とし、操作する永続的なトランザクションをコミットします。 クライアントには、エラーが発生すると、そのことができますトランザクションをロールバック、トランザクションのコミットではなく、トランザクションの操作を削除します。

通常、カーネル モードの KTM を使用するトランザクションのクライアントでは、トランザクションごとに次のタスクを実行する必要があります。

1.  トランザクション オブジェクトを作成します。

    呼び出し[ **ZwCreateTransaction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcreatetransaction)トランザクション オブジェクトを作成、オブジェクトのハンドルを提供し、クライアントを識別するためにリソース マネージャーに渡すことができるオブジェクト識別子 (GUID) を割り当てます、トランザクションです。

2.  トランザクション オブジェクトの識別子を取得します。

    クライアントが呼び出すことができます[ **ZwQueryInformationTransaction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntqueryinformationtransaction)オブジェクト識別子を取得します。

3.  リソース マネージャーには、トランザクション オブジェクトの識別子を渡します。

    通常、クライアントは、リソース マネージャーのエクスポートされたインターフェイスを resource manager への通信パスを開くし、パスをトランザクションに関連付けるを呼び出します。 たとえば、リソース マネージャーを取得、 *CreateDataObject*はのようなルーチンを[TP コンポーネントについて](understanding-tps-components.md)トピックについて説明します。

4.  トランザクションに含まれる操作を実行します。

    通常、クライアントは、リソース マネージャーのリソースにアクセスするリソース マネージャーのインターフェイスを呼び出します。 たとえば、データベース マネージャーのクライアントはから読み取られ、データベースに書き込む可能性があります。

5.  コミットまたはトランザクションをロールバックします。

    すべてのリソースの操作が成功した場合、クライアントが呼び出す必要があります[ **ZwCommitTransaction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommittransaction)永続的な操作を作成します。 操作に失敗した場合、クライアントが呼び出す必要があります[ **ZwRollbackTransaction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrollbacktransaction)の代わりに**ZwCommitTransaction**します。 たとえば、書き込み操作が失敗しましたが、一連の 1 つは、認識された、クライアント データベース マネージャーの場合、クライアント呼び出す必要があります**ZwRollbackTransaction**永続的な書き込み操作のいずれになるようにします。

    クライアントが呼び出すことができます**ZwCommitTransaction**と**ZwRollbackTransaction**同期または非同期にします。 クライアントは、これらのルーチンを同期的に呼び出す、コミットまたはロールバック操作が完了するまで、ルーチンは返されません。

    コミットし、トランザクションをロールバックする方法の詳細については、次を参照してください。[トランザクション操作の処理](handling-transaction-operations.md)します。

6.  トランザクション オブジェクトのハンドルを閉じます。

    呼び出す必要がありますが、クライアントは、トランザクションの処理が終了したら、 [ **ZwClose** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntclose)トランザクション オブジェクトのハンドルを終了するには

TP では、1 つ以上のリソース マネージャーを含めることができます。 クライアントのトランザクションには、2 つのリソース マネージャーをサポートする 2 つのデータベースなど、複数のリソースに対する操作が含まれている場合、クライアントが通常は、次に。

1.  トランザクションごとに 1 つのトランザクション オブジェクトを作成します。

2.  各リソース マネージャーには、トランザクション オブジェクトの id を渡します。

3.  各リソース マネージャーのインターフェイスを呼び出すことによって、各データベースでの操作を実行します。

4.  すべての操作が完了したこと、またはエラーが検出された場合は、トランザクションをロールバックする場合は、トランザクションをコミットします。

TP が含まれている場合、*優先的なトランザクション マネージャー*、トランザクションのクライアントが通常 KTM では呼び出しません。 優先的なトランザクション マネージャーとそのクライアントの詳細については、次を参照してください。[上位のトランザクション マネージャーを作成する](creating-a-superior-transaction-manager.md)します。

トランザクションのクライアントが呼び出すことができます[ **ZwSetInformationTransaction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntsetinformationtransaction)トランザクション固有の情報を設定します。 たとえば、クライアントは、トランザクションのタイムアウト値を設定またはわかりやすい文字列を指定します。 クライアントが呼び出すことができます[ **ZwQueryInformationTransaction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntqueryinformationtransaction)トランザクションに関する情報を取得します。 たとえば、クライアントは、トランザクションがコミットまたはロールバックするかどうかを判断するには、このルーチンを呼び出すことができます。

 

 




