---
title: IEEE 1394 バスでの非同期 I/O 要求パケットの送信
description: IEEE 1394 バスでの非同期 I/O 要求パケットの送信
ms.assetid: 93ad0cdf-5ac2-4916-b90e-1e64ca4494b6
keywords:
- 非同期 I/O 要求を送信します。
- raw モードのアドレス指定 WDK IEEE 1394 バス
- 仮想モードのアドレス指定 WDK IEEE 1394 バス
- 通常モードのアドレス指定 WDK IEEE 1394 バス
- WDK の IEEE 1394 をアドレスします。
- データは、WDK の IEEE 1394 をブロックします。
- WDK の IEEE 1394 の連続するデータ ブロックします。
- データの非増分 WDK IEEE 1394 をブロックします。
- WDK の IEEE 1394 をバッファー処理します。
- バスのリセット WDK IEEE 1394 の生成
- WDK の IEEE 1394 の生成をリセットします。
- WDK の IEEE 1394 をロック
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3241353282dac50fefebbc983cc932d2244c3384
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381038"
---
# <a name="sending-asynchronous-io-request-packets-on-the-ieee-1394-bus"></a>IEEE 1394 バスでの非同期 I/O 要求パケットの送信





ドライバーが要求を使用して\_ASYNC\_読み取り、要求\_ASYNC\_書き込み、および要求\_ASYNC\_ロック非同期送信を読み取り、書き込み、および IEEE 1394 バス上のデバイスに操作をロックします。 要求の\_ASYNC\_読み取りおよび要求\_ASYNC\_書き込み、いずれかで、IRB の操作に固有のパラメーターが格納されている**u.AsyncRead**または**u.AsyncWrite** IRB のメンバー。

### <a name="types-of-addressing"></a>種類のアドレス指定

非同期 I/O 要求を作成するドライバーは、型の変換先のアドレスを指定する必要があります[ **IO\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/1394/ns-1394-_io_address)で、 **DestinationAddress** IRB のメンバー。 送信先アドレスは、2 つの値で構成されています。 ノードのアドレスとアドレスのオフセット。 バス ドライバーは、これら 2 つの値を解釈は、要求を開始するドライバーによって使用されるアドレス指定のモードによって異なります。

アドレス指定の 3 つのモードが非同期 1394 パケットを送信できる:*通常*、*生*、および*仮想*します。

通常モードへの対処には、要求を開始するドライバーは、アドレスのオフセットを提供しますが、ターゲット デバイスのノードのアドレスを指定しません。 バス ドライバーは、デバイスが列挙されるとき、デバイスの PDO に保存しておいた情報を使用して、ノードのアドレスに格納します。

Raw モードでアドレス指定、ノードのアドレスとアドレスのオフセットの両方には、要求を開始するドライバーが提供する必要があります。 さらに、ターゲット デバイスの PDO を要求を送信する代わりに、ドライバーする必要がありますに要求を送信ホスト コント ローラーの PDO します。 パケット内のノードのアドレス情報を上書きする必要があります、バス ドライバーに通知されます。

仮想モードのアドレス指定のドライバーが要求を開始する必要があります明示的にノードのアドレスを示します、パケット内のターゲット デバイスへの対応の raw モードと同様。 ただし、仮想デバイスでは、1394 バスの実際のノード アドレスは必要はありません。 仮想デバイスのノード アドレスは、そのパケットを識別するために仮想デバイスのドライバーを許可する規則を確立する値だけです。 仮想デバイス ドライバーがバスには、ブロードキャストし、それらを調べているすべてのパケットを受信する必要があります、適切に動作するときにそのデバイスの「ノード アドレス」されて値が含まれるパケットの検索

仮想デバイスの要求を開始するドライバーは、バス ドライバーがパケットに記録されているノードのアドレスを上書きするを防ぐために特別な手順を実行する必要はありません。 バス ドライバーは、まず、仮想デバイスを列挙する場合、デバイスの拡張機能にデバイスの PDO をデバイスが仮想であることを示すフラグを設定します。 このデバイスの要求を受信するには、バス ドライバーは仮想デバイスであり、パケット内のノード アドレスを上書きしないことを確認できます。

