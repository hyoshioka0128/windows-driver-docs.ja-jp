---
title: その他のトランザクション インターフェイス
description: その他のトランザクション インターフェイス
ms.assetid: cbd88c96-6445-436b-8e02-09dd9cf40d77
keywords:
- トランザクション WDK KTM、非 KTM インターフェイス
- トランザクションインターフェイス WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 325221049233093e0ca88ea86a8c9234f74da01e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837239"
---
# <a name="additional-transactional-interfaces"></a>その他のトランザクション インターフェイス


KTM にアクセスすることによって使用できるトランザクションインターフェイスに加えて、Microsoft では次のようないくつかの追加のトランザクションインターフェイスが提供されています。

-   ファイルシステムミニフィルタードライバーでは、[フィルタマネージャー](https://docs.microsoft.com/windows-hardware/drivers/ifs/filter-manager-and-minifilter-driver-architecture)によって、ミニフィルタードライバーをトランザクションに参加させたり、トランザクション状態の変更に関する通知を受信したり、コンテキストをトランザクションにアタッチしたりできるルーチンが用意されています。 これらの機能の詳細については、「 [**Fldisks Listintransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltenlistintransaction)」を参照してください。

-   Windows Vista 以降では、NTFS ファイルシステムとレジストリは、トランザクション操作をサポートするリソースマネージャーとして実装されています。 トランザクション NTFS とトランザクションレジストリの機能の詳細については、Microsoft Windows SDK を参照してください。

-   分散トランザクションコーディネーター (DTC) は、 **Iカーネルトランザクション**インターフェイスを介して、KTM との相互運用性を提供します。 **Iカーネルトランザクション**インターフェイスの詳細については、Microsoft Windows SDK を参照してください。

-   .NET Framework**は、system.string 名前空間**をサポートしています。 この名前空間の詳細については、 [Microsoft developer web サイト](https://go.microsoft.com/fwlink/p/?linkid=8714)を参照してください。

 

 




