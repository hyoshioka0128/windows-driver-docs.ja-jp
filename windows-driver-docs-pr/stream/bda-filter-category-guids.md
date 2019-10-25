---
title: BDA フィルターカテゴリ Guid
description: BDA フィルターカテゴリ Guid
ms.assetid: fbd4bf91-8309-423a-97ea-7e4f90cd3b68
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c9c75c8d2208216540bba31bf64c6c7cd73ce1f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840618"
---
# <a name="bda-filter-category-guids"></a>BDA フィルターカテゴリ Guid


## <span id="ddk_bda_filter_category_guids_ks"></span><span id="DDK_BDA_FILTER_CATEGORY_GUIDS_KS"></span>


Bda ミニドライバーは、bda フィルターカテゴリ Guid を使用して、作成する BDA フィルターの種類を指定します。 BDA ミニドライバーは、このような Guid を配列に割り当てます。これらの Guid は、 [**Ksk フィルター\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_descriptor)構造体の**カテゴリ**メンバーが指しています。 これらの Guid は、 *Bdamedia*ヘッダーファイルで定義されています。

次のフィルターカテゴリ Guid は、BDA で使用できます。

<span id="KSCATEGORY_BDA_RECEIVER_COMPONENT"></span><span id="kscategory_bda_receiver_component"></span>KSCATEGORY\_BDA\_レシーバー\_コンポーネント  
BDA ミニドライバーは、この GUID を割り当てて、BDA レシーバーフィルターを作成するように指定します。

<span id="KSCATEGORY_BDA_NETWORK_TUNER"></span><span id="kscategory_bda_network_tuner"></span>KSCATEGORY\_BDA\_ネットワーク\_チューナー  
BDA ミニドライバーは、この GUID を割り当てて、BDA ネットワークチューナーフィルターを作成するように指定します。

<span id="KSCATEGORY_BDA_NETWORK_EPG"></span><span id="kscategory_bda_network_epg"></span>KSCATEGORY\_BDA\_ネットワーク\_EPG  
BDA ミニドライバーは、この GUID を割り当てて、BDA 電子番組ガイド (EPG) フィルターを作成するように指定します。

<span id="KSCATEGORY_BDA_IP_SINK"></span><span id="kscategory_bda_ip_sink"></span>KSCATEGORY\_BDA\_IP\_シンク  
BDA ミニドライバーは、この GUID を割り当てて、BDA IP シンクフィルターを作成するように指定します。

<span id="KSCATEGORY_BDA_NETWORK_PROVIDER"></span><span id="kscategory_bda_network_provider"></span>KSCATEGORY\_BDA\_ネットワーク\_プロバイダー  
BDA ミニドライバーは、この GUID を割り当てて、BDA ネットワークプロバイダーフィルターを作成するように指定します。

<span id="KSCATEGORY_BDA_TRANSPORT_INFORMATION"></span><span id="kscategory_bda_transport_information"></span>KSCATEGORY\_BDA\_TRANSPORT\_情報  
BDA ミニドライバーは、この GUID を割り当てて、BDA トランスポート情報フィルター (TIF) を作成するように指定します。

 

 





