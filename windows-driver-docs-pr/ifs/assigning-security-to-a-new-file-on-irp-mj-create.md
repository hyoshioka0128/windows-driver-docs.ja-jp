---
title: IRP_MJ_CREATE での新規ファイルへのセキュリティの割り当て
description: IRP_MJ_CREATE での新規ファイルへのセキュリティの割り当て
ms.assetid: f01a09c4-f71f-4b9e-99c8-9bc7ca5ca316
keywords:
- IRP_MJ_CREATE
- 新しいファイルのセキュリティ WDK ファイル システム
- セキュリティは、WDK のファイル システム、irp_mj_create 用を確認します。
- WDK のセキュリティ記述子をファイル システムでは、新しいファイルします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9d9b60374ee4c7f214f8bfc887b7e1c5f316c74
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350271"
---
# <a name="assigning-security-to-a-new-file-on-irpmjcreate"></a>IRP 上の新しいファイルへのセキュリティの割り当て\_MJ\_を作成します。


## <span id="ddk_assigning_security_to_a_new_file_on_irp_mj_create_if"></span><span id="DDK_ASSIGNING_SECURITY_TO_A_NEW_FILE_ON_IRP_MJ_CREATE_IF"></span>


最後のタスクの作成処理は、新しいファイルにセキュリティを割り当てることができます。 Windows のセキュリティ モデルは、継承をサポートしています (個々 の ACE のエントリがこのような方法でマークされている新しいファイルまたはディレクトリが作成されたときに継承されること) これは、ファイル システムの外部に実装します。 そのため、ファイル システム内のロジックの大部分は、新しいセキュリティ記述子を格納する専用です。 ルーチンの例を次に示します。

```cpp
NTSTATUS FsdAssignInitialSecurity( PIRP_CONTEXT IrpContext, 
        PFCB Fcb, PFCB Directory)
{
    NTSTATUS status = STATUS_SUCCESS;
    BOOLEAN CreateDir = ((IrpContext->IrpSp->Parameters.Create.Options
        & FILE_DIRECTORY_FILE)==FILE_DIRECTORY_FILE);
    PACCESS_STATE AccessState = 
    IrpContext->IrpSp->Parameters.Create.SecurityContext->AccessState;
    PSECURITY_DESCRIPTOR SecurityDescriptor = NULL;

    //
    // Make sure the parent directory's security descriptor is loaded.
    //
    (void) FsdLoadSecurityDescriptor(IrpContext, Directory);

    //
    // don't care about the return code here, as it is handled later
    //
    if (Directory->SecurityDescriptor == NULL) {

        //
        // If the parent has no security, then we are outside
        // of the normal Windows paradigm.
        //
        // The child (that is, the target of the create) will also have
        // a NULL SD.
        //
        // Note that you can always assign security to the file object 
        // explicitly at later on.
        //
        return STATUS_SUCCESS;

    }

    //
    // Now create the security descriptor.
    //
    status = SeAssignSecurity(Directory->SecurityDescriptor, 
                              AccessState->SecurityDescriptor,
                              &SecurityDescriptor, 
                              CreateDir, 
                              &AccessState->SubjectSecurityContext,
                              IoGetFileObjectGenericMapping(),
                              PagedPool);

    if (!NT_SUCCESS(status)) {

        return status;
    }

    //
    // Associate the SD with the file; use our own storage so when 
    // cleanup occurs it is unnecessary to know if the storage came from the 
    // security reference monitor.
     //
    Fcb->SecurityDescriptorLength = 
        RtlLengthSecurityDescriptor( SecurityDescriptor );
 
    Fcb->SecurityDescriptor = ExAllocatePoolWithTag(PagedPool, 
        Fcb->SecurityDescriptorLength, 'DSyM');

    if (!Fcb->SecurityDescriptor) {
        //
        // There is no paged pool.
        //
        SeDeassignSecurity(&SecurityDescriptor);
        Fcb->SecurityDescriptorLength = 0;
        return STATUS_NO_MEMORY;
    }

    RtlCopyMemory(Fcb->SecurityDescriptor, SecurityDescriptor, 
        Fcb->SecurityDescriptorLength);
 
    SeDeassignSecurity(&SecurityDescriptor);
 
    //
    // Store the SD persistently (this is file system specific).
    //
    (void) FsdStoreSecurityDescriptor(IrpContext, Fcb);

    return STATUS_SUCCESS;
}
```

初期のセキュリティ記述子 (理解の継承の例) を構築するロジックがファイル システム内で処理されないことに注意してください。 これは、合わせて、ファイル システム レイヤー内でのセキュリティ記述子を処理するための単純なモデルです。

 

 




