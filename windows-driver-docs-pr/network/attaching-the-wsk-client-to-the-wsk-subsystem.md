---
title: WSK サブシステムへの WSK クライアントのアタッチ
description: WSK サブシステムへの WSK クライアントのアタッチ
ms.assetid: 752d204f-3022-48b0-9237-707b753a7ad3
keywords:
- ネットワーク モジュール レジストラー WDK Winsock カーネル
- NMR WDK Winsock カーネル
- アンロード WSK クライアント
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b71e4690dfde5d598b0c7589a653024b358c0bf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354641"
---
# <a name="attaching-the-wsk-client-to-the-wsk-subsystem"></a>WSK サブシステムへの WSK クライアントのアタッチ


アプリケーションが登録されて、Winsock カーネル (WSK) した後、[ネットワーク モジュール レジストラー (NMR)](network-module-registrar2.md) WSK NPI のクライアントとして、NMR すぐに呼び出し、アプリケーションの[ *ClientAttachProvider*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nc-netioddk-npi_client_attach_provider_fn) WSK サブシステムが読み込まれ、NMR に登録した場合、コールバック関数。 WSK サブシステムが、NMR で登録されていない場合、NMR がアプリケーションを呼び出しません*ClientAttachProvider* NMR WSK サブシステムに登録されるまで、コールバック関数。

WSK アプリケーションでは、次の一連の呼び出しが、添付ファイルの手順を完了するを実行する必要があります。

1.  NMR が WSK アプリケーションを呼び出すときに*ClientAttachProvider*コールバック関数へのポインターを渡しますが、 [ **NPI\_登録\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/ns-netioddk-_npi_registration_instance) WSK サブシステムに関連付けられている構造体。 WSK アプリケーションの*ClientAttachProvider*コールバック関数は、NMR によって渡されたデータを使用して、WSK サブシステムにアタッチができるかどうかを判断します。 通常、WSK アプリケーションでのみに含まれるバージョン情報が必要、 [ **WSK\_プロバイダー\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/ns-wsk-_wsk_provider_characteristics) を指しています構造**NpiSpecificCharacteristics** WSK サブシステムの NPI のメンバー\_登録\_インスタンス構造体。

2.  WSK アプリケーションが、WSK サブシステムに、WSK アプリケーションのアタッチすることができますを指定する場合*ClientAttachProvider*コールバック関数は、割り当て、WSK サブシステムに添付ファイルのバインド コンテキストの構造体を初期化します. その後、アプリケーションを呼び出す、 [ **NmrClientAttachProvider** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nf-netioddk-nmrclientattachprovider)添付ファイルの処理を続行する関数。

    場合**NmrClientAttachProvider**ステータスを返します\_成功すると、WSK アプリケーションが正常にアタッチ WSK サブシステムにします。 このような状況で、WSK アプリケーションの*ClientAttachProvider*コールバック関数に渡された、NMR バインド ハンドルを保存する必要があります、 *NmrBindingHandle*パラメーター、NMR が呼び出されたときに、アプリケーションの*ClientAttachProvider*コールバック関数。 WSK アプリケーションの*ClientAttachProvider*コールバック関数ではクライアント オブジェクトへのポインターを保存してもする必要があります ( [ **WSK\_クライアント**](https://docs.microsoft.com/windows-hardware/drivers/network/wsk-client)) とプロバイダーディスパッチ テーブル ( [ **WSK\_プロバイダー\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/ns-wsk-_wsk_provider_dispatch)) に渡される、アプリケーション変数に返される、 **NmrClientAttachProvider**で機能、 *ProviderBindingContext*と*ProviderDispatch*パラメーター。 通常、WSK アプリケーションでは、このデータが WSK サブシステムに添付ファイルのバインド コンテキストに保存します。 WSK 後にアプリケーションが正常に WSK サブシステムに、WSK アプリケーションのアタッチ*ClientAttachProvider*コールバック関数は、状態を返す必要があります\_成功します。

3.  場合**NmrClientAttachProvider**ステータスを返します\_NOINTERFACE、WSK アプリケーションが呼び出すことによって、WSK サブシステムにアタッチする別の試行を行うことができます、 **NmrClientAttachProvider**渡すことをもう一度、関数、 *ClientDispatch*別へのポインター [ **WSK\_クライアント\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/ns-wsk-_wsk_client_dispatch)構造体アプリケーションでサポートされている WSK NPI の別のバージョンを指定します。

4.  呼び出し、 **NmrClientAttachProvider**関数には、状態は返しません\_成功すると、WSK アプリケーションはさらに、WSK サブシステムに、WSK アプリケーションの接続試行はすべてを行わない *。ClientAttachProvider*コールバック関数のクリーンアップおよびと呼ばれる前に、割り当てられているすべてのリソースの割り当てを解除する必要があります**NmrClientAttachProvider**します。 このような状況で、WSK アプリケーションの*ClientAttachProvider*コールバック関数は、最後の呼び出しによって返されたステータス コードを返す必要があります、 **NmrClientAttachProvider**関数。

5.  プロバイダー モジュールに、アプリケーションの接続にすることはできません、WSK アプリケーションと判断した場合*ClientAttachProvider*コールバック関数は、状態を返す必要があります\_NOINTERFACE します。

次のコード例では、どのように WSK アプリケーションにアタッチできる自体、WSK サブシステムを示します。

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

 

 





