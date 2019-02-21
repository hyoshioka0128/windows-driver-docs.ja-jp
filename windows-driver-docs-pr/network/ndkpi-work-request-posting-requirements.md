---
title: NDKPI 作業要求の投稿の要件
description: このセクションは、NDKPI 作業要求投稿するための要件を説明します
ms.assetid: 2BF6F253-FCB4-4A61-9A67-81092F3C44E4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c063b33f5396498d020e4150a1ffc71f35fb6755
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530192"
---
# <a name="ndkpi-work-request-posting-requirements"></a>NDKPI 作業要求の投稿の要件


## <a name="work-request-posting-rules-for-the-consumer"></a>作業要求が、コンシューマーの転記ルール


NDK コンシューマーは、次の種類の作業要求を発信側キューに投稿されます。

-   *NdkBind* ([*NDK\_FN\_BIND*](https://msdn.microsoft.com/library/windows/hardware/hh439859))
-   *NdkFastRegister* ([*NDK\_FN\_FAST\_REGISTER*](https://msdn.microsoft.com/library/windows/hardware/hh439887))
-   *NdkInvalidate* ([*NDK\_FN\_INVALIDATE*](https://msdn.microsoft.com/library/windows/hardware/hh439901))
-   *NdkRead* ([*NDK\_FN\_READ*](https://msdn.microsoft.com/library/windows/hardware/hh439906))
-   *NdkSend* ([*NDK\_FN\_SEND*](https://msdn.microsoft.com/library/windows/hardware/hh439914))
-   *NdkSendAndInvalidate* ([*NDK\_FN\_SEND\_AND\_INVALIDATE*](https://msdn.microsoft.com/library/windows/hardware/dn265507))
-   *NdkWrite* ([*NDK\_FN\_WRITE*](https://msdn.microsoft.com/library/windows/hardware/hh439917))

コンシューマーでは、投稿*NdkReceive* ([*NDK\_FN\_受信*](https://msdn.microsoft.com/library/windows/hardware/hh439907)) 受信キューに要求します。

コンシューマーはのすべてが同じ個別のキューにこれらの要求を投稿、 [ **NDK\_QP** ](https://msdn.microsoft.com/library/windows/hardware/hh439933)または[ **NDK\_の**](https://msdn.microsoft.com/library/windows/hardware/hh439939)シリアル化された形式でします。 つまり、コンシューマーがない任意の作業要求関数への 2 つの同時呼び出しに属する個々 のキューで同じで、 **NDK\_QP**または**NDK\_の**します。

つまり、たとえば、その同時*NdkReceive*発行された、同時呼び出しはできません*NdkSend*と*NdkWrite*呼び出しを発行しませんが、同時*NdkReceive*と*NdkWrite* 、同じ呼び出しを発行できる[ **NDK\_QP**](https://msdn.microsoft.com/library/windows/hardware/hh439933)します。

## <a name="work-request-posting-rules-for-the-provider"></a>作業の要求プロバイダーの規則を投稿します。


プロバイダーでは、コンシューマーによってシリアル化することが保証されますので、上記の作業要求関数内で冗長なロックは必要ありません。

プロバイダーは、処理できる必要があります*NdkFlush* ([*NDK\_FN\_フラッシュ*](https://msdn.microsoft.com/library/windows/hardware/hh439889))、作業と同時に呼び出すことが呼び出しの呼び出しを要求します。同じ[ **NDK\_QP**](https://msdn.microsoft.com/library/windows/hardware/hh439933)します。

プロバイダーは、処理できる必要があります、 **NdkCloseConnector**呼び出し (後継の[ **NDK\_コネクタ**](https://msdn.microsoft.com/library/windows/hardware/hh439852)オブジェクト、 [ **NDK\_QP**](https://msdn.microsoft.com/library/windows/hardware/hh439933)) を呼び出すことができます、作業要求の呼び出しと同時に同じ**NDK\_QP**します。

## <a name="related-topics"></a>関連トピック


[ネットワーク ダイレクト カーネル プロバイダー インターフェイス (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






