---
title: ファイル システム制御処理
description: ファイル システム制御処理
ms.assetid: 95a610c8-b48c-4fff-bf1f-f9fb6abb0fd9
keywords:
- セキュリティ WDK ファイルシステム、セマンティックモデルチェック
- セマンティックモデルでは、WDK ファイルシステム、制御処理をチェックします。
- FILE_SPECIAL_ACCESS
- FSCTL_MOVE_FILE
- WDK ファイルシステムの処理の制御
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4423eb0804942870ffcbadbabbbd56b093f8563d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841410"
---
# <a name="file-system-control-processing"></a>ファイル システム制御処理


## <span id="ddk_file_system_control_processing_if"></span><span id="DDK_FILE_SYSTEM_CONTROL_PROCESSING_IF"></span>


[**IRP\_MJ\_ファイル\_システム\_制御**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-file-system-control)操作は、ファイルシステム内の他の操作に必要なデータバッファー処理とは異なります。 これは、各操作によって、CTL\_コードマクロを使用して制御コードの一部として、i/o マネージャーに固有のデータ転送機構が確立されるためです。 また、コントロールコードでは、呼び出し元に必要なファイルアクセスを指定します。 このアクセスは i/o マネージャーによって適用されるため、コントロールコードを定義するときは、ファイルシステムが特にこの問題を cognizant する必要があります。 一部の i/o 制御コード (FSCTL\_MOVE\_ファイルなど) では、ファイル\_特別な\_アクセスを指定します。これは、ファイルシステムによって操作のセキュリティがファイルシステムによって直接チェックされることをファイルシステムが示すことを許可するメカニズムです。 ファイル\_特別な\_アクセスは、ファイル\_すべての\_アクセスに相当します。そのため、i/o マネージャーでは特定のセキュリティチェックが行われず、ファイルシステムではなく遅延されます。 ファイル\_特別な\_アクセスは、主に、ファイルシステムによって追加のチェックが行われるドキュメントを提供します。

いくつかのファイルシステム操作では、ファイル\_特別な\_アクセスが指定されています。 FSCTL\_MOVE\_FILE 操作は、ファイルシステムの最適化インターフェイスの一部として使用され、ファイル\_特別な\_アクセスを指定します。 読み取りと書き込みが行われている開いているファイルを最適化できるようにするため、使用するハンドルには、共有アクセスの競合を防ぐためにアクセスを許可されたファイル\_読み取り\_属性のみがあります。 ただし、ディスクが低いレベルで変更されているため、この操作は特権操作である必要があります。 この問題を解決するには、FSCTL\_MOVE\_ファイルの発行に使用されるハンドルが、特権ハンドルであるダイレクトアクセスストレージデバイス (DASD) ユーザーボリュームを開いていることを確認します。 開いているユーザーボリュームに対してこの操作が実行されていることを確認する FASTFAT ファイルシステムコードは、 **FatMoveFile**関数にあります (WDK に含まれる FASTFAT サンプルの fsctrl ソースファイルを参照してください)。

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

FSCTL\_MOVE\_FILE 操作で使用される構造体は、移動するファイルを指定します。

```cpp
typedef struct {
    HANDLE FileHandle;
    LARGE_INTEGER StartingVcn;
    LARGE_INTEGER StartingLcn;
    ULONG ClusterCount;
} MOVE_FILE_DATA, *PMOVE_FILE_DATA;
```

前述のように、FSCTL\_MOVE\_ファイルを発行するために使用されるハンドルはボリューム全体の "オープン" 操作であり、実際には、移動\_ファイル\_データ入力バッファーに指定されたファイルハンドルに適用されます。 これにより、この操作のセキュリティチェックがやや複雑になります。 たとえば、このインターフェイスでは、ファイルハンドルを移動するファイルを表すファイルオブジェクトに変換する必要があります。 これには、ドライバーの一部を慎重に検討する必要があります。 FASTFAT は、WDK に含まれる FASTFAT サンプルの fsctrl ソースファイルの**FatMoveFile**関数で、保護された方法で[**obreferenceobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject)を使用します。

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

Irp&gt;Irp->requestormode を使用して、呼び出し元がユーザーモードアプリケーションである場合、ハンドルをカーネルハンドルにすることはできません。 ファイルがアクティブにアクセスされている間に移動できるように、必要なアクセス権は0です。 最後に、呼び出しがユーザーモードで開始された場合、この呼び出しは正しいプロセスコンテキストで行う必要があることに注意してください。 FASTFAT ファイルシステムのソースコードでは、fsctrl の**FatMoveFile**関数にもこれが適用されます。

```cpp
    //
    //  Force WAIT to true. There is a handle in the input buffer that can only
    //  be referenced within the originating process.
    //

    SetFlag( IrpContext->Flags, IRP_CONTEXT_FLAG_WAIT );
```

FAT ファイルシステムによって実行されるこれらのセマンティックセキュリティチェックは、ハンドルを渡すすべての操作について、ファイルシステムによって必要とされる一般的なものです。 また、FAT ファイルシステムも、操作に固有の正常性チェックを実行する必要があります。 これらの正常性チェックでは、呼び出し元が許可されていない場合に特権操作を実行しないようにするために、異なるパラメーターに互換性があることを確認します (移動するファイルは、開かれたボリューム上にあります)。

ファイルシステムによっては、次のようなファイルシステム制御操作において適切なセキュリティが不可欠です。

-   ユーザーハンドルを適切に検証します。

-   ユーザーバッファーアクセスの保護。

-   特定の操作のセマンティクスを検証しています。

多くの場合、適切な検証とセキュリティを実行するために必要なコードは、指定された関数内のコードの大部分を構成することができます。

 

 




