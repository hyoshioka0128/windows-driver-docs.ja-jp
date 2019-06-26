---
title: ファイル システム制御処理
description: ファイル システム制御処理
ms.assetid: 95a610c8-b48c-4fff-bf1f-f9fb6abb0fd9
keywords:
- WDK ファイル システムのセキュリティ、セマンティック モデルを確認します
- セマンティック モデルは、WDK のファイル システムを確認しますコントロールの処理。
- FILE_SPECIAL_ACCESS
- FSCTL_MOVE_FILE
- WDK のファイル システムの処理を制御
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2418d48befb37aa9c5c754823a48708b0d971ba9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385549"
---
# <a name="file-system-control-processing"></a>ファイル システム制御処理


## <span id="ddk_file_system_control_processing_if"></span><span id="DDK_FILE_SYSTEM_CONTROL_PROCESSING_IF"></span>


処理、 [ **IRP\_MJ\_ファイル\_システム\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-file-system-control)操作とは異なるその他の操作に必要なデータのバッファー処理ファイル システム。 これは、各操作は、CTL を使用して I/O マネージャーをそのコントロールのコードの一部として、特定のデータ転送メカニズムを確立するため\_コード マクロ。 さらに、コントロールのコードでは、呼び出し元に必要なファイル アクセスを指定します。 ファイル システムはず特にこの問題を理解しているコントロールのコードを定義するときにこのアクセスが I/O マネージャーによって適用されるためです。 いくつかの I/O 制御コード (FSCTL\_移動\_ファイル、たとえば) ファイルを指定\_特殊\_をファイルで操作のセキュリティをチェックすることを示すために、ファイル システムを許可するためのメカニズムのアクセスシステムで直接使用します。 ファイル\_特別な\_アクセスはファイルに数値に相当\_ANY\_I/O マネージャーは、特定のセキュリティ チェックを提供しない代わりに、ファイル システムを保留するようにアクセスします。 ファイル\_特殊\_アクセスは主に、ファイル システムで追加のチェックが行われるドキュメントを提供します。

ファイルを指定するいくつかのファイル システム操作\_特殊\_アクセスします。 FSCTL\_移動\_ファイルの操作はファイル システムの最適化のインターフェイスの一部として使用され、ファイルを指定します\_特殊\_アクセスします。 アクティブにされている開いているファイルの断片化を解消することができるようにするために読み取りし、書き込みハンドルを使用するがファイルのみ\_読み取り\_共有へのアクセスの競合を回避するアクセス許可属性。 ただし、この操作は、特権操作できるように、ディスクは、低レベルで変更されている必要があります。 ソリューションは、ハンドルは、使用、FSCTL を発行することを確認する\_移動\_ファイルが直接アクセス記憶域デバイス (DASD) ユーザー ボリュームを開き、特権のハンドルであります。 オープン ユーザー ボリュームに対して実行が、この操作に確実に FASTFAT ファイル システム コードの中、 **FatMoveFile**関数 (WDK を含む fastfat サンプルから fsctrl.c ソース ファイルを参照してください)。

```cpp
    //
    //  extract and decode the file object and check for type of open
    //

    if (FatDecodeFileObject( IrpSp->FileObject, &Vcb, &FcbOrDcb, &Ccb ) != UserVolumeOpen) {

        FatCompleteRequest( IrpContext, Irp, STATUS_INVALID_PARAMETER );

        DebugTrace(-1, Dbg, "FatMoveFile -> %08lx\n", STATUS_INVALID_PARAMETER);
        return STATUS_INVALID_PARAMETER;
    }
```

FSCTL によって使用される構造\_移動\_ファイル操作が移動されるファイルを指定します。

```cpp
typedef struct {
    HANDLE FileHandle;
    LARGE_INTEGER StartingVcn;
    LARGE_INTEGER StartingLcn;
    ULONG ClusterCount;
} MOVE_FILE_DATA, *PMOVE_FILE_DATA;
```

前述のとおり、FSCTL を発行するためのハンドル\_移動\_ファイルは、ボリューム全体の「開く」の操作、移動で指定したファイル ハンドルに操作が実際に適用される\_ファイル\_データ入力バッファー。 これにより、この操作のセキュリティ チェックが多少複雑にします。 たとえば、このインターフェイスは、移動されるファイルを表すファイル オブジェクトをファイル ハンドルを変換する必要があります。 これには、すべてのドライバーの方を慎重に検討が必要です。 FASTFAT はこれを使用して[ **ObReferenceObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obfreferenceobject)で保護された方法で、 **FatMoveFile** WDK を含む fastfat サンプル fsctrl.c ソース ファイル内の関数。

```cpp
    //
    //  Try to get a pointer to the file object from the handle passed in.
    //

    Status = ObReferenceObjectByHandle( InputBuffer->FileHandle,
                                        0,
                                        *IoFileObjectType,
                                        Irp->RequestorMode,
                                        &FileObject,
                                        NULL );

    if (!NT_SUCCESS(Status)) {

        FatCompleteRequest( IrpContext, Irp, Status );

        DebugTrace(-1, Dbg, "FatMoveFile -> %08lx\n", Status);
        return Status;
    }
    //  Complete the following steps to ensure that this is not an invalid attempt
    //
    //    - check that the file object is opened on the same volume as the
    //      DASD handle used to call this routine.
    //
    //    - extract and decode the file object and check for type of open.
    //
    //    - if this is a directory, verify that it's not the root and that
    //      you are not trying to move the first cluster.  You cannot move the
    //      first cluster because sub-directories have this cluster number
    //      in them and there is no safe way to simultaneously update them
    //      all.
    //
    //  Allow movefile on the root directory if it's FAT32, since the root dir
    //  is a real chained file.
    //    //
```

Irp の使用に注意してください&gt;requestormode でいる場合、呼び出し元を確認するは、ユーザー モード アプリケーション、ハンドルがカーネル ハンドルをすることはできません。 アクティブにアクセスされるときに、ファイルを移動できるように、必要なアクセス権は 0 です。 最後に、呼び出しがユーザー モードで作成された場合は、適切なプロセスのコンテキストで、この呼び出しを行う必要がありますに注意してください。 FASTFAT ファイル システムからソース コードの適用にもこの、 **FatMoveFile** fsctrl.c 関数。

```cpp
    //
    //  Force WAIT to true. There is a handle in the input buffer that can only
    //  be referenced within the originating process.
    //

    SetFlag( IrpContext->Flags, IRP_CONTEXT_FLAG_WAIT );
```

FAT ファイル システムによって実行されるこれらのセマンティックのセキュリティ チェックは、一般的な操作を識別するハンドルを渡すためのファイル システムで必要なものです。 さらに、FAT ファイル システム操作に固有のサニティ チェックを実行する必要があります。 これらのサニティ チェックがさまざまなパラメーターに互換性があることを確認するには (移動されるファイルが開かれたボリューム上) が許可されていないときに、特権操作を実行してから、呼び出し元を防ぐためにします。

正しいセキュリティは、ファイル システムの管理操作の重要な部分に、ファイル システムを含めます。

-   ユーザーのハンドルを適切に検証しています。

-   ユーザー バッファーへのアクセスを保護します。

-   特定の操作のセマンティクスを検証しています。

多くの場合、適切な検証とセキュリティを実行するために必要なコードは、指定された関数内のコードの大部分を構成します。

 

 




