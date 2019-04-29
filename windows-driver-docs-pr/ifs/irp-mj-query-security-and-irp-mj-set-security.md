---
title: IRP_MJ_QUERY_SECURITY と IRP_MJ_SET_SECURITY
description: IRP_MJ_QUERY_SECURITY と IRP_MJ_SET_SECURITY
ms.assetid: 64216496-55f0-4ad4-b475-341ed9eb6886
keywords:
- IRP_MJ_QUERY_SECURITY
- IRP_MJ_SET_SECURITY
- セキュリティ WDK ファイル システム、セキュリティ チェックを追加します。
- セキュリティは、WDK のファイル システム、IRP_MJ_SET_SECURITY を確認します。
- セキュリティは、WDK のファイル システム、IRP_MJ_QUERY_SECURITY を確認します。
- WDK のセキュリティ記述子、ファイル システムのセキュリティ チェック
- WDK の記述子ファイル システム、セキュリティ チェック
- セキュリティ記述子を取得します。
- セキュリティ記述子のクエリを実行します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f97cf8905c6699ceaaad773ee83d78f28c934b88
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324480"
---
# <a name="irpmjquerysecurity-and-irpmjsetsecurity"></a>IRP\_MJ\_クエリ\_セキュリティと IRP\_MJ\_設定\_セキュリティ


さいわいなことに、ファイル システムのセキュリティ記述子の取得と実際のストレージは比較的不透明です。 これは、ファイル システムで、記述子の理解を必要としない自己相対形式のセキュリティ記述子の性質です。 したがって、クエリ操作の処理は、非常に単純な演習では通常です。 ファイル システムの実装の例を次に示します。

```cpp
NTSTATUS FsdCommonQuerySecurity( PIRP_CONTEXT IrpContext)
{
    NTSTATUS status = STATUS_SUCCESS;
    PSECURITY_DESCRIPTOR LocalPointer;

    // Need to add code to lock the FCB here

    status = FsdLoadSecurityDescriptor(IrpContext, IrpContext->Fcb);
 
    if (NT_SUCCESS(status) ) {
 
        //
        // copy the SecurityDescriptor into the callers buffer
        // note that this copy can throw an exception that must be handled
        // (code to handle the exception was omitted here for brevity)
        //
        LocalPointer = IrpContext->Fcb->SecurityDescriptor;

        status = SeQuerySecurityDescriptorInfo(
     &IrpContext->IrpSp->Parameters.QuerySecurity.SecurityInformation,
            (PSECURITY_DESCRIPTOR)IrpContext->Irp->UserBuffer,
            &IrpContext->IrpSp->Parameters.QuerySecurity.Length,
            &LocalPointer );
 
        //
        // CACLS utility expects OVERFLOW
        //
        if (status == STATUS_BUFFER_TOO_SMALL ) {
            status = STATUS_BUFFER_OVERFLOW;
        }
    }
 
    // Need to add code to unlock the FCB here

    return status;
}
```

このルーチンは、実際のセキュリティ記述子を (この実装では、既に読み込まれていない場合、ルーチンがそのセキュリティ記述子をのみ読み込むこと) の永続的な記憶域から読み込む外部関数に依存しているに注意してください。 セキュリティ記述子は、ファイル システムに対して非透過的であるために、セキュリティ参照モニターは、記述子をユーザーのバッファーにコピーするために使用する必要があります。 ここには、このコード サンプルに関して 2 つの点に注意してください。

1.  エラー コードの状態の変換\_バッファー\_すぎます\_警告コードの状態に小さな\_バッファー\_オーバーフローがいくつかの Windows セキュリティ ツールの正しい動作を提供するために必要な。

2.  両方のクエリし、セキュリティ操作のセットが通常行いますので、バッファーには、ユーザーとは、処理でエラーが発生するユーザーのバッファーを直接使用します。 このによって管理されている、**フラグ**デバイスのメンバー\_ファイル システムによって作成されたオブジェクト。 このコードに基づくファイル システムの実装、呼び出し元の関数を使用する必要は、 \_\_無効なユーザー バッファーから保護するためのブロックを実行してください。

ファイル システムがストレージからセキュリティ記述子を読み込む方法の詳細 (、 **FsdLoadSecurityDescriptor**この例では関数)、ファイル システムのセキュリティ記述子のストレージの実装に完全に異なります。

セキュリティ記述子を格納するは、少し複雑です。 ファイル システムは、セキュリティ記述子では、ファイル システムは、セキュリティ記述子の共有をサポートしている場合に、既存のセキュリティ記述子が一致するかどうかを判断する必要があります。 セキュリティ記述子の一致しないファイル システムは、この新しいセキュリティ記述子の新しい記憶域を割り当てる必要があります。 ファイルのセキュリティ記述子を置換するためのルーチンの例を次に示します。

