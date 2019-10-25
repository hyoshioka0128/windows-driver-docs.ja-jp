---
title: オプションのフィルター ドライバー サービスの構成
description: オプションのフィルター ドライバー サービスの構成
ms.assetid: 698e1b2a-de1a-435a-bc30-0d27d9e15e19
keywords:
- フィルタードライバー WDK ネットワーク、サービス
- NDIS フィルタードライバー WDK、サービス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 227cc60698e3ee4e5c8a9b4799e9935bc416b6b6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838183"
---
# <a name="configuring-optional-filter-driver-services"></a>オプションのフィルター ドライバー サービスの構成





NDIS は、フィルタードライバーの[*FilterSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)関数を呼び出して、オプションのフィルタードライバーサービスを構成します。 NDIS は、フィルタードライバーの[**NdisFRegisterFilterDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfregisterfilterdriver)関数の呼び出しのコンテキスト内で*FilterSetOptions*を呼び出します。

*FilterSetOptions*は、オプションのサービスに必要なオプションの*filterxxx*関数の既定のエントリポイントを登録し、他のドライバーリソースを割り当てることができます。 オプションのサービスを登録するために、フィルタードライバーは[**NdisSetOptionalHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)関数を呼び出し、オプションの*ハンドラー*パラメーターで特性の構造体を渡します。

現在の Windows バージョンには、オプションのフィルタードライバーサービスがありません。

フィルタードライバーは、 **NdisSetOptionalHandlers**を呼び出して、特定のフィルターモジュールの一部の*filterxxx*関数のエントリポイントを設定することもできます。 詳細については、「[データバイパスモード](data-bypass-mode.md)」を参照してください。

フィルタードライバーが*Filterrestart*から**NdisSetOptionalHandlers**を呼び出した場合、構成の変更は、NDIS によって再起動されるフィルターモジュールにのみ影響します。 他のフィルターモジュールの構成は影響を受けません。

 

 





