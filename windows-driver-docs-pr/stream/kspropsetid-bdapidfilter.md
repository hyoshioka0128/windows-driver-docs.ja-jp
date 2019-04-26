---
title: KSPROPSETID\_BdaPIDFilter
description: KSPROPSETID\_BdaPIDFilter
ms.assetid: 9a2655cb-d7e9-4f61-803a-63fe3fd3501b
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea85c0951b86dc4dbd79844ce3043acd164a1711
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358508"
---
# <a name="kspropsetidbdapidfilter"></a>KSPROPSETID\_BdaPIDFilter


## <span id="ddk_kspropsetid_bdapidfilter_ks"></span><span id="DDK_KSPROPSETID_BDAPIDFILTER_KS"></span>


KSPROPSETID\_BdaPIDFilter は BDA パケット識別子 (PID) フィルターのプロパティ セット。 受信したブロードキャスト MPEG2 トランスポート ストリームから不要なサブストリームをフィルター処理に使用されます。 このプロパティは、PID フィルター ノードのプロパティをコントロールに設定します。

次のプロパティを使用できます。

<span id="KSPROPERTY_BDA_PIDFILTER_MAP_PIDS"></span><span id="ksproperty_bda_pidfilter_map_pids"></span>[**KSPROPERTY\_BDA\_PIDFILTER\_マップ\_PID**](ksproperty-bda-pidfilter-map-pids.md)  
ダウン ストリームのフィルターまたはノードに渡す必要があるトランスポート ストリームのパケットの MPEG2 Pid の一覧については、PID フィルター ノードを通知します。

<span id="KSPROPERTY_BDA_PIDFILTER_UNMAP_PIDS"></span><span id="ksproperty_bda_pidfilter_unmap_pids"></span>[**KSPROPERTY\_BDA\_PIDFILTER\_UNMAP\_PID**](ksproperty-bda-pidfilter-unmap-pids.md)  
特定の Pid を入力ストリームからフィルターで識別されるパケットに関する PID フィルター ノードに通知します。

<span id="KSPROPERTY_BDA_PIDFILTER_LIST_PIDS"></span><span id="ksproperty_bda_pidfilter_list_pids"></span>[**KSPROPERTY\_BDA\_PIDFILTER\_一覧\_PID**](ksproperty-bda-pidfilter-list-pids.md)  
PID フィルター ノードを出力ストリームに入力ストリームから提供されたパケットのグループを識別する Pid の配列を返します。

 

 





