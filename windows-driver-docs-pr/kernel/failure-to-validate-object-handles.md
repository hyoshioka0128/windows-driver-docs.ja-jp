---
title: オブジェクト ハンドルの検証に失敗しました
description: オブジェクト ハンドルの検証に失敗しました
ms.assetid: 67d52ca8-4e86-4fe2-a541-f7a0e4040b93
keywords:
- 信頼性 WDK カーネルでは、オブジェクトのハンドルの検証
- 検証エラーの WDK カーネル
- オブジェクト ハンドル WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 198ace4aca05664a91f8244398fe2e3bc80c6ef5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538709"
---
# <a name="failure-to-validate-object-handles"></a>オブジェクト ハンドルの検証に失敗しました





一部のドライバーでは、呼び出し元が、渡されたオブジェクトを操作する必要があります。 または同時に 2 つのファイル オブジェクトを処理する必要があります。 たとえば、モデムのドライバーは、イベント オブジェクトを識別するハンドルを受け取ることがあります。 またはネットワーク ドライバーは、2 つの別のファイル オブジェクトへのハンドルを受け取ることがあります。 ドライバーは、これらのハンドルを検証する必要があります。 I/O マネージャーではなく、呼び出し元によって渡されるために、I/O マネージャーは、検証チェックを実行できません。

たとえば、次のコード スニペットで、ドライバーが渡されたハンドル**AscInfo -&gt;AddressHandle**を呼び出す前に、検証されていませんが、 [ **ObReferenceObjectByHandle**](https://msdn.microsoft.com/library/windows/hardware/ff558679):

```cpp
   //
   // This handle is embedded in a buffered request.
   //
   status = ObReferenceObjectByHandle(
                      AscInfo->AddressHandle,
                      0,
                      NULL,
                      KernelMode,
                      &fileObject,
                      NULL);

   if (NT_SUCCESS(status)) {
       if ( (fileObject->DeviceObject == DeviceObject) &&
            (fileObject->FsContext2 == TRANSPORT_SOCK) ) {
```

呼び出し**ObReferenceObjectByHandle**成功すると、コードが返されるポインターが、ファイル オブジェクトを参照していることを確認に失敗した。 正しい情報を渡す呼び出し元を信頼します。

場合でも、呼び出しのすべてのパラメーター **ObReferenceObjectByHandle**が正しいこと、および呼び出しが成功すると、ファイル オブジェクトはドライバーのためのものである場合、ドライバーは予期しない結果を取得もできます。 次のコード フラグメントでは、ドライバーは、呼び出しが成功したことが予想ファイル オブジェクトへのポインターを返すこと前提とします。

```cpp
   status = ObReferenceObjectByHandle (
                             AcpInfo->Handle,
                             0L,
                             DesiredAccess,
                             *IoFileObjectType,
                             Irp->RequestorMode,
                             (PVOID *)&AcpEndpointFileObject,
                             NULL);

   if ( !NT_SUCCESS(status) ) {
      goto complete;
   }
   AcpEndpoint = AcpEndpointFileObject->FsContext;

   if ( AcpEndpoint->Type != BlockTypeEndpoint ) 
```

**ObReferenceObjectByHandle**返しますが、ドライバー、ファイル オブジェクトへのポインターにポインターが必要ですが、ファイル オブジェクトを参照している保証がありません。 この場合、ドライバーはドライバー固有のデータにアクセスする前にポインターを検証する必要があります**AcpEndpointFileObject -&gt;FsContext**します。

このような問題を回避するために、ドライバーは、有効なデータには、次のように確認する必要があります。

-   ドライバーで必要なものかどうかを確認するオブジェクトの種類を確認します。

-   要求されたアクセスがオブジェクトの種類と必要なタスクに適していることを確認します。 ドライバーは、高速ファイル コピーを実行する場合、ハンドルが読み取りアクセス権を確認します。

-   適切なアクセス モードを指定してください (**UserMode**または**kernelmode である**) アクセス モードが要求されるアクセスと互換性があるとします。

-   ドライバーには、ドライバー自体に作成されたファイル オブジェクトを識別するハンドルが必要ですが場合、は、ドライバー、デバイスのオブジェクトに対するハンドルを検証します。 ただし、異常なデバイスの I/O 要求の送信フィルターを中断しないように注意します。

-   それらを区別する手段がある、ドライバーがサポートする複数の種類 (など、コントロール チャネル、アドレス オブジェクト、および TDI ドライバーの接続やファイル システムのボリューム、ディレクトリ、およびファイルのオブジェクト)、ファイル オブジェクトのことを確認します。 場合、

 

 




