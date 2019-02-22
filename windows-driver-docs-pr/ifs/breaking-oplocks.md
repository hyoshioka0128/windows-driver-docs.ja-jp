---
title: 各 Oplock の解除
description: 各 Oplock の解除
ms.assetid: 1f3c4a99-5ad2-4597-a1c9-a21f80c40291
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79818cd997acc69e0b5ab5cc229faa9b59529ee9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531848"
---
# <a name="breaking-oplocks"></a>各 Oplock の解除


## <span id="ddk_network_redirector_design_and_performance_if"></span><span id="DDK_NETWORK_REDIRECTOR_DESIGN_AND_PERFORMANCE_IF"></span>


Oplock が付与された後にその oplock の所有者は、(要求された oplock の種類に基づく) ストリームにアクセスできます。 受信操作に現在の oplock の互換性がない場合、oplock は解除されます。

Oplock が付与される要求元の IRP が保留にします。 状態で保留 oplock 要求 IRP が完了しました、oplock が切れた場合\_成功します。 レベル 1、バッチ、およびフィルターの各 oplock の**IoStatus.Information** IRP のメンバー、oplock の重大なレベルを示すために設定されます。 これらのレベルは次のとおりです。

-   ファイル\_OPLOCK\_切断\_TO\_なし - oplock が解除され、ストリームの現在の oplock はありません。 Oplock が壊れている"none"と呼ばれます。

-   ファイル\_OPLOCK\_切断\_TO\_レベル\_2 - 現在の oplock (レベル 1 またはバッチ) は、レベル 2 oplock に変換されました。 レベル 2 へのフィルターの各 oplock を解除しないを None に常に中断することに注意してください。

ハンドルの読み取りの読み取り/書き込みと読み取り-書き込みハンドル oplocks、oplock の重大なレベルが 0 個以上の OPLOCK のフラグの組み合わせとして説明されている\_レベル\_キャッシュ\_読み取り、OPLOCK\_レベル\_キャッシュ\_ハンドル、または OPLOCK\_レベル\_キャッシュ\_書き込み、 **NewOplockLevel**メンバー要求の\_OPLOCK\_出力\_として渡されたバッファーの構造、 *lpOutBuffer*パラメーターの[DeviceIoControl](https://go.microsoft.com/fwlink/p/?linkid=124239)します。 同様の方法で[ **FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)と[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)カーネル モードから Windows 7 の各 oplock を要求するために使用できます。 詳細については、次を参照してください。 [ **FSCTL\_要求\_OPLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff545530)します。

フィルター処理、読み取り/書き込み、読み取り、書き込みハンドル、または、特定の状況 (注を参照してください)、読み取りハンドル oplock、IRP の完了、oplock パッケージによって保留 oplock の要求および、oplock を原因となった操作自体では、レベル 1 に、バッチを中断するときに保留 (同期ハンドルでは、上で、操作が発行または IRP が場合\_MJ\_作成で、同期は常に、I/O マネージャーにより、操作の状態を返すのではなく、ブロック、\_PENDING) 待機している、保留操作を続行するには、安全では、その処理が終了したら、oplock のパッケージを指示する、oplock の所有者から受信確認。 この遅延の目的は、現在の操作を続行する前に一貫性のある状態に戻るストリームを格納する、oplock の所有者を許可します。 システムは、タイムアウトが存在しないため、受信確認の受信を永久に待機します。 適切なタイミングで、中断を受け入れますが、oplock の所有者の責任ためです。 保留操作の IRP がキャンセル可能な状態に設定されています。 Oploack パッケージのステータスの IRP がすぐに完了場合は、アプリケーションまたはドライバーが、待機を実行する終了する\_キャンセルします。

IRP\_MJ\_IRP の作成は、ファイルを指定できます\_完了\_場合\_OPLOCKED oplock 中断の受信確認の一部としてブロックされるを防ぐためのオプションを作成します。 このオプションは、oplock の中断の受信確認が受信されるまで作成 IRP のブロックを oplock パッケージを指定します。 代わりに、作成の実行を許可します。 リターン コードは、状態、oplock の場合、正常に作成\_OPLOCK\_BREAK\_IN\_状態ではなく、進行状況\_成功します。 ファイル\_完了\_場合\_OPLOCKED フラグは、通常、デッドロックを回避するために使用します。 たとえば、クライアントにストリームの oplock が所有するいるし、同じストリームを開いて、同じクライアント、クライアントには自体を oplock の承認を待つがブロックします。 このシナリオでは、ファイルの使用\_完了\_場合\_OPLOCKED フラグは、デッドロックを回避できます。

NTFS ファイル システムでは、共有違反をチェックする前にバッチとフィルターの各 oplock の oplock の区切りを開始するため、指定されたファイルを作成する可能性が\_完了\_場合\_OPLOCKEDの状態で失敗するには\_共有\_違反では、中断するバッチまたはフィルター oplock が発生します。 ここでの情報のメンバー、 [ **IO\_状態\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff550671)構造がファイルに設定されている\_OPBATCH\_中断\_このケースを検出するために、呼び出し元を許可するには、進行中です。

ハンドルの読み取りと書き込みハンドルの読み取り oplock の場合は、NTFS をチェックし、共有違反を検出した後、oplock が開始されます。 これにより、そのハンドルを閉じるし、なり、ユーザーに返さない共有違反の可能性を邪魔を取得するこれらの各 oplock 営業案件の所有者です。 また、無条件に oplock を oplock をキャッシュするハンドルは、新規作成と競合しない場合もなくなります。

第 2 のレベルを読み取るときに、特定の状況 (注を参照してください) で読み取りハンドル oplock の中断、システムは受信確認の場合に待機しません。 これは、ことはありませんキャッシュされている状態で他のクライアントへのアクセスを許可する前に、ファイルを復元する必要があるストリームであるためにです。

Oplock を切断する必要があるかどうかを判断する現在の oplock の状態を確認する特定のファイル システム操作があります。 以下のセクションでは、各操作を一覧表示し、oplock 何によってトリガー、どのようにして決まります oplock が区切りレベルと、中断の受信確認が必要かどうかについて説明します。

- [IRP_MJ_CREATE](irp-mj-create2.md)

- [IRP_MJ_READ](irp-mj-read2.md)

- [IRP_MJ_WRITE](irp-mj-write2.md)

- [IRP_MJ_CLEANUP](irp-mj-cleanup2.md)

- [IRP_MJ_LOCK_CONTROL](irp-mj-lock-control2.md)

- [IRP_MJ_SET_INFORMATION](irp-mj-set-information2.md)

- [IRP_MJ_FILE_SYSTEM_CONTROL](irp-mj-file-system-control2.md)

Windows 7 の oplock の中断が場合、受信確認を必要とする要求\_OPLOCK\_出力\_フラグ\_ACK\_必須フラグが設定されて、**フラグ**のメンバー、要求\_OPLOCK\_出力\_の出力パラメーターとして渡されたバッファーの構造体[DeviceIoControl](https://go.microsoft.com/fwlink/p/?linkid=124239)(*lpOutBuffer*)、 [ **FltFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff542988)(*OutBuffer*) または[ **ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)(*OutBuffer*)。 詳細については、次を参照してください。 [ **FSCTL\_要求\_OPLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff545530)します。

**注**  上記の操作を一覧表示と読み取りハンドル oplock の中断がの結果の詳細を説明します。、保留中、oplock を無効にした操作の。 たとえば、 [IRP\_MJ\_作成](irp-mj-create2.md)トピックに関連付けられているハンドルの読み取りの詳細が含まれています。

 

 

 