### <a name="buffering-of-io-requests"></a>I/O 要求のバッファリング

非同期の I/O 要求を開始するドライバーでは、I/O バッファーを指定する、MDL にポインターを提供する必要があります。 このポインターに入れ、 **Mdl** IRB のメンバー。 バス ドライバーでは、このバッファーを使用して、そこに、デバイスまたはデバイスに書き込むデータのソースとしてデータをコピーします。

ドライバーのデータ バッファーのサイズを指定する、 **nNumberOfBytesToRead**または**nNumberOfBytesToWrite**のメンバー **u.AsyncXXX**、およびブロック サイズ、 **nBlockSize**メンバー。 実際に行われると、トランザクション、バス ドライバー改で指定されたサイズのパケットにデータを**nBlockSize**します。 既定では、バス ドライバーが読み取り、またはデータを連続的に書き込みます: 各ブロックを読み取りまたはデバイスのアドレス空間内の連続した場所に書き込まれます。

次の図は、連続するデータ ブロックを示します。

![連続するデータ ブロックを示す図](images/1394blkd.png)

必要に応じて、ドライバーは、ASYNC を指定できます\_フラグ\_NONINCREMENTING にフラグを要求は、バス ドライバーが各ブロックのアドレスの同じセットを使用します。

次の図は、非同期の非増分データ ブロックを示します。

![非同期の非増分データ ブロックを示す図](images/1394blkf.png)

**警告**  バス ドライバーは、現在の接続速度、デバイスとコンピューター間の非同期パケットの最大サイズを適用し、最高速度、デバイスは、最大でレポート\_の推奨値フィールド、ROM. の構成 場合**nBlockSize**がいずれかのよりも大きい、これらの値、バス ドライバーはブロック サイズの強制の値を使用します。 場合は、ドライバーの設定、ASYNC\_フラグ\_NONINCREMENTING フラグ、これが目的の動作を提供する可能性があります。 ドライバーは、このフラグが設定された場合、は、ブロック サイズは、要求を送信する前に適用される制限よりも小さいことを確認する必要があります。

 

### <a name="sending-lock-requests"></a>ロック要求を送信します。

IEEE 1394 のバス プロトコルでは、アトミック、テストとセットの種類の操作を許可する非同期ロック要求を提供します。 送信先アドレスを指定するだけでなく (で**u.AsyncLock.DestinationAddress**)、ドライバーがトランザクションの種類を指定します (で**u.AsyncLock.fulTransactionType**)。 データ値と、操作の引数の値が渡されますが (詳細については、IEEE 1394 の仕様を参照してください) **u.AsyncLock.DataValues**と**u.AsyncLock.Arguments**します。

### <a name="bus-reset-generation"></a>バスのリセットの生成

非同期 I/O を使用するデバイス ドライバーは、バスのリセットの生成を追跡します。 内でその値を報告するデバイス ドライバー、非同期要求ごとに、 **u.AsyncXxx.ulGeneration**要求の IRB のメンバー。 バス ドライバーが、実際に生成数にその値を比較し、状態のステータス値を持つ要求は失敗しますが、一致するように失敗した場合\_無効な\_生成します。 要求は、この方法で失敗すると場合、でも、ドライバーは、要求を使用して正しい生成にクエリする必要があります\_取得\_生成\_bus 要求の数。 ただし、ドライバーは、新世代で、バスのリセット通知コールバックを取得するまでこの状態で失敗したすべての要求を再実行する必要がありますいないします。 これにより、デバイスがバスにまだ存在します。 クライアント ドライバーが IRP に依存する必要がありますしないことに注意してください\_MN\_BUS\_バスのリセットの通知をリセットします。 IRP\_MN\_BUS\_リセットは Windows XP 以降のオペレーティング システムで廃止されています。

 

 




