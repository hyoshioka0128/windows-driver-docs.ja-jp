---
title: IRP_MJ_DIRECTORY_CONTROL のセキュリティチェック
description: ファイルシステムがセキュリティチェックを行う方法について説明し IRP_MJ_DIRECTORY_CONTROL
ms.assetid: 27c2de1c-5550-4211-97cc-4c66f18d3b99
keywords:
- IRP_MJ_DIRECTORY_CONTROL
- セキュリティ WDK ファイルシステム、セキュリティチェックの追加
- セキュリティチェック WDK ファイルシステム、IRP_MJ_DIRECTORY_CONTROL
- WDK ファイルシステムを管理するディレクトリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1296c259ae0025c3c2df858ac99e35cf4aae48d
ms.sourcegitcommit: df50dc10210c124f2c7fb173d6e4fb796f56e5bd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/22/2020
ms.locfileid: "86949726"
---
# <a name="security-checks-on-irp_mj_directory_control"></a>IRP_MJ_DIRECTORY_CONTROL のセキュリティチェック

特定のディレクトリ制御操作 (特に変更通知を扱うもの) を処理する場合は、セキュリティが考慮されます。 セキュリティ上の問題は、ディレクトリ変更通知によって、変更された特定のファイルに関する情報が返される可能性があるということです。 ディレクトリへのパスを走査する権限がユーザーに与えられていない場合、変更に関する情報をユーザーに返すことはできません。 それ以外の場合、ユーザーには、ユーザーが所有してはならないディレクトリに関する追加情報を学習するためのメカニズムが用意されています。

ファイルシステムのランタイムライブラリによるディレクトリ変更通知のサポートにより、ファイルシステムは、ディレクトリ変更通知を返す前に走査チェックを実行するためのコールバック関数を指定できます。 このコールバック関数は、多数のパラメーターを受け取ります。 セキュリティの考慮事項として、次の3つのパラメーターが重要です。

- *Notifycontext*は、変更通知がアクティブになっているディレクトリのコンテキストです。 これは、 [**Fsrtlnotifyfullchangedirectory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlnotifyfullchangedirectory)への呼び出しに渡される*fscontext*パラメーターになります。

- *Targetcontext*は、変更されたファイルのコンテキストです。 これは、 [**Fsrtlnotifyfilterreportchange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlnotifyfilterreportchange)を呼び出すときにファイルシステムによって渡される*targetcontext*パラメーターになります。

- *Subjectcontext*は、ディレクトリ変更通知を要求しているスレッドのセキュリティコンテキストです。 これは、 **Fsrtlnotifyfullchangedirectory**へのディレクトリ変更通知の呼び出しが行われたときにファイルシステムによってキャプチャされたサブジェクトセキュリティコンテキストです。

変更が発生すると、ファイルシステムによってファイルシステムのランタイムライブラリに対して指定されます。 ファイルシステムランタイムライブラリは、ファイルシステムによって提供されるコールバック関数を呼び出して、変更に関する情報を呼び出し元に与えることができるかどうかを確認します。 呼び出し元にチェックが必要な場合にのみ、ファイルシステムでコールバック関数を登録する必要があることに注意してください。 これは、呼び出し元のセキュリティトークンの TOKEN_HAS_TRAVERSE_PRIVILEGE に示されているように、呼び出し元で SeChangeNotifyPrivilege が有効になっていない場合に当てはまります。

コールバック関数内では、ファイルシステムは、 *Notifycontext*パラメーターによって指定されたディレクトリから、 *targetcontext*パラメーターによって指定された変更されたファイルへの走査チェックを実行する必要があります。 次のサンプルルーチンでは、このようなチェックを実行します。

```cpp
BOOLEAN
FsdNotifyTraverseCheck (
    IN PDIRECTORY_CONTEXT OriginalDirectoryContext,
    IN PFILE_CONTEXT ModifiedDirectoryContext,
    IN PSECURITY_SUBJECT_CONTEXT SubjectContext
    )
{
  BOOLEAN AccessGranted = TRUE;
  PFILE_CONTEXT CurrentDirectoryContext;
  ACCESS_MASK GrantedAccess;
  NTSTATUS Status;
  PPRIVILEGE_SET Privileges = NULL;
  PFILE_CONTEXT TopDirectory;

  //
  //  Nothing to do if there is no file context.
  //
  if (ModifiedDirectoryContext == NULL) {

    return TRUE;
  }

  //
  // If the directory that changed is the original directory,
  // we can return , since the caller has access.
  // Note that the directory  context is unique to the specific
  // open instance, while the modified directory context
  // represents the per-file/directory context.
  // How these data structures work in your file system will vary.
  //
  if (OriginalDirectoryContext->FileContext == ModifiedDirectoryContext) {
    return TRUE;
  }

  //
  // Lock the subject context.
  //
  SeLockSubjectContext(SubjectContext);

  for( TopDirectory = OriginalDirectoryContext->FileContext,
          CurrentDirectoryContext = ModifiedDirectoryContext;
          CurrentDirectoryContext == TopDirectory || !AccessGranted;
          CurrentDirectoryContext = CurrentDirectoryContext->ParentDirectory) {
    //
    // Ensure we have the current security descriptor loaded for
    // this directory.
    //
    FsdLoadSecurity( NULL, CurrentDirectoryContext);

    //
    // Perform traverse check.
    //
    AccessGranted = SeAccessCheck(
            CurrentDirectoryContext->SecurityDescriptor,
            SubjectContext,
            TRUE,
            FILE_TRAVERSE,
            0,
            &Privileges,
            IoGetFileObjectGenericMapping(),
            UserMode,
            &GrantedAccess,
            &Status);

    //
    // At this point, exit the loop if access was not granted,
    // or if the parent directory is the same as where the change
    // notification was made.
    //

  }

  //
  // Unlock subject context.
  //
  SeUnlockSubjectContext(SubjectContext);

  return AccessGranted;
}
```

このルーチンは、セキュリティ情報をキャッシュするファイルシステムや、ファイルやディレクトリ間のリンクを追跡するための構造を使用するファイルなど、ファイルシステムによって大幅に異なる可能性があります。 このサンプルでは、この例を簡略化するために、リンクをサポートしているファイルシステムは考慮されていません。