```cpp
NTSTATUS FsdCommonSetSecurity(PIRP_CONTEXT IrpContext)
{
    NTSTATUS status = STATUS_SUCCESS;
    PSECURITY_DESCRIPTOR SavedDescriptorPtr = 
        IrpContext->Fcb->SecurityDescriptor;
    ULONG SavedDescriptorLength = 
        IrpContext->Fcb->SecurityDescriptorLength;
    PSECURITY_DESCRIPTOR newSD = NULL;
    POW_FCB Fcb = IrpContext->Fcb;
    ULONG Information = IrpContext->Irp->IoStatus.Information;

    //
    // make sure that the FCB security descriptor is up to date
    //
    status = FsdLoadSecurityDescriptor(IrpContext, Fcb);

    if (!NT_SUCCESS(status)) {
      //
      // Something is seriously wrong 
      //
      IrpContext->Irp->IoStatus.Status = status;
      IrpContext->Irp->IoStatus.Information = 0;
      return status;
    }        
 
    status = SeSetSecurityDescriptorInfo(
       NULL,
       &IrpContext->IrpSp->Parameters.SetSecurity.SecurityInformation,
       IrpContext->IrpSp->Parameters.SetSecurity.SecurityDescriptor,
       &Fcb->SecurityDescriptor,
       PagedPool,
       IoGetFileObjectGenericMapping()
       );

    if (!NT_SUCCESS(status)) {

        //
        // restore things  and return
        //
        Fcb->SecurityDescriptorLength = SavedDescriptorLength;
        Fcb->SecurityDescriptor = SavedDescriptorPtr;
        IrpContext->Irp->IoStatus.Status = status;
        IrpContext->Irp->IoStatus.Information = 0;

        return status;
    }

    //
    // get the new length
    //
    Fcb->SecurityDescriptorLength = 
        RtlLengthSecurityDescriptor(Fcb->SecurityDescriptor);

    //
    // allocate our own private SD to replace the one from
    // SeSetSecurityDescriptorInfo so we can track our memory usage
    //
    newSD = ExAllocatePoolWithTag(PagedPool, 
        Fcb->SecurityDescriptorLength, 'DSyM');

    if (!newSD) {
 
      //
      // paged pool is empty
      //
      SeDeassignSecurity(&Fcb->SecurityDescriptor);
      status = STATUS_NO_MEMORY;
      Fcb->SecurityDescriptorLength = SavedDescriptorLength;
      Fcb->SecurityDescriptor = SavedDescriptorPtr;
 
      //
      // make sure FCB security is in a valid state
      //
      IrpContext->Irp->IoStatus.Status = status;
      IrpContext->Irp->IoStatus.Information = 0;
 
      return status;
 
    } 
 
    //
    // store the new security on disk
    //
    status = FsdStoreSecurityDescriptor(IrpContext, Fcb);

    if (!NT_SUCCESS(status)) {
      //
      // great- modified the in-core SD but couldn't get it out
      // to disk. undo everything. 
      //
      ExFreePool(newSD);
      SeDeassignSecurity(&Fcb->SecurityDescriptor);
      status = STATUS_NO_MEMORY;
      Fcb->SecurityDescriptorLength = SavedDescriptorLength;
      Fcb->SecurityDescriptor = SavedDescriptorPtr;
      IrpContext->Irp->IoStatus.Status = status;
      IrpContext->Irp->IoStatus.Information = 0;
 
      return status;
    }
 
    //
    // if we get here everything worked! 
    //
    RtlCopyMemory(newSD, Fcb->SecurityDescriptor, 
        Fcb->SecurityDescriptorLength);
 
    //
    // deallocate the security descriptor
    //
    SeDeassignSecurity(&Fcb->SecurityDescriptor);
 
    //
    // this either is the new private SD or NULL if 
    // memory allocation failed
    //
    Fcb->SecurityDescriptor = newSD;

    //
    // free the memory from the previous descriptor
    //
    if (SavedDescriptorPtr) {
      //
      // this  must always be from private allocation
      //
      ExFreePool(SavedDescriptorPtr);
 
    }        
 
    IrpContext->Irp.IoStatus = status;
    IrpContext->Irp.Information = Information;

    return status;
}
```

これは、実装内の領域がファイル システムにファイル システムからと大幅に異なります。 たとえば、セキュリティ記述子の共有をサポートするファイル システムは一致するセキュリティ記述子を検索する明示的なロジックを追加する必要があります。 このサンプルは、実装ガイダンスを提供する試みのみです。

 

 




