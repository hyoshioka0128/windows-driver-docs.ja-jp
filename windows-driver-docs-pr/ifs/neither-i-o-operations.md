---
title: I/O のどちらでもない操作
description: I/O のどちらでもない操作
ms.assetid: c8fc4742-e220-45c4-9113-ec5658bc09cc
keywords:
- WDK ファイル システムのセキュリティ、セマンティック モデルを確認します
- セマンティック モデルは、WDK のファイル システム、どちらの I/O 操作を確認します。
- ファイル システムの I/O の WDK
- どちらの I/O 操作の WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3f6a0c14551cd2232327dd67e42d2c24a678ca7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384809"
---
# <a name="neither-io-operations"></a>I/O のどちらでもない操作


## <span id="ddk_neither_i_o_operations_if"></span><span id="DDK_NEITHER_I_O_OPERATIONS_IF"></span>


ファイル システムでは、通常ユーザー バッファーを直接操作に関連する操作を処理する必要があります。 このような操作は、ユーザーのアドレスが無効になるため、本質的に危険です。 ファイル システムは、このような操作を特に意識し、適切に保護することを確認する必要があります。 次の操作に依存して、**フラグ**I/O マネージャーのユーザーとカーネル アドレス スペース間でデータを転送する方法を指定するファイル システムのデバイス オブジェクトのメンバー。

-   [**IRP\_MJ\_ディレクトリ\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-directory-control)

-   [**IRP\_MJ\_クエリ\_EA**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-ea)

-   [**IRP\_MJ\_クエリ\_クォータ**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-quota)

-   [**IRP\_MJ\_READ**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-read)

-   [**IRP\_MJ\_SET\_EA**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-ea)

-   [**IRP\_MJ\_SET\_QUOTA**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-quota)

-   [**IRP\_MJ\_WRITE**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-write)

通常、ファイル システムがどちらの I/O に暗黙的にどちらの操作を設定して\_直接\_IO も DO\_バッファーに格納された\_で IO、**フラグ**ボリューム デバイスのメンバー オブジェクトを作成します。

次の操作は、無視、**フラグ**ファイル システムのメンバーのデバイス オブジェクトと、どちらの I/O を使用して、ユーザーとカーネル アドレス スペース間でデータを転送します。

-   [**IRP\_MJ\_QUERY\_SECURITY**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-security)

どちらの I/O を使用して、ファイル システムは、独自のデータ転送操作を処理します。 これにより、アプリケーションのユーザー スペースのバッファーにデータを直接配置することで、操作を満たすためにファイル システムです。 ファイル システムは、操作が開始され、操作が進行中に無効になるバッファーを適切に処理、ユーザーのバッファーが有効であることを確認したがって必要があります。 また、高速の I/O には、生のポインターが渡されます。 開発者が認識操作の開始位置のバッファーの有効性のチェックが不十分であることが、操作全体で有効にすることを確認する必要があります。 たとえば、悪意のあるアプリケーションでした (たとえばセクション) から、メモリ ブロックにマップ、発行、I/O 操作および I/O 操作が進行中にメモリ ブロックを解除します。

このような状況を処理するためにファイル システムのいくつかの方法はあります。 1 つのメカニズムはユーザーのアドレスに対応する物理メモリをロックダウンする、オペレーティング システムのアドレス空間に 2 つ目のマッピングを作成します。 これにより、ファイル システムがそれによって制御される仮想アドレスを使用します。 その場合でも、ユーザーのアドレスが無効になると、ファイル システムによって作成されたアドレスは有効のようになります。 FASTFAT のファイル システムのコードでは、これを実現するために 2 つの異なる関数を使用します。 ユーザーのバッファーを最初の関数のロック。

