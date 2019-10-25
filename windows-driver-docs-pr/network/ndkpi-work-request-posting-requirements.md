---
title: NDKPI 作業要求投稿要件
description: このセクションでは、NDKPI work 要求の投稿の要件について説明します。
ms.assetid: 2BF6F253-FCB4-4A61-9A67-81092F3C44E4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7df322909559045a3412a3b471558c0e5cf80ead
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829108"
---
# <a name="ndkpi-work-request-posting-requirements"></a>NDKPI 作業要求投稿要件


## <a name="work-request-posting-rules-for-the-consumer"></a>コンシューマーの勤務先要求の投稿ルール


NDK コンシューマーは、次の種類の作業要求を発信側キューに送信します。

-   *Ndkbind* ([*NDK\_FN\_BIND*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_bind))
-   *Ndkfastregister* ([*NDK\_FN\_FAST\_REGISTER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_fast_register))
-   *NdkInvalidate* ([*NDK\_FN\_無効化*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_invalidate))
-   *Ndkread* ([*NDK\_FN\_読み取り*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_read))
-   *Ndksend* ([*NDK\_FN\_SEND*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_send))
-   *Ndksendandinvalidate* ([*NDK\_FN\_SEND\_および\_無効化*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_send_and_invalidate))
-   *Ndkwrite* ([*NDK\_FN\_書き込み*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_write))

コンシューマーは、受信キューに*Ndkreceive* ([*NDK\_FN\_receive*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_receive)) 要求を送信します。

コンシューマーは、すべての要求を[**NDK\_QP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_qp)または ndk の同じ個別のキューに送信し、シリアル化された形式で[ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_srq)します。 つまり、1つの**ndk\_QP**または**ndk\_** に属する同一のキューにあるすべての作業要求関数に対して、コンシューマーが同時に2回呼び出しを行うことはありません。

つまり、たとえば、同時*Ndkreceive*呼び出しは発行されず、同時*Ndkreceive*呼び出しと*ndkreceive*呼び出しは発行されませんが、同時*ndkreceive*および*ndkreceive*呼び出しは同じ NDK で発行される可能性があり[ **@no__ QP (_s)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_qp)。

## <a name="work-request-posting-rules-for-the-provider"></a>プロバイダーの作業要求の投稿ルール


プロバイダーは、コンシューマーによってシリアル化されることが保証されるため、上記の作業要求関数内に冗長なロックを設定することはできません。

プロバイダーは、同じ[**ndk\_QP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_qp)で作業要求呼び出しと同時に呼び出すことができる*ndkflush* ([*ndk\_FN\_FLUSH*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_flush)) 呼び出しを処理できる必要があります。

プロバイダーは、同じ**ndk\_qp**で作業要求呼び出しと同時に呼び出される可能性がある、( [**ndk\_QP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_qp)の後継[ **\_コネクタ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_connector)オブジェクトの **) 呼び出しを**処理できる必要があります。

## <a name="related-topics"></a>関連トピック


[ネットワークダイレクトカーネルプロバイダーインターフェイス (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






