---
title: KTM でのログ ストリームの使用
description: KTM でのログ ストリームの使用
ms.assetid: d7ad0e16-d1f2-4c41-b647-95b5445c2708
keywords:
- ログ ストリーム WDK KTM
- カーネル トランザクション マネージャ WDK、ログ ストリーム
- KTM WDK、ログ ストリーム
- 一般的なログ ファイル システムの WDK カーネル、KTM ログ ストリーム
- CLFS WDK カーネル、KTM ログ ストリーム
- WDK の KTM をトランザクションのログ ストリーム
- WDK の KTM のリソース マネージャーのログ ストリーム
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2660cca01196810fd1101b16c4b173f141cb387
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381631"
---
# <a name="using-log-streams-with-ktm"></a>KTM でのログ ストリームの使用


KTM ベースのトランザクション処理 (TPSs) システムはトランザクションのアクティビティを使用してログインする必要があります、 [Common Log File System](using-common-log-file-system.md) (CLFS)。 KTM では、各トランザクション マネージャー オブジェクト用のログ ストリームを作成します。 各 resource manager では、独自のログ ストリームを作成する必要があります。

### <a name="creating-log-streams-for-transaction-manager-objects"></a>トランザクション マネージャー オブジェクト用のログ ストリームの作成

Resource manager を呼び出すと[ **ZwCreateTransactionManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcreatetransactionmanager)、CLFS ログ ストリームの名前を指定する必要があります。 指定したストリームが存在しない場合は、KTM 作成されます。 ストリームが既に存在する場合**ZwCreateTransactionManager**して再度開きます。 KTM では、トランザクション マネージャー オブジェクトをこのログ ストリームを割り当てます。

KTM は、トランザクション マネージャーのオブジェクトとすべてのリソース マネージャーのオブジェクト、トランザクション オブジェクト、およびトランザクション マネージャーのオブジェクトに関連付けられた参加リストのオブジェクトの内部状態情報を記録、トランザクション マネージャー オブジェクトのログ ストリームを使用します. それらが完了する前にトランザクション操作が中断された場合 KTM ことができます、情報を参照してログにコミットするか、トランザクションをロールバックするかどうかを判断します。

KTM では、リソース マネージャーからの受信またはクライアントに送信するトランザクション データは記録されません。 リソース マネージャーは、独自のログ ストリームを使用して、この情報を記録する必要があります。

リソース マネージャーを呼び出すことができます[ **ZwQueryInformationTransactionManager** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntqueryinformationtransactionmanager)ログ ストリームのパス名またはその KTM GUID などのオブジェクトのログ ストリームのトランザクション マネージャーに関する情報を取得するにはストリームに割り当てられます。

### <a name="creating-log-streams-for-resource-managers"></a>リソース マネージャーのログ ストリームの作成

初期化コードで各リソース マネージャーを呼び出す必要があります[ **ClfsCreateLogFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfscreatelogfile)独自のログ ストリームを作成します。 各リソース マネージャーは、そのストリームを使用して、コミット、ロールバック、またはトランザクションのデータを回復するために必要なトランザクションのすべての情報を記録する必要があります。

KTM と、TP のすべてのリソース マネージャーは、単一のログ ファイルを使用できますが、各 TP コンポーネントは、ログ ファイル内で別のストリームを使用する必要があります。 ログ ファイル内の個々 のストリームを指定する方法については、次を参照してください。 [ **ClfsCreateLogFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfscreatelogfile)します。

KTM を定期的に、作成、[再開領域](reading-restart-records-from-a-clfs-stream.md)トランザクション マネージャーのログ ストリームにします。 KTM では、復旧操作を実行する場合は、システムのシャット ダウンする前に開いていたオブジェクトの状態を回復するのには、最後の再開領域を読み取ります。 同様に、リソース マネージャーがそのログ ストリームの再開領域を定期的に作成する必要があります。 たとえば、resource manager 作成再開領域トランザクション操作が完了するたびにします。

CLFS 内の再開領域の詳細についてはログ ストリームを参照してください[CLFS Stream から読み取りを再開レコード](reading-restart-records-from-a-clfs-stream.md)します。 またを参照してください、 [ **ClfsWriteRestartArea**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfswriterestartarea)、 [ **ClfsReadRestartArea**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfsreadrestartarea)、および[ **ClfsReadPreviousRestartArea** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfsreadpreviousrestartarea)ルーチン。

### <a name="using-log-streams-for-recovery"></a>回復のログ ストリームの使用

Resource manager の呼び出し後**ZwCreateTransactionManager**、呼び出す必要があります[ **ZwRecoverTransactionManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrecovertransactionmanager)します。 **ZwRecoverTransactionManager**ルーチンは、トランザクション マネージャーに最適なポイント TP の状態を回復するオブジェクトのログのストリームを読み取ります。 コンピューターが正常にシャット ダウンしている場合、またはシャット ダウンしませんでした: ログ ストリームには後、リソース マネージャーは、最後に読み込まれた、最小限の情報が含まれています。 システムのクラッシュが発生した場合、ログのストリームには、すべてのトランザクションを既知の状態に復元するための十分な回復情報が含まれています。

Resource manager の呼び出し後[ **ZwCreateResourceManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcreateresourcemanager)、呼び出す必要があります[ **ZwRecoverResourceManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrecoverresourcemanager)します。 **ZwRecoverResourceManager**ルーチンは、リソース マネージャーの参加リストのそれぞれに関連付けられているトランザクションを回復しようとしています。 リソース マネージャーのトランザクションを復旧する方法の詳細については、次を参照してください。[回復操作の処理](handling-recovery-operations.md)します。

### <a name="storing-transaction-data"></a>トランザクション データを格納します。

CLFS ログ ストリームを使用するリソース マネージャーがトランザクション データを格納する必要があります[領域をマーシャ リング CLFS](clfs-marshalling-areas.md)します。 CLFS は、ログのストリームからのデータの永続的なストレージ メディアに領域をマーシャ リングを定期的に移動します。 ログイン データを変更する操作は、リソース マネージャーは、次の操作を行います可能性があります。

1.  マーシャ リング領域に書き込み操作を変更し、前に、元のデータをコピーします。

2.  データベースの永続的なストレージ メディアを変更することがなく、データのコピーで、操作を実行します。

3.  新しいデータをマーシャ リング領域にコピーします。

リソース マネージャーは、ロールバック通知を受信する場合は、ログ ストリームから元のデータを復元ができます。 コミット通知を受信した場合、リソース マネージャーにコピーできます、変更されたデータのログ ストリームから、データベースの永続的なストレージ メディア。

リソース マネージャーを使用することも、 [ **ZwSetInformationEnlistment** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntsetinformationenlistment)ルーチンを参加オブジェクトに回復情報を格納します。 KTM では、この情報は、ログ ストリームに保存し、回復操作中にログ ストリームから読み取ります。 リソース マネージャーが呼び出すことによって、いつでもこの回復情報を取得するため、 [ **ZwQueryInformationEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntqueryinformationenlistment)します。

 

 




