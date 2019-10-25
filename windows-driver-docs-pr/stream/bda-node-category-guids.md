---
title: BDA ノードカテゴリ Guid
description: BDA ノードカテゴリ Guid
ms.assetid: cf439881-d20d-4efc-8ea3-3752e117b14d
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c568b6a9cbc9f5064b0130ed3fef4f47770fefb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840616"
---
# <a name="bda-node-category-guids"></a>BDA ノードカテゴリ Guid


## <span id="ddk_bda_node_category_guids_ks"></span><span id="DDK_BDA_NODE_CATEGORY_GUIDS_KS"></span>


BDA ミニドライバーは、BDA ノードカテゴリ Guid を使用して、作成可能な BDA ノードの種類を指定します。 BDA ミニドライバーは、この Guid のうちの1つを、Ksnode の**型**メンバー [ **\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksnode_descriptor)構造体が指す変数に割り当てます。 これらの Guid は、 *Bdamedia*ヘッダーファイルで定義されています。

ネットワークプロバイダーは、 [\_ksk](kspropsetid-bdatopology.md)プロパティ\_BDA\_NODE\_types プロパティを使用して、bda ミニドライバーから使用可能なノードの種類の一覧を取得しています。 このノード型の一覧は、KSK ノード\_記述子の構造体の配列です。

次のノードカテゴリ Guid は、BDA で使用できます。

<span id="KSNODE_BDA_RF_TUNER"></span><span id="ksnode_bda_rf_tuner"></span>KSNODE\_BDA\_RF\_チューナー  
BDA ミニドライバーは、この GUID を割り当てて、ケーブル、衛星放送、または地上波放送の BDA 無線周波数チューナーノードを指定します。

<span id="KSNODE_BDA_ANALOG_DEMODULATOR"></span><span id="ksnode_bda_analog_demodulator"></span>KSNODE\_BDA\_アナログ\_DEMODULATOR  
BDA ミニドライバーは、この GUID を割り当てて、BDA アナログ型 demodulator ノードを指定します。

<span id="KSNODE_BDA_QAM_DEMODULATOR"></span><span id="ksnode_bda_qam_demodulator"></span>KSNODE\_BDA\_QAM\_DEMODULATOR  
BDA ミニドライバーは、この GUID を割り当てて、デジタルビデオ放送 (DVB-T) ケーブル demodulators の BDA QAM type demodulator ノードを指定します。

<span id="KSNODE_BDA_QPSK_DEMODULATOR"></span><span id="ksnode_bda_qpsk_demodulator"></span>KSNODE\_BDA\_QPSK\_DEMODULATOR  
BDA ミニドライバーは、この GUID を割り当てて、DVB-T demodulators の BDA QPSK 型 demodulator ノードを指定します。

<span id="KSNODE_BDA_8VSB_DEMODULATOR"></span><span id="ksnode_bda_8vsb_demodulator"></span>KSNODE\_BDA\_8VSB\_DEMODULATOR  
BDA ミニドライバーは、この GUID を割り当てて、高度なテレビシステム委員会 (ATSC) 地上波 demodulators 用に BDA 8VSB type demodulator ノードを指定します。

<span id="KSNODE_BDA_COFDM_DEMODULATOR"></span><span id="ksnode_bda_cofdm_demodulator"></span>KSNODE\_BDA\_COFDM\_DEMODULATOR  
BDA ミニドライバーは、DVB-T COFDM の demodulator ノードを指定するために、この GUID を割り当てます。

<span id="KSNODE_BDA_OPENCABLE_POD"></span><span id="ksnode_bda_opencable_pod"></span>KSNODE\_BDA\_OPENCABLE\_ポッド  
BDA ミニドライバーは、この GUID を割り当てて、BDA オープンケーブルポッドノードを指定します。

<span id="KSNODE_BDA_COMMON_CA_POD"></span><span id="ksnode_bda_common_ca_pod"></span>KSNODE\_BDA\_共通\_CA\_ポッド  
BDA ミニドライバーは、この GUID を割り当てて、BDA コモン条件付きアクセスポッドノードを指定します。

<span id="KSNODE_BDA_PID_FILTER"></span><span id="ksnode_bda_pid_filter"></span>KSNODE\_BDA\_PID\_フィルター  
BDA ミニドライバーは、この GUID を割り当てて、BDA パケット識別子 (PID) フィルターノードを指定します。

<span id="KSNODE_BDA_IP_SINK"></span><span id="ksnode_bda_ip_sink"></span>KSNODE\_BDA\_IP\_シンク  
BDA ミニドライバーは、この GUID を割り当てて、BDA IP シンクノードを指定します。

<span id="KSNODE_BDA_ISDB_T_DEMODULATOR"></span><span id="ksnode_bda_isdb_t_demodulator"></span>KSNODE\_BDA\_ISDB\_T\_DEMODULATOR  
BDA ミニドライバーは、DVB-T ISDB の demodulator ノードを指定するために、この GUID を割り当てます。

<span id="KSNODE_BDA_ISDB_S_DEMODULATOR"></span><span id="ksnode_bda_isdb_s_demodulator"></span>KSNODE\_BDA\_ISDB\_S\_DEMODULATOR  
BDA ミニドライバーは、この GUID を割り当てて、DVB-T demodulators の BDA ISDB 型 demodulator ノードを指定します。

 

 





