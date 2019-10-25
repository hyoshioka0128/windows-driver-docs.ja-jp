---
title: KTM でのログ ストリームの使用
description: KTM でのログ ストリームの使用
ms.assetid: d7ad0e16-d1f2-4c41-b647-95b5445c2708
keywords:
- ログストリーム WDK KTM
- カーネルトランザクションマネージャー WDK、ログストリーム
- KTM WDK、ログストリーム
- WDK カーネル、KTM ログストリームの共通ログファイルシステム
- CLFS WDK カーネル、KTM ログストリーム
- トランザクションマネージャー WDK KTM、ログストリーム
- リソースマネージャー WDK KTM、ログストリーム
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67bd25dc59063e1c1f16739dd1e87e6b24befa12
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835975"
---
# <a name="using-log-streams-with-ktm"></a>KTM でのログ ストリームの使用


KTM ベースのトランザクション処理システム (TPSs) では、[共通ログファイルシステム](using-common-log-file-system.md)(CLFS) を使用してトランザクションアクティビティをログに記録する必要があります。 KTM は、各トランザクションマネージャーオブジェクトのログストリームを作成します。 各リソースマネージャーは、独自のログストリームを作成する必要があります。

### <a name="creating-log-streams-for-transaction-manager-objects"></a>トランザクションマネージャーオブジェクトのログストリームの作成

リソースマネージャーが[**Zwcreatetransactionmanager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreatetransactionmanager)を呼び出す場合、CLFS ログストリームの名前を指定する必要があります。 指定されたストリームが存在しない場合は、KTM によって作成されます。 ストリームが既に存在する場合は、 **Zwcreatetransactionmanager**が再度開きます。 KTM は、このログストリームをトランザクションマネージャーオブジェクトに割り当てます。

KTM は、トランザクションマネージャーオブジェクトのログストリームを使用して、トランザクションマネージャーオブジェクトと、トランザクションマネージャーオブジェクトに関連付けられているすべての resource manager オブジェクト、トランザクションオブジェクト、および参加オブジェクトに関する内部状態情報を記録します. トランザクション操作が完了する前に中断された場合、KTM はログ内の情報を使用して、トランザクションをコミットまたはロールバックするかどうかを判断できます。

KTM では、リソースマネージャーがクライアントとの間で送受信するトランザクションデータは記録されません。 リソースマネージャーは、独自のログストリームを使用して、この情報を記録する必要があります。

リソースマネージャーは、 [**Zwqueryinformationtransactionmanager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntqueryinformationtransactionmanager)を呼び出して、トランザクションマネージャーオブジェクトのログストリームに関する情報を取得できます。たとえば、ログストリームのパス名や、KTM によってストリームに割り当てられた GUID などです。

### <a name="creating-log-streams-for-resource-managers"></a>リソースマネージャーのログストリームの作成

その初期化コードでは、各リソースマネージャーは[**ClfsCreateLogFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfscreatelogfile)を呼び出して独自のログストリームを作成する必要があります。 各リソースマネージャーは、そのストリームを使用して、トランザクションのデータをコミット、ロールバック、または復旧するために必要なトランザクションに関するすべての情報を記録する必要があります。

KTM と TP のすべてのリソースマネージャーは1つのログファイルを使用できますが、各 TPS コンポーネントはログファイル内の別のストリームを使用する必要があります。 ログファイル内の個々のストリームを指定する方法の詳細については、「 [**ClfsCreateLogFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfscreatelogfile)」を参照してください。

KTM では、定期的に、トランザクションマネージャーのログストリームに[再開領域](reading-restart-records-from-a-clfs-stream.md)が作成されます。 KTM が回復操作を実行すると、最後の再起動領域が読み取られ、システムがシャットダウンする前に開いていたオブジェクトの状態が回復されます。 同様に、リソースマネージャーは、ログストリームに再起動領域を定期的に作成する必要があります。 たとえば、トランザクション操作が完了するたびに、リソースマネージャーが再起動領域を作成する場合があります。

CLFS ログストリームの再開領域の詳細については、「 [CLFS ストリームからの再起動レコードの読み取り](reading-restart-records-from-a-clfs-stream.md)」を参照してください。 「 [**ClfsWriteRestartArea**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfswriterestartarea)、 [**ClfsReadRestartArea**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreadrestartarea)、および[**ClfsReadPreviousRestartArea**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreadpreviousrestartarea)ルーチン」も参照してください。

### <a name="using-log-streams-for-recovery"></a>復旧にログストリームを使用する

リソースマネージャーは**Zwcreatetransactionmanager**を呼び出した後、 [**zwの**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecovertransactionmanager)transactionmanager を呼び出す必要があります。 **Zw回復**のルーチンは、トランザクションマネージャーオブジェクトのログストリームを読み取り、tp の状態を既知の良好なポイントに復旧します。 コンピューターが正常にシャットダウンされた場合、またはシャットダウンされなかった場合、リソースマネージャーが最後に読み込まれた後、ログストリームには最小限の情報が含まれます。 システムクラッシュが発生した場合、ログストリームには、すべてのトランザクションを既知の状態に復元するための十分な回復情報が含まれています。

リソースマネージャーは[**Zwcreateresourcemanager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreateresourcemanager)を呼び出した後、 [**Zwの resourcemanager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecoverresourcemanager)を呼び出す必要があります。 **Zw回復マネージャー**ルーチンは、各リソースマネージャーの参加リストに関連付けられているトランザクションを復旧しようとします。 リソースマネージャーのトランザクションを復旧する方法の詳細については、「[復旧操作の処理](handling-recovery-operations.md)」を参照してください。

### <a name="storing-transaction-data"></a>トランザクションデータの格納

CLFS ログストリームを使用するリソースマネージャーでは、トランザクションデータを[CLFS マーシャリング領域](clfs-marshalling-areas.md)に格納する必要があります。 CLFS は、ログストリームのマーシャリング領域から永続的なストレージメディアにデータを定期的に移動します。 データを変更する操作をログに記録するために、リソースマネージャーは次の操作を実行できます。

1.  書き込み操作によって変更される前に、元のデータをマーシャリング領域にコピーします。

2.  データベースの永続的なストレージメディアを変更せずに、データのコピーに対して操作を実行します。

3.  新しいデータをマーシャリング領域にコピーします。

リソースマネージャーは、ロールバック通知を受け取ると、ログストリームから元のデータを復元できます。 コミット通知を受信した場合、リソースマネージャーは、変更されたデータをログストリームからデータベースの永続的なストレージメディアにコピーできます。

リソースマネージャーは、 [**Zwsetinformationenlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntsetinformationenlistment)ルーチンを使用して、回復情報を参加リストオブジェクトに格納することもできます。 KTM は、この情報をログストリームに保存し、復旧操作中にログストリームから読み取ります。 そのため、リソースマネージャーは、 [**Zwqueryinformationenlistment リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntqueryinformationenlistment)を呼び出すことによって、いつでもこの復旧情報を取得できます。

 

 




