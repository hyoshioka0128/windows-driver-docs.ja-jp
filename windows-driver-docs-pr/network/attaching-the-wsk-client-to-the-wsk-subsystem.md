---
title: WSK サブシステムへの WSK クライアントのアタッチ
description: WSK サブシステムへの WSK クライアントのアタッチ
ms.assetid: 752d204f-3022-48b0-9237-707b753a7ad3
keywords:
- ネットワークモジュールレジストラー WDK Winsock カーネル
- NMR WDK Winsock カーネル
- WSK クライアントのアンロード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4872bc1ad829e78eadb2837050f4d1355c17b0ff
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835272"
---
# <a name="attaching-the-wsk-client-to-the-wsk-subsystem"></a>WSK サブシステムへの WSK クライアントのアタッチ


Winsock カーネル (WSK) アプリケーションが WSK NPI のクライアントとして[ネットワークモジュールレジストラー (NMR)](network-module-registrar2.md)に登録されると、NMR は wsk サブシステムが読み込まれた場合、アプリケーションの[*clientattachprovider*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_attach_provider_fn)コールバック関数を直ちに呼び出します。NMR に登録されています。 WSK サブシステムが NMR に登録されていない場合、NMR は WSK サブシステムが NMR に登録するまで、アプリケーションの*Clientattachprovider*コールバック関数を呼び出しません。

WSK アプリケーションは、添付ファイルの手順を完了するために、次の一連の呼び出しを行う必要があります。

1.  NMR は WSK アプリケーションの*Clientattachprovider*コールバック関数を呼び出すと、wsk サブシステムに関連付けられている[**NPI\_REGISTRATION\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/ns-netioddk-_npi_registration_instance)構造体へのポインターを渡します。 WSK アプリケーションの*Clientattachprovider*コールバック関数は、NMR によって渡されたデータを使用して、wsk サブシステムにアタッチできるかどうかを判断できます。 通常、wsk アプリケーションで必要なのは、wsk [ **\_プロバイダーの\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_characteristics)の構造に含まれているバージョン情報だけです。この構造体は wsk サブシステムの NPI**のメンバーに**よってポイントされ\_登録\_インスタンス構造。

