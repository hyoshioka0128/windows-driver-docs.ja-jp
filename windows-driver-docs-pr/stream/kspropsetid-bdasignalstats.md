---
title: KSPROPSETID\_BdaSignalStats
description: KSPROPSETID\_BdaSignalStats
ms.assetid: ea368344-e56d-47d1-bc1f-241ba8aa0bc4
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d203b775bb3c4b29e31bd2cf9b7a1168efbfddef
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391389"
---
# <a name="kspropsetidbdasignalstats"></a>KSPROPSETID\_BdaSignalStats


## <span id="ddk_kspropsetid_bdasignalstats_ks"></span><span id="DDK_KSPROPSETID_BDASIGNALSTATS_KS"></span>


KSPROPSETID\_BdaSignalStats は BDA 信号の統計情報のプロパティ セット。 制御ノードまたは pin からシグナルの統計を取得に使用されます。

次のプロパティを使用できます。

<span id="KSPROPERTY_BDA_SIGNAL_STRENGTH"></span><span id="ksproperty_bda_signal_strength"></span>[**KSPROPERTY\_BDA\_信号\_強度**](ksproperty-bda-signal-strength.md)必要です。
MDb (デシベル (DB) の 1/1000) でのシグナルの運送業者の強さを示します。
<span id="KSPROPERTY_BDA_SIGNAL_QUALITY"></span><span id="ksproperty_bda_signal_quality"></span>[**KSPROPERTY\_BDA\_信号\_品質**](ksproperty-bda-signal-quality.md)必要です。
割合で示した信号から正常に抽出されたデータの量を示します。
<span id="KSPROPERTY_BDA_SIGNAL_PRESENT"></span><span id="ksproperty_bda_signal_present"></span>[**KSPROPERTY\_BDA\_信号\_存在**](ksproperty-bda-signal-present.md)必要です。
シグナル通信事業者が存在するかどうかを示します。
<span id="KSPROPERTY_BDA_SIGNAL_LOCKED"></span><span id="ksproperty_bda_signal_locked"></span>[**KSPROPERTY\_BDA\_信号\_ロック**](ksproperty-bda-signal-locked.md)必要です。
シグナルをロックできるかどうかを示します。
<span id="KSPROPERTY_BDA_SAMPLE_TIME"></span><span id="ksproperty_bda_sample_time"></span>[**KSPROPERTY\_BDA\_サンプル\_時間**](ksproperty-bda-sample-time.md)省略可能です。
レベルと品質を平均する信号をサンプル時間を示します。
<span id="KSPROPERTY_BDA_SIGNAL_LOCK_CAPS"></span><span id="ksproperty_bda_signal_lock_caps"></span>[**KSPROPERTY\_BDA\_信号\_ロック\_CAP** ](ksproperty-bda-signal-lock-caps.md)必要です。
ロックの種類のシグナル、ドライバーがサポートできることを示します。
<span id="KSPROPERTY_BDA_SIGNAL_LOCK_TYPE"></span><span id="ksproperty_bda_signal_lock_type"></span>[**KSPROPERTY\_BDA\_信号\_ロック\_型**](ksproperty-bda-signal-lock-type.md)必要です。
シグナルの現在のロックの種類を示します。
### <a name="comments"></a>コメント

KSPROPSETID の特定のプロパティを指定するときに\_BdaSignalStats プロパティが、暗証番号 (pin) からシグナルの統計情報を取得する設定の設定、 **NodeId** KSP のメンバー\_− 1 のノードの構造体。

 

 





