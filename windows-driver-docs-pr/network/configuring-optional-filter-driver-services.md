---
title: オプションのフィルター ドライバー サービスの構成
description: オプションのフィルター ドライバー サービスの構成
ms.assetid: 698e1b2a-de1a-435a-bc30-0d27d9e15e19
keywords:
- フィルター ドライバー WDK ネットワー キング、サービス
- NDIS フィルター ドライバー WDK、サービス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad6ed28f3e075081fb37b6c3edd93a006fe998c6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384213"
---
# <a name="configuring-optional-filter-driver-services"></a>オプションのフィルター ドライバー サービスの構成





NDIS フィルター ドライバーを呼び出す[ *FilterSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)オプションのフィルター ドライバー サービスを構成する関数。 NDIS 呼び出し*FilterSetOptions*フィルター ドライバーの呼び出しのコンテキスト内で、 [ **NdisFRegisterFilterDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfregisterfilterdriver)関数

*FilterSetOptions*の既定のエントリ ポイントを登録します。 省略可能な*FilterXxx*関数をオプションのサービスに必要なその他のドライバー リソースを割り当てることができます。 省略可能なサービスをフィルター ドライバーの呼び出しを登録する、 [ **NdisSetOptionalHandlers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissetoptionalhandlers)関数をある特性構造体を渡します、 *OptionalHandlers*パラメーター。

現在の Windows バージョンでは、オプションのフィルター ドライバーのサービスはありません。

フィルター ドライバーを呼び出すことも**NdisSetOptionalHandlers** 、いくつか設定する*FilterXxx*関数の特定のフィルター モジュールのエントリ ポイント。 詳細については、次を参照してください。[データ バイパス モード](data-bypass-mode.md)します。

フィルター ドライバーを呼び出す場合**NdisSetOptionalHandlers**から*FilterRestart*構成の変更では、NDIS を再起動するフィルター モジュールのみに影響します。 その他のフィルター モジュールの構成が影響を受けません。

 

 