2.  Wsk アプリケーションが wsk サブシステムにアタッチできると判断した場合、WSK アプリケーションの*Clientattachprovider*コールバック関数は wsk サブシステムへの添付ファイルのバインドコンテキスト構造を割り当てて初期化します。 次に、アプリケーションは[**NmrClientAttachProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrclientattachprovider)関数を呼び出して、添付ファイルの処理を続行します。

    **NmrClientAttachProvider**が STATUS\_SUCCESS を返した場合、wsk アプリケーションは wsk サブシステムに正常にアタッチされています。 この場合、WSK アプリケーションの*clientattachprovider*コールバック関数は、NMR がアプリケーションの*clientattachprovider*を呼び出したときに、NMR が*NmrBindingHandle*パラメーターに渡したバインドハンドルを保存する必要があります。コールバック関数。 WSK アプリケーションの*Clientattachprovider*コールバック関数は、クライアントオブジェクト ( [**wsk\_クライアント**](https://docs.microsoft.com/windows-hardware/drivers/network/wsk-client)) へのポインターと、で返されるプロバイダーディスパッチテーブル ( [**WSK\_プロバイダー\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_dispatch)) にも保存する必要があります。アプリケーションが*ProviderBindingContext*および*Providerdispatch*パラメーターの**NmrClientAttachProvider**関数に渡された変数。 WSK アプリケーションは、通常、WSK サブシステムへの添付ファイルのバインドコンテキストにこのデータを保存します。 Wsk アプリケーションが WSK サブシステムに正常にアタッチされた後、WSK アプリケーションの*Clientattachprovider*コールバック関数は、STATUS\_SUCCESS を返す必要があります。

3.  **NmrClientAttachProvider**が STATUS\_nointerface を返した場合、wsk アプリケーションはもう一度**NmrClientAttachProvider**関数を呼び出し、 *clientdispatch*を渡すことによって wsk サブシステムへのアタッチを試みることができます。アプリケーションでサポートされている WSK NPI の代替バージョンを指定する別の[**wsk\_クライアント\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_client_dispatch)構造体へのポインター。

4.  **NmrClientAttachProvider**関数の呼び出しで STATUS\_SUCCESS が返されず、wsk アプリケーションが wsk サブシステムへのアタッチをそれ以上試行していない場合、wsk アプリケーションの*clientattachprovider*コールバック関数は、 **NmrClientAttachProvider**を呼び出す前に割り当てられたすべてのリソースをクリーンアップし、割り当てを解除する必要があります。 この場合、WSK アプリケーションの*Clientattachprovider*コールバック関数は、 **NmrClientAttachProvider**関数の最後の呼び出しによって返されたステータスコードを返す必要があります。

5.  WSK アプリケーションがプロバイダーモジュールにアタッチできないと判断した場合、アプリケーションの*Clientattachprovider*コールバック関数はステータス\_nointerface を返す必要があります。

WSK アプリケーションを WSK サブシステムにアタッチする方法を次のコード例に示します。

```C++
// Context structure type for the WSK application's
// binding to the WSK subsystem
typedef struct WSK_APP_BINDING_CONTEXT_ {
  HANDLE NmrBindingHandle;
  PWSK_CLIENT WskClient;
  PWSK_PROVIDER_DISPATCH WskProviderDispatch;
  .
  . // Other application-specific members
  .
} WSK_APP_BINDING_CONTEXT, *PWSK_APP_BINDING_CONTEXT;

// Pool tag used for allocating the binding context
#define BINDING_CONTEXT_POOL_TAG 'tpcb'

// The WSK application uses version 1.0 of WSK
#define WSK_APP_WSK_VERSION MAKE_WSK_VERSION(1,0)

// Structure for the WSK application's dispatch table
const WSK_CLIENT_DISPATCH WskAppDispatch = {
  WSK_APP_WSK_VERSION,
  0,
  NULL  // No WskClientEvent callback
};

// ClientAttachProvider NMR API callback function
NTSTATUS
  ClientAttachProvider(
    IN HANDLE NmrBindingHandle,
    IN PVOID ClientContext,
    IN PNPI_REGISTRATION_INSTANCE ProviderRegistrationInstance
    )
{
  PNPI_MODULEID WskProviderModuleId;
  PWSK_PROVIDER_CHARACTERISTICS WskProviderCharacteristics;
  PWSK_APP_BINDING_CONTEXT BindingContext;
  PWSK_CLIENT WskClient;
  PWSK_PROVIDER_DISPATCH WskProviderDispatch;
  NTSTATUS Status;

  // Get pointers to the WSK subsystem's identification and
  // characteristics structures
  WskProviderModuleId = ProviderRegistrationInstance->ModuleId;
  WskProviderCharacteristics =
    (PWSK_PROVIDER_CHARACTERISTICS)
      ProviderRegistrationInstance->NpiSpecificCharacteristics;

  //
  // The WSK application can use the data in the structures pointed
  // to by ProviderRegistrationInstance, WskProviderModuleId, and
  // WskProviderCharacteristics to determine if the WSK application
  // can attach to the WSK subsystem.
  //
  // In this example, the WSK application does not perform any
  // checks to determine if it can attach to the WSK subsystem.
  //

  // Allocate memory for the WSK application's binding
  // context structure
  BindingContext =
    (PWSK_APP_BINDING_CONTEXT)
      ExAllocatePoolWithTag(
        NonPagedPool,
        sizeof(WSK_APP_BINDING_CONTEXT),
        BINDING_CONTEXT_POOL_TAG
        );

  // Check result of allocation
  if (BindingContext == NULL)
  {
    // Return error status code
    return STATUS_INSUFFICIENT_RESOURCES;
  }

  // Initialize the binding context structure
  ...
 
  // Continue with the attachment to the WSK subsystem
  Status = NmrClientAttachProvider(
    NmrBindingHandle,
    BindingContext,
    &WskAppDispatch,
    &WskClient,
    &WskProviderDispatch
    );

  // Check result of attachment
  if (Status == STATUS_SUCCESS)
  {
    // Save NmrBindingHandle, WskClient, and
    // WskProviderDispatch for future reference
    BindingContext->NmrBindingHandle = NmrBindingHandle;
    BindingContext->WskClient = WskClient;
    BindingContext->WskProviderDispatch = WskProviderDispatch;
  }

  // Attachment did not succeed
  else
  {
    // Free memory for application's binding context structure
    ExFreePoolWithTag(
      BindingContext,
      BINDING_CONTEXT_POOL_TAG
      );
  }

  // Return result of attachment
  return Status;
}
```

 

 





