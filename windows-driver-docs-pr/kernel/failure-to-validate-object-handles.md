---
title: オブジェクトハンドルの検証エラー
description: オブジェクトハンドルの検証エラー
ms.assetid: 67d52ca8-4e86-4fe2-a541-f7a0e4040b93
keywords:
- 信頼性 WDK カーネル、オブジェクトハンドルの検証
- 検証エラー (WDK カーネル)
- オブジェクトは WDK カーネルを処理します
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc8f4a028e51bd06407dd6463bc03b91cbfb8909
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838697"
---
# <a name="failure-to-validate-object-handles"></a>オブジェクトハンドルの検証エラー





一部のドライバーでは、呼び出し元によって渡されたオブジェクトを操作する必要があります。または、2つのファイルオブジェクトを同時に処理する必要があります。 たとえば、モデムドライバーがイベントオブジェクトへのハンドルを受け取る場合や、ネットワークドライバーが2つの異なるファイルオブジェクトへのハンドルを受け取る場合があります。 ドライバーは、これらのハンドルを検証する必要があります。 I/o マネージャーは、i/o マネージャーを介してではなく、呼び出し元によって渡されるため、i/o マネージャーは検証を実行できません。

たとえば、次のコードスニペットでは、ドライバーにハンドル**Ascinfo-&gt;AddressHandle**が渡されていますが、 [**Obreferenceobjectbyhandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)を呼び出す前にこのドライバーは検証されていません。

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

**Obreferenceobjectbyhandle**の呼び出しは成功しますが、コードは返されたポインターがファイルオブジェクトを参照することを確認できません。正しい情報を渡すために、呼び出し元を信頼します。

**Obreferenceobjectbyhandle**への呼び出しのすべてのパラメーターが正しい場合でも、呼び出しが成功しても、ファイルオブジェクトがドライバー用ではない場合でも、ドライバーは予期しない結果を受ける可能性があります。 次のコードフラグメントでは、正常な呼び出しによって、予期されたファイルオブジェクトへのポインターが返されると想定しています。

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

**Obreferenceobjectbyhandle**はファイルオブジェクトへのポインターを返しますが、ドライバーは、ポインターが予期されたファイルオブジェクトを参照することを保証しません。 この場合、ドライバーは、 **AcpEndpointFileObject-&gt;FsContext**でドライバー固有のデータにアクセスする前に、ポインターを検証する必要があります。

このような問題を回避するには、次のように、ドライバーが有効なデータを確認する必要があります。

-   オブジェクトの種類を確認して、ドライバーが想定しているものであることを確認してください。

-   要求されたアクセスがオブジェクトの種類と必要なタスクに適していることを確認します。 たとえば、ドライバーが高速ファイルコピーを実行する場合は、ハンドルに読み取りアクセス権があることを確認します。

-   適切なアクセス**モード ([モード]** または **[kernelmode で]** ) を指定し、アクセスモードが要求されたアクセスと互換性があることを確認してください。

-   ドライバー自体が作成したファイルオブジェクトへのハンドルをドライバーが要求する場合は、デバイスオブジェクトまたはドライバーに対するハンドルを検証します。 ただし、奇妙なデバイスの i/o 要求を送信するフィルターを中断しないように注意してください。

-   ドライバーが複数の種類のファイルオブジェクト (コントロールチャネル、アドレスオブジェクト、およびファイルシステムのボリューム、ディレクトリ、ファイルオブジェクトの接続など) をサポートしている場合は、それらを区別する方法があることを確認してください。

 

 




