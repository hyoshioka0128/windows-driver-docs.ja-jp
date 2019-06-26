---
title: NDKPI 作業要求投稿要件
description: このセクションは、NDKPI 作業要求投稿するための要件を説明します
ms.assetid: 2BF6F253-FCB4-4A61-9A67-81092F3C44E4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4182ffa518121beab9ac7ac71d12629f29731654
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364022"
---
# <a name="ndkpi-work-request-posting-requirements"></a>NDKPI 作業要求投稿要件


## <a name="work-request-posting-rules-for-the-consumer"></a>作業要求が、コンシューマーの転記ルール


NDK コンシューマーは、次の種類の作業要求を発信側キューに投稿されます。

-   *NdkBind* ([*NDK\_FN\_BIND*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_bind))
-   *NdkFastRegister* ([*NDK\_FN\_FAST\_REGISTER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_fast_register))
-   *NdkInvalidate* ([*NDK\_FN\_INVALIDATE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_invalidate))
-   *NdkRead* ([*NDK\_FN\_READ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_read))
-   *NdkSend* ([*NDK\_FN\_SEND*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_send))
-   *NdkSendAndInvalidate* ([*NDK\_FN\_SEND\_AND\_INVALIDATE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_send_and_invalidate))
-   *NdkWrite* ([*NDK\_FN\_WRITE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_write))

コンシューマーでは、投稿*NdkReceive* ([*NDK\_FN\_受信*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_receive)) 受信キューに要求します。

コンシューマーはのすべてが同じ個別のキューにこれらの要求を投稿、 [ **NDK\_QP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_qp)または[ **NDK\_の**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_srq)シリアル化された形式でします。 つまり、コンシューマーがない任意の作業要求関数への 2 つの同時呼び出しに属する個々 のキューで同じで、 **NDK\_QP**または**NDK\_の**します。

つまり、たとえば、その同時*NdkReceive*発行された、同時呼び出しはできません*NdkSend*と*NdkWrite*呼び出しを発行しませんが、同時*NdkReceive*と*NdkWrite* 、同じ呼び出しを発行できる[ **NDK\_QP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_qp)します。

## <a name="work-request-posting-rules-for-the-provider"></a>作業の要求プロバイダーの規則を投稿します。


プロバイダーでは、コンシューマーによってシリアル化することが保証されますので、上記の作業要求関数内で冗長なロックは必要ありません。

プロバイダーは、処理できる必要があります*NdkFlush* ([*NDK\_FN\_フラッシュ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_flush))、作業と同時に呼び出すことが呼び出しの呼び出しを要求します。同じ[ **NDK\_QP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_qp)します。

プロバイダーは、処理できる必要があります、 **NdkCloseConnector**呼び出し (後継の[ **NDK\_コネクタ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_connector)オブジェクト、 [ **NDK\_QP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_qp)) を呼び出すことができます、作業要求の呼び出しと同時に同じ**NDK\_QP**します。

## <a name="related-topics"></a>関連トピック


[ネットワーク ダイレクト カーネル プロバイダー インターフェイス (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






