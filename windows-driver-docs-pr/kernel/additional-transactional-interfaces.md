---
title: その他のトランザクション インターフェイス
description: その他のトランザクション インターフェイス
ms.assetid: cbd88c96-6445-436b-8e02-09dd9cf40d77
keywords:
- トランザクション WDK KTM、KTM 以外のインターフェイス
- トランザクション インターフェイス WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 381f4e9ca14aebdce12dc4360bf2201270dfe3c4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369989"
---
# <a name="additional-transactional-interfaces"></a>その他のトランザクション インターフェイス


KTM にアクセスして使用できるトランザクション インターフェイスだけでなく、マイクロソフトは、次を含む、いくつかの追加トランザクション インターフェイスを提供します。

-   ファイル システム ミニフィルター ドライバーについて、[フィルター マネージャー](https://docs.microsoft.com/windows-hardware/drivers/ifs/filter-manager-and-minifilter-driver-architecture)トランザクションに参加するミニフィルター ドライバーを有効にするルーチン トランザクション状態の変更に関する通知を受け取るし、コンテキストをトランザクションにアタッチを提供します。 これらの機能の詳細については、次を参照してください。 [ **FltEnlistInTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltenlistintransaction)します。

-   Windows Vista 以降、NTFS ファイル システムとレジストリとして実装されますトランザクション操作をサポートするリソース マネージャー。 トランザクション NTFS とレジストリのトランザクション機能の詳細については、Microsoft Windows SDK を参照してください。

-   分散トランザクション コーディネーター (DTC) から KTM と相互運用性を提供する、 **IKernelTransaction**インターフェイス。 詳細については、 **IKernelTransaction**インターフェイス、Microsoft Windows SDK を参照してください。

-   .NET Framework のサポート、 **System.Transactions**名前空間。 この名前空間の詳細については、次を参照してください。、 [Microsoft 開発者向けの web サイト](https://go.microsoft.com/fwlink/p/?linkid=8714)します。

 

 




