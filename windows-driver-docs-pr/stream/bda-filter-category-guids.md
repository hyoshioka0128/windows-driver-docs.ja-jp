---
title: BDA フィルター カテゴリの GUID
description: BDA フィルター カテゴリの GUID
ms.assetid: fbd4bf91-8309-423a-97ea-7e4f90cd3b68
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7f9d1e033ac03dc8b6e124a5568efbe18ed20a5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386689"
---
# <a name="bda-filter-category-guids"></a>BDA フィルター カテゴリの GUID


## <span id="ddk_bda_filter_category_guids_ks"></span><span id="DDK_BDA_FILTER_CATEGORY_GUIDS_KS"></span>


BDA ミニドライバーでは、BDA フィルター カテゴリ Guid を使用して、作成する BDA フィルターの種類を指定します。 BDA ミニドライバーこれら Guid の割り当て先の配列、**カテゴリ**のメンバー、 [ **KSFILTER\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksfilter_descriptor)ポイントを構造体します。 *Bdamedia.h*ヘッダー ファイルには、これらの Guid が定義されています。

次のフィルターのカテゴリの Guid を BDA 使用できます。

<span id="KSCATEGORY_BDA_RECEIVER_COMPONENT"></span><span id="kscategory_bda_receiver_component"></span>KSCATEGORY\_BDA\_受信者\_コンポーネント  
BDA ミニドライバーは、BDA 受信者フィルターを作成するを指定するには、この GUID を割り当てます。

<span id="KSCATEGORY_BDA_NETWORK_TUNER"></span><span id="kscategory_bda_network_tuner"></span>KSCATEGORY\_BDA\_ネットワーク\_チューナー  
BDA ミニドライバーは、BDA ネットワーク チューナー フィルターを作成するを指定するには、この GUID を割り当てます。

<span id="KSCATEGORY_BDA_NETWORK_EPG"></span><span id="kscategory_bda_network_epg"></span>KSCATEGORY\_BDA\_ネットワーク\_EPG  
BDA ミニドライバーは、BDA 電子番組ガイド (EPG) フィルターを作成するを指定するには、この GUID を割り当てます。

<span id="KSCATEGORY_BDA_IP_SINK"></span><span id="kscategory_bda_ip_sink"></span>KSCATEGORY\_BDA\_IP\_シンク  
BDA ミニドライバーは、シンク BDA IP フィルターを作成するを指定するには、この GUID を割り当てます。

<span id="KSCATEGORY_BDA_NETWORK_PROVIDER"></span><span id="kscategory_bda_network_provider"></span>KSCATEGORY\_BDA\_ネットワーク\_プロバイダー  
BDA ミニドライバーは、BDA ネットワーク プロバイダーのフィルターを作成するを指定するには、この GUID を割り当てます。

<span id="KSCATEGORY_BDA_TRANSPORT_INFORMATION"></span><span id="kscategory_bda_transport_information"></span>KSCATEGORY\_BDA\_トランスポート\_情報  
BDA ミニドライバーは、フィルターを作成する BDA トランスポート情報 (TIF) を指定するには、この GUID を割り当てます。

 

 





