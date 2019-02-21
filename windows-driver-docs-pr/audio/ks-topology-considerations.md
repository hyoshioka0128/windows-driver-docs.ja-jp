---
title: KS トポロジに関する考慮事項
description: KS トポロジに関する考慮事項
ms.assetid: 81a2a41a-2a10-4de0-9a64-2c8f86a0c96d
keywords:
- 非 PCM のオーディオ形式の WDK、KS トポロジ
- ブリッジ ピン WDK オーディオ
- API の WDK オーディオ ミキサー
- KS は、WDK オーディオ、wave 形式の非 PCM をフィルター処理します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c783e80f14b13c4035474470f0ffa11442d83b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551459"
---
# <a name="ks-topology-considerations"></a>KS トポロジに関する考慮事項


## <span id="ks_topology_considerations"></span><span id="KS_TOPOLOGY_CONSIDERATIONS"></span>


[WDMAud システム ドライバー](user-mode-wdm-audio-components.md#wdmaud_system_driver) (Wdmaud.sys) を通じて公開されているレガシ ミキサー行 KS フィルター トポロジに変換、**ミキサー** API。 SRC 行に対応する非 PCM pin (MIXERLINE\_COMPONENTTYPE\_SRC\_*XXX*) ミキサー API でします。 この pin が最終的に、PCM 以外のデータは専用のブリッジ pin (エンドポイントで、グラフの物理接続) に流入するデータ パスにある場合、**ミキサー** API は、追加の DST ライン (MIXERLINEとしてブリッジの暗証番号(pin)を公開します。\_COMPONENTTYPE\_DST\_*XXX*)、PCM のデータの DST の線とは別です。 これによって表示されるコントロールに不要な複雑さを追加することができます、**ミキサー**SndVol32 ユーティリティの交換などの API のクライアント。

この方法で非 PCM 暗証番号 (pin) を公開しないようにする場合、1 つは、PCM のデータ パスによって共有されている合計ノードにフィードのデータ パスが最終的に、暗証番号 (pin) を格納していることを確認します。 つまり、PCM 夏時間のない行をメインの DST の行に参加させます。 残念ながら、この回避策は、本物のハードウェア トポロジを偽って示す、合計ノードからのダウン ストリーム ノードを通じて、PCM 以外のデータ ストリームを制御しようとするクライアントの将来の問題を生じる可能性があります。 優れたアプローチが変更するのには、**ミキサー**-API クライアント コントロールを持たない src 属性と DST の行を無視します。

使用する場合、 [KsStudio ユーティリティ](ksstudio-utility.md)KSCATEGORY で wave フィルターを表示する\_オーディオ、はず PCM 以外のデータを個別に暗証番号 (pin) を参照してください。 KSCATEGORY 複合システム オーディオのグラフを表示するときに\_オーディオ\_デバイス、PCM のデータ範囲をすべてと共に、メイン wave 出力ピン、PCM 以外のデータ範囲を確認する必要があります。

SysAudio (Sysaudio.sys) Windows Server 2003、Windows XP、Windows 2000、および Windows でシステム オーディオ デバイスをサイトに問題は 98/。 SysAudio KSCATEGORY を生成することに注意してください\_オーディオ\_デバイス自動的には、ドライバーは登録自体手動でこのカテゴリにします。

トポロジのミニポート ドライバーに PCM 以外のデータ パスを接続する必要はありません。 この接続は、PCM 以外のデータ パスがデバイスのトポロジの残りの部分とやり取りする場合にのみの特典はたとえば、一般的なミキサーまたはサンプル レート コンバーターにフィードする場合。 ブリッジの pin、両方のピンが wave ミニポート ドライバー上にあるへのストリーミングに暗証番号 (pin) をたとえば S/PDIF ポートに直接流れるデータ ストリームの非 PCM、有効な完全なトポロジを形成します。

 

 