```cpp
VOID
FatLockUserBuffer (
    IN PIRP_CONTEXT IrpContext,
    IN OUT PIRP Irp,
    IN LOCK_OPERATION Operation,
    IN ULONG BufferLength
    )

/*++
Routine Description:

    This routine locks the specified buffer for the specified type of
    access. The file system requires this routine because it does not
    ask the I/O system to lock its buffers for direct I/O. This routine
    can only be called from the file system driver (FSD) while still in the user context.

    Note that this is the *input/output* buffer.

Arguments:
    Irp - Pointer to the Irp for which the buffer will be locked.
    Operation - IoWriteAccess for read operations, or IoReadAccess for
                write operations.
    BufferLength - Length of user buffer.

Return Value:
    None
--*/

{
    PMDL Mdl = NULL;

    if (Irp->MdlAddress == NULL) {
        //
        // Allocate the Mdl and Raise if the allocation fails.
        //
        Mdl = IoAllocateMdl( Irp->UserBuffer, BufferLength, FALSE, FALSE, Irp );
        if (Mdl == NULL) {
            FatRaiseStatus( IrpContext, STATUS_INSUFFICIENT_RESOURCES );
        }

        //
        // now probe the buffer described by the Irp. If there is an exception,
        // deallocate the Mdl and return the appropriate "expected" status.
        //
        try {
            MmProbeAndLockPages( Mdl,
                                 Irp->RequestorMode,
                                 Operation );
        } except(EXCEPTION_EXECUTE_HANDLER) {
            NTSTATUS Status;
            Status = GetExceptionCode();
            IoFreeMdl( Mdl );
            Irp->MdlAddress = NULL;
            FatRaiseStatus( IrpContext,
                            FsRtlIsNtstatusExpected(Status) ? Status : STATUS_INVALID_USER_BUFFER );
        }
    }

    UNREFERENCED_PARAMETER( IrpContext );
}
```

このルーチンにより、ユーザーのアドレスをサポートする物理メモリは再利用できません、他の目的、操作が進行中にようになります。 ファイル システムは、基になるボリューム管理またはディスク クラスのレイヤーにキャッシュされていないユーザー I/O を満たすために、I/O 操作を送信するためにこれを実行します。 このような場合は、ファイル システムにバッファーに独自の仮想アドレスは必要ありません。 2 番目の関数は、カーネルのアドレス空間に、ファイル システムのマッピングを作成します。

```cpp
PVOID
FatMapUserBuffer (
    IN PIRP_CONTEXT IrpContext,
    IN OUT PIRP Irp
    )
/*++
Routine Description:
    This routine conditionally maps the user buffer for the current I/O
    request in the specified mode. If the buffer is already mapped, it
    just returns its address.
 
    Note that this is the *input/output* buffer.

Arguments:
    Irp - Pointer to the Irp for the request.

Return Value:
    Mapped address
--*/
{
    UNREFERENCED_PARAMETER( IrpContext );

    //
    // If there is no Mdl, then we must be in  the FSD, and can simply
    // return the UserBuffer field from the Irp.
    //
    if (Irp->MdlAddress == NULL) {
        return Irp->UserBuffer;
    } else {
        PVOID Address = MmGetSystemAddressForMdlSafe( Irp->MdlAddress, NormalPagePriority );
        if (Address == NULL) {
            ExRaiseStatus( STATUS_INSUFFICIENT_RESOURCES );
        }
        return Address;
    }
}
```

FASTFAT 実装では、FAT ファイル システムは、返されたアドレスは、(ユーザーまたはカーネル) が有効でなければならないことを確認する必要がありますを同様に、ユーザー レベルのアドレスを返す 2 つ目のルーチンを許可します。 これを使用して、 \_\_お試しくださいと\_\_保護されたブロックを作成するためのキーワードを除きます。

これらのルーチンは、WDK を含む fastfat サンプルから deviosup.c ソース ファイルには。

もう 1 つの重要な問題では、呼び出し元のコンテキストでは、要求が満たされていない場合に発生します。 ファイル システムでは、要求、ワーカー スレッドを投稿記事、した場合、ドライバーをことのない見失う MDL バッファーをロックする必要があります。 **FatPrePostIrp** fastfat サンプルから workque.c ソース ファイル内の関数は、FASTFAT ファイル システムでこの問題を処理する方法の例を示します。

FASTFAT ファイル システムは、これらのルーチンを使用して、まで、広範囲のない単に無効なユーザーのバッファーの障害から保護します。 これは、非常に強力な手法でも、すべての保護されたコード ブロックが正しくが保持しているすべてのリソースを解放することを確認が必要です。 リソース解放するにはには、メモリ、同期オブジェクト、またはファイル システム自体の他のリソースが含まれます。 そのためには、障害は、リソースを使い果たしてにオペレーティング システムに多くを繰り返し呼び出すことで、リソースの枯渇を引き起こすことが可能に志望攻撃者になります。

 

 




