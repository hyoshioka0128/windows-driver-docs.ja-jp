---
title: 偽装
description: 偽装
ms.assetid: 368c6741-b51a-4629-8ae6-a7848c07c0fc
keywords:
- セキュリティ WDK ファイル システム、セキュリティ チェックを追加します。
- セキュリティは、WDK のファイル システム、権限借用を確認します。
- 権限借用 WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c01fda410e546f57488f0effc9c614e5acd1ce0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375689"
---
# <a name="impersonation"></a>偽装


## <span id="ddk_impersonation_if"></span><span id="DDK_IMPERSONATION_IF"></span>


一部のファイル システムに役に立つ最初の呼び出し元の代わりに操作を実行します。 たとえば、ネットワーク ファイル システムは、適切な資格情報を使用して、後続の操作を実行できるように、ファイルを開いた時点で、呼び出し元のセキュリティの情報をキャプチャする必要があります。 さまざまな他の特殊なケースこの種の機能が便利ですが、特定のアプリケーションと同様にもファイル システム内で両方がある間違いありません。

キーのルーチンに必要な権限の借用が含まれます。

-   [**PsImpersonateClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-psimpersonateclient) [**SeImpersonateClientEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-seimpersonateclientex)--偽装を開始します。 特定のスレッドは、指定した場合を除き、権限の借用は、現在のスレッド コンテキストで行われます。

-   **PsRevertToSelf**--現在のスレッド コンテキスト内で権限借用を終了します。

-   [**PsReferencePrimaryToken**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-psreferenceprimarytoken)--指定されたプロセスのプライマリ (プロセス) トークンの参照を保持します。 この関数は、システム上のどのプロセスのトークンをキャプチャを使用できます。

-   [**PsDereferencePrimaryToken**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-psdereferenceprimarytoken)-参照されている以前のプライマリ トークンの参照を解放します。

-   [**SeCreateClientSecurityFromSubjectContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-secreateclientsecurityfromsubjectcontext)--クライアントに返しますサブジェクト コンテキストからの権限借用のための便利なセキュリティ コンテキスト (中に、FSD に提供される、 **IRP\_MJ\_を作成します。** 処理など)。

-   [**SeCreateClientSecurity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-secreateclientsecurity)--システム上の既存のスレッドのセキュリティ資格情報に基づいたクライアントのセキュリティ コンテキストを作成します。

-   **ImpersonateSecurityContext**--ksecdd.sys、カーネルのセキュリティ サービス内でのセキュリティ コンテキストの権限を借用します。

-   **RevertSecurityContext**--ksecdd.sys、カーネルのセキュリティ サービス内で権限借用を終了します。

権限借用には、実装するために簡単です。 次のコード例では、基本的な権限の借用を示しています。

```cpp
NTSTATUS PerformSpecialTask(IN PFSD_CONTEXT Context)
{
  BOOLEAN CopyOnOpen;
  BOOLEAN EffectiveOnly;
  SECURITY_IMPERSONATION_LEVEL ImpersonationLevel;
  NTSTATUS Status;
  PACCESS_TOKEN oldToken;

  //
  // We need to perform a task in the system process context
  //
  if (NULL == Context->SystemProcess) {

    return STATUS_NO_TOKEN;

  }

  //
  // Save the existing token, if any (otherwise NULL)
  //
  oldToken = PsReferenceImpersonationToken(PsGetCurrentThread(),
                                           &CopyOnOpen,
                                           &EffectiveOnly,
                                           &ImpersonationLevel);

  Status = PsImpersonateClient( PsGetCurrentThread(),
                                Context->SystemProcess,
                                TRUE,
                                TRUE,
                                SecurityImpersonation);
  if (!NT_SUCCESS(Status)) {

    if (oldToken)
        PsDereferenceImpersonationToken(oldToken);
    return Status;

  }

  //
  // Perform task - whatever it is
  //


  //
  // Restore to previous impersonation level
  //
  if (oldToken) {
    Status = PsImpersonateClient(PsGetCurrentThread(),
                                 oldToken,
                                 CopyOnOpen,
                                 EffectiveOnly,
                                 ImpersonationLevel);

    if (!NT_SUCCESS(Status)) {
      //
      // This is bad - we can't restore, we can't leave it this way 
      //
      PsRevertToSelf();
    }
    PsDereferenceImpersonationToken(oldToken);
  } else {
    PsRevertToSelf();
  }

  return Status;
}
```

ファイル システムの開発者が利用できるは、この権限借用のコードのさまざまなバリエーションがありますが、この方法の基本的な説明を提供します。

 

 




