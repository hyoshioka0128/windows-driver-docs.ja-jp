---
title: 名前の変更とハード リンクの処理
description: 名前の変更とハード リンクの処理
ms.assetid: 53eb3c9b-cb48-4d5f-8e26-dc93b7607813
keywords:
- WDK ファイル システムのセキュリティ、セマンティック モデルを確認します
- セマンティック モデルは、WDK のファイル システム、名前変更操作を確認します。
- WDK のファイル システム操作の名前を変更します。
- セマンティック モデルは、WDK のファイル システム、ハード リンクの操作を確認します。
- ハード リンク操作 WDK ファイル システム
- WDK の名前のファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 781e954139ec90a2085b75c49b9e27855f6ead1b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553135"
---
# <a name="rename-and-hard-link-processing"></a>名前の変更とハード リンクの処理


## <span id="ddk_rename_and_hard_link_processing_if"></span><span id="DDK_RENAME_AND_HARD_LINK_PROCESSING_IF"></span>


ファイル システムの特定の問題の領域は、名前変更操作の適切な処理です。 問題のような領域は、ハード リンクをサポートするファイル システムのハード リンクの作成です。 名前の変更操作の場合は、ファイル システム、ファイル システムで追加のセキュリティ チェックを必要とするファイル (名前の変更操作のターゲット) を削除する可能性があります。

構造体のフィールドの 1 つは、名前の変更操作の制御構造を調べるときに、 **ReplaceIfExists**オプション。

```cpp
typedef struct _FILE_RENAME_INFORMATION {
    BOOLEAN ReplaceIfExists;
    HANDLE RootDirectory;
    ULONG FileNameLength;
    WCHAR FileName[1];
} FILE_RENAME_INFORMATION, *PFILE_RENAME_INFORMATION;
```

同様に、ハード リンク操作のコントロール構造体で構造体のフィールドのいずれかは、 **ReplaceIfExists**オプション。

```cpp
typedef struct _FILE_LINK_INFORMATION {
    BOOLEAN ReplaceIfExists;
    HANDLE RootDirectory;
    ULONG FileNameLength;
    WCHAR FileName[1];
} FILE_LINK_INFORMATION, *PFILE_LINK_INFORMATION;
```

どちらの場合も、オプションは存在する場合、操作の対象を置き換えるには。 FASTFAT ファイル システムがハード リンクをサポートしていないときに、名前の変更操作をサポートします。 これらのセマンティクスと動作 FASTFAT ファイル システムのソース コード内で認識される、 **FatSetRenameInfo**関数 (を参照してください、 *Fileinfo.c* WDK を含む fastfat サンプルからソース ファイル)。

名前の変更操作を処理するためには、次のコード例では、ファイルを削除するためのファイル システムのチェックを模倣します。 堅牢なセキュリティを備えたファイル システムのモデル (NTFS の例) は、このチェックは、セキュリティ (呼び出し元には、削除に必要な適切なアクセス許可が必要がある)、指定されたファイルを削除する、呼び出し元が許可されていることを確認するチェックも必要です。

```cpp
    //
    //  The name already exists. Check if the user wants
    //  to overwrite the name and has access to do the overwrite.
    //  We cannot overwrite a directory.
    //

    if ((!ReplaceIfExists) ||
        (FlagOn(TargetDirent->Attributes, FAT_DIRENT_ATTR_DIRECTORY)) || 
        (FlagOn(TargetDirent->Attributes, FAT_DIRENT_ATTR_READ_ONLY))) {

        try_return( Status = STATUS_OBJECT_NAME_COLLISION );
    }

    //
    //  Check that the file has no open user handles; otherwise, 
    //  access will be denied. To do the check, search
    //  the list of FCBs opened under the parent Dcb, and make
    //  sure that none of the matching FCBs have a nonzero unclean count or
    //  outstanding image sections.
    //

    for (Links = TargetDcb->Specific.Dcb.ParentDcbQueue.Flink;
            Links != &TargetDcb->Specific.Dcb.ParentDcbQueue; ) {

        TempFcb = CONTAINING_RECORD( Links, FCB, ParentDcbLinks );

        //
        //  Advance now. The image section flush may cause the final
        //  close, which will recursively happen underneath of us here.
        //  It would be unfortunate if we looked through free memory.
        //

        Links = Links->Flink;

        if ((TempFcb->DirentOffsetWithinDirectory == TargetDirentOffset) &&
                ((TempFcb->UncleanCount != 0) ||
                !MmFlushImageSection( &TempFcb->NonPaged->SectionObjectPointers,
                MmFlushForDelete))) {

            //
            //  If there are batch oplocks on this file, then break the
            //  oplocks before failing the rename.
            //

            Status = STATUS_ACCESS_DENIED;

            if ((NodeType(TempFcb) == FAT_NTC_FCB) &&
                    FsRtlCurrentBatchOplock( &TempFcb->Specific.Fcb.Oplock )) {

                //
                //  Do all of the cleanup now since the IrpContext
                //  could go away when this request is posted.
                //

                FatUnpinBcb( IrpContext, TargetDirentBcb );

                Status = FsRtlCheckOplock( &TempFcb->Specific.Fcb.Oplock,
                    Irp,
                    IrpContext,
                    FatOplockComplete,
                    NULL );

                if (Status != STATUS_PENDING) {

                    Status = STATUS_ACCESS_DENIED;
                }
            }

            try_return( NOTHING );
        }
    }

    //
    //  OK, this target is finished. Remember the Lfn offset.
    //

    TargetLfnOffset = TargetDirentOffset -
        FAT_LFN_DIRENTS_NEEDED(&TargetLfn) * sizeof(DIRENT);

    DeleteTarget = TRUE;
}
```

 

 




