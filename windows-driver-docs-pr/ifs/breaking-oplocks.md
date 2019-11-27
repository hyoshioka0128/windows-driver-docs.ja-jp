---
title: Oplock の破損
description: Oplock の破損
ms.assetid: 1f3c4a99-5ad2-4597-a1c9-a21f80c40291
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be10a1b3a47d9296b7e8937af665654246f778e2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841482"
---
# <a name="breaking-oplocks"></a>Oplock の破損


## <span id="ddk_network_redirector_design_and_performance_if"></span><span id="DDK_NETWORK_REDIRECTOR_DESIGN_AND_PERFORMANCE_IF"></span>


Oplock が付与されると、その oplock の所有者は、要求された oplock の種類に基づいて、ストリームにアクセスできるようになります。 受信した操作が現在の oplock と互換性がない場合、oplock は解除されます。

Oplock が付与されると、要求元の IRP は保留されます。 Oplock が解除されると、保留中の oplock 要求の IRP は状態\_SUCCESS で完了します。 レベル1、バッチ、およびフィルターについては、の Iostatus を適用し**ます。** IRP の情報メンバーは、oplock が中断されているレベルを示すように設定されます。 これらのレベルは次のとおりです。

-   ファイル\_OPLOCK\_破損している\_を\_NONE-oplock が解除され、ストリームに現在の oplock がありません。 Oplock は "None に破損しています" と言います。

-   ファイル\_OPLOCK\_\_レベル\_2 に\_破損しています。現在の oplock (レベル1またはバッチ) はレベル2の oplock に変換されました。 フィルターの oplock がレベル2になることはないことに注意してください。これは常に [なし] になります。

読み取りハンドル、読み取り/書き込み、および読み取り/書き込みハンドルの oplock は、oplock を解除するレベルを、0個以上のフラグ OPLOCK の組み合わせとして記述されます\_レベル\_キャッシュ\_読み取り、OPLOCK\_レベル\_キャッシュ\_ハンドル、または OPLOCK\_レベル\_キャッシュ\_要求の DeviceIoControl の*Lpoutbuffer*パラメーターとして渡さ**れたバッファー**構造を書き込み\_ます。 [](https://go.microsoft.com/fwlink/p/?linkid=124239).\_\_ 同様の方法で、 [**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)と[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)を使用して、カーネルモードから Windows 7 の oplock を要求できます。 詳細については、「 [**FSCTL\_REQUEST\_OPLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-request-oplock)」を参照してください。

レベル1、バッチ、フィルター、読み取り/書き込み、読み取り/書き込みハンドル、または特定の状況下で (注を参照)、読み取りハンドルの oplock を解除すると、oplock パッケージによって保留中の oplock 要求 IRP が完了し、oplock の原因となった操作が実行されます。保留 (操作が同期ハンドルに対して実行される場合、または同期ハンドルに対して実行される場合は、IRP\_MJ\_CREATE (常に同期される) であることに注意してください。 i/o マネージャーによって操作がブロックされます。返される状態\_PENDING)は、oplock の所有者からの受信確認を待機して、処理が完了したことを oplock パッケージに伝えます。また、保留中の操作を続行することも安全です。 この遅延の目的は、oplock の所有者が、現在の操作を続行する前にストリームを一貫性のある状態に戻すことができるようにすることです。 タイムアウトがないため、システムは無期限に受信確認を受信します。 そのため、oplock の所有者は、適切なタイミングで中断を確認する必要があります。 保留中の操作の IRP は、キャンセル可能な状態に設定されます。 待機を実行しているアプリケーションまたはドライバーが終了した場合、o/the IRP は状態\_取り消された状態で直ちに完了します。

IRP\_MJ\_CREATE IRP では、oplock 解除確認の一部としてブロックされないように\_OPLOCKED create オプションを指定すると、ファイル\_\_完了するように指定できます。 このオプションは、oplock 解除の受信確認が受信されるまで、create IRP をブロックしないように oplock パッケージに指示します。 代わりに、作成を続行できます。 作成が成功した場合、oplock ブレークが発生すると、ステータス\_SUCCESS ではなく\_の進行状況で\_中断\_\_OPLOCK が返されます。 \_OPLOCKED フラグがデッドロックを回避するために通常使用される場合は、ファイル\_完了\_ます。 たとえば、クライアントがストリームで oplock を所有していて、同じクライアントが同じストリームを開いた場合、クライアントは、それ自体が oplock の中断を確認するのを待機してブロックします。 このシナリオでは、\_OPLOCKED フラグによってデッドロックが回避される場合、ファイル\_\_を使用します。

NTFS ファイルシステムは、共有違反を確認する前に、バッチとフィルターの oplock に対して oplock の解除を開始するため、指定されたファイル\_が\_完了したとしても、\_OPLOCKED が状態\_共有に失敗する可能性があり\_違反が発生しても、バッチまたはフィルターの oplock は中断されます。 この場合は、 [**IO\_STATUS\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造体の情報メンバーが FILE\_opbatch\_BREAK\_実行中に設定され、呼び出し元がこのケースを検出できるようになります。

読み取りハンドルと読み取り/書き込みハンドルの oplock の場合、共有違反を検出して検出すると、oplock の解除が開始されます。 これにより、これらの oplock を解除してハンドルを終了し、ユーザーに共有違反を返すことができないようにする機会が与えられます。 また、oplock によってキャッシュされたハンドルが新しい create と競合しない場合に、無条件で oplock が解除されるのを回避できます。

レベル2、読み取り、および、特定の状況下 (注を参照)、読み取りハンドル oplock 解除、システムは受信確認を待機しません。 これは、他のクライアントからのアクセスを許可する前に、ファイルに復元する必要があるストリームには、キャッシュされた状態がないためです。

現在の oplock 状態をチェックして oplock を解除する必要があるかどうかを判断する、特定のファイルシステム操作があります。 次のセクションでは、各操作の一覧を示し、oplock 解除のトリガー、oplock が中断されるレベルを決定する方法、および中断の確認が必要かどうかについて説明します。

- [IRP_MJ_CREATE](irp-mj-create2.md)

- [IRP_MJ_READ](irp-mj-read2.md)

- [IRP_MJ_WRITE](irp-mj-write2.md)

- [IRP_MJ_CLEANUP](irp-mj-cleanup2.md)

- [IRP_MJ_LOCK_CONTROL](irp-mj-lock-control2.md)

- [IRP_MJ_SET_INFORMATION](irp-mj-set-information2.md)

- [IRP_MJ_FILE_SYSTEM_CONTROL](irp-mj-file-system-control2.md)

Windows 7 の oplock を解除するには、要求の**Flags**メンバーで\_出力\_フラグ\_ACK\_必要なフラグが設定されている場合は、受信確認が必要\_要求\_OPLOCK\_出力\_バッファー[DeviceIoControl](https://go.microsoft.com/fwlink/p/?linkid=124239)(*Lpoutbuffer*)、 [**fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)(*Outbuffer*)、または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)(*outbuffer*) の出力パラメーターとして渡された構造体。 詳細については、「 [**FSCTL\_REQUEST\_OPLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-request-oplock)」を参照してください。

ここに示されている操作ごとのトピックでは、読み取りハンドルの oplock が解除されたときに、oplock を壊す操作が保留になった場合の詳細について説明し**て  ます**。 たとえば、 [IRP\_MJ\_CREATE](irp-mj-create2.md)トピックには、関連付けられている読み取りハンドルの詳細が含まれています。

 

 

 




