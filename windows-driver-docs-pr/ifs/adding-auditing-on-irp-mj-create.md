---
title: IRP_MJ_CREATE での監査の追加
description: IRP_MJ_CREATE での監査の追加
ms.assetid: cb71fe83-44f4-48dd-8fff-250f1d27c123
keywords:
- IRP_MJ_CREATE
- WDK のファイル システムの監査
- セキュリティは、WDK のファイル システム、irp_mj_create 用を確認します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a96484269cbd7d72e31972fbc45fa950128f1cae
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323164"
---
# <a name="adding-auditing-on-irpmjcreate"></a>IRP の監査を追加する\_MJ\_を作成します。


## <span id="ddk_adding_auditing_on_irp_mj_create_if"></span><span id="DDK_ADDING_AUDITING_ON_IRP_MJ_CREATE_IF"></span>


ファイル システム内でセキュリティ チェックのもう 1 つの重要な側面では、必要に応じて、監査を追加します。 通常、これは監査の目的は、システムによるセキュリティ上の決定を記録するために、セキュリティ上の決定を行うルーチンの同じセットの一部として行います。 たとえば、次のコードは、アクセス チェックの完了後にファイル システム内で監査を実装するために管理される可能性があります。

```cpp
{
UNICODE_STRING FileAuditObjectName;

RtlInitUnicodeString(&FileAuditObjectName, L"File");

if ( SeAuditingFileOrGlobalEvents (AccessGranted, 
        &Fcb->SecurityDescriptor, 
        &AccessState->SubjectSecurityContext)) {
    //
    // Must pass complete Windows path name, including device name.
    //
    ConstructAuditFileName(Irp, Fcb, &AuditName);

    if (IrpSp->Parameters.Create.SecurityContext->FullCreateOptions 
            & FILE_DELETE_ON_CLOSE) {
        SeOpenObjectForDeleteAuditAlarm(&FileAuditObjectName,
                                        NULL,
                                        &AuditName,
                                        &Fcb->SecurityDescriptor,
                                        AccessState,
                                        FALSE, // Object not created.
                                        // Was it  successful?  
                                        // Based on SeAccessCheck
                                        SeAccessCheckAccessGranted, 
                                        // UserMode or KernelMode
                                        EffectiveMode, 
                                        &AccessState->GenerateOnClose
                                        );
    } else {
        SeOpenObjectAuditAlarm(&FileAuditObjectName,
                               NULL,
                               &AuditName,
                               &Fcb->SecurityDescriptor,
                               AccessState,
                               FALSE, // object not created
                               // Was it successful?  
                               // Based on SeAccessCheck
                               AccessGranted, 
                               // UserMode or KernelMode
                               EffectiveMode, 
                               &AccessState->GenerateOnClose
                               );
    }

    //
    // Free file name here if needed.
    //
}
```

 

 




