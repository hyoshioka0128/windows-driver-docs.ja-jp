---
title: BDA ノード カテゴリの GUID
description: BDA ノード カテゴリの GUID
ms.assetid: cf439881-d20d-4efc-8ea3-3752e117b14d
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ffd408ea016f9eb1ffbd0938a1594e06512629ec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574442"
---
# <a name="bda-node-category-guids"></a>BDA ノード カテゴリの GUID


## <span id="ddk_bda_node_category_guids_ks"></span><span id="DDK_BDA_NODE_CATEGORY_GUIDS_KS"></span>


BDA ミニドライバーは、BDA ノード カテゴリの Guid を使用して、作成に使用できる BDA ノードの種類を指定します。 BDA ミニドライバー割り当てますこれらのいずれかの Guid を変数に、**型**のメンバー、 [ **KSNODE\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff563473)ポイントを構造体します。 *Bdamedia.h*ヘッダー ファイルには、これらの Guid が定義されています。

ネットワーク プロバイダーは、KSPROPERTY\_BDA\_ノード\_の型のプロパティ、 [KSPROPSETID\_BdaTopology](kspropsetid-bdatopology.md)から使用できるノード型の一覧を取得するプロパティを設定しますBDA ミニドライバーします。 このノードの種類の一覧が KSNODE の配列\_記述子構造体。

次のノード カテゴリの Guid を BDA 使用できます。

<span id="KSNODE_BDA_RF_TUNER"></span><span id="ksnode_bda_rf_tuner"></span>KSNODE\_BDA\_RF\_チューナー  
BDA ミニドライバーは、ケーブル、衛星、または地上波のブロードキャストの BDA 無線周波数チューナー ノードを指定するには、この GUID を割り当てます。

<span id="KSNODE_BDA_ANALOG_DEMODULATOR"></span><span id="ksnode_bda_analog_demodulator"></span>KSNODE\_BDA\_アナログ\_復調器  
BDA ミニドライバーは、BDA アナログ型復調器ノードを指定するには、この GUID を割り当てます。

<span id="KSNODE_BDA_QAM_DEMODULATOR"></span><span id="ksnode_bda_qam_demodulator"></span>KSNODE\_BDA\_QAM\_復調器  
BDA ミニドライバーに BDA QAM 型復調器のノードのデジタル ビデオのブロードキャスト (DVB) を指定するには、この GUID が割り当てられます-demodulators ケーブルを接続します。

<span id="KSNODE_BDA_QPSK_DEMODULATOR"></span><span id="ksnode_bda_qpsk_demodulator"></span>KSNODE\_BDA\_QPSK\_復調器  
BDA ミニドライバーは、DVB サテライト demodulators の BDA QPSK 型復調器のノードを指定するのには、この GUID を割り当てます。

<span id="KSNODE_BDA_8VSB_DEMODULATOR"></span><span id="ksnode_bda_8vsb_demodulator"></span>KSNODE\_BDA\_8VSB\_復調器  
BDA ミニドライバーは、高度なテレビ システム委員会 (ATSC) の BDA 8VSB 型復調器ノードを指定するには、この GUID を割り当て、地上波 demodulators します。

<span id="KSNODE_BDA_COFDM_DEMODULATOR"></span><span id="ksnode_bda_cofdm_demodulator"></span>KSNODE\_BDA\_COFDM\_復調器  
BDA ミニドライバーは、DVB 地上 demodulators の BDA COFDM 型復調器のノードを指定するのには、この GUID を割り当てます。

<span id="KSNODE_BDA_OPENCABLE_POD"></span><span id="ksnode_bda_opencable_pod"></span>KSNODE\_BDA\_OPENCABLE\_ポッド  
BDA ミニドライバーは、BDA オープン ケーブル ポッド ノードを指定するには、この GUID を割り当てます。

<span id="KSNODE_BDA_COMMON_CA_POD"></span><span id="ksnode_bda_common_ca_pod"></span>KSNODE\_BDA\_共通\_CA\_ポッド  
BDA ミニドライバーは、BDA の共通の条件付きアクセスのポッド ノードを指定するには、この GUID を割り当てます。

<span id="KSNODE_BDA_PID_FILTER"></span><span id="ksnode_bda_pid_filter"></span>KSNODE\_BDA\_PID\_フィルター  
BDA ミニドライバーは、BDA パケット識別子 (PID) のフィルター ノードを指定するには、この GUID を割り当てます。

<span id="KSNODE_BDA_IP_SINK"></span><span id="ksnode_bda_ip_sink"></span>KSNODE\_BDA\_IP\_シンク  
BDA ミニドライバーは、シンク ノード BDA IP を指定するには、この GUID を割り当てます。

<span id="KSNODE_BDA_ISDB_T_DEMODULATOR"></span><span id="ksnode_bda_isdb_t_demodulator"></span>KSNODE\_BDA\_ISDB\_T\_復調器  
BDA ミニドライバーは、DVB 地上 demodulators の BDA ISDB 型復調器のノードを指定するのには、この GUID を割り当てます。

<span id="KSNODE_BDA_ISDB_S_DEMODULATOR"></span><span id="ksnode_bda_isdb_s_demodulator"></span>KSNODE\_BDA\_ISDB\_S\_復調器  
BDA ミニドライバーは、DVB サテライト demodulators の BDA ISDB 型復調器のノードを指定するのには、この GUID を割り当てます。

 

 





