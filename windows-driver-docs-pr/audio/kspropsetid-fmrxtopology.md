---
title: KSPROPSETID\_FMRXTopology
description: KSPROPSETID\_FMRXTopology プロパティ セットは、FM ラジオ プロパティを設定するために使用します。
ms.assetid: 66ACE82D-F0C2-4BF8-9B16-8A1B3A2C05E0
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5adc0f31ca156727332ec9664cda43ef8ef7e98
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332486"
---
# <a name="kspropsetidfmrxtopology"></a>KSPROPSETID\_FMRXTopology


`KSPROPSETID_FMRXTopology`プロパティ セットは、FM ラジオ プロパティを設定するために使用します。

`KSPROPSETID_FMRXTopology`プロパティ セットには、次のプロパティが含まれています。

-   [**KSPROPERTY\_FMRX\_ANTENNAENDPOINTID**](ksproperty-fmrx-antennaendpointid.md)

-   [**KSPROPERTY\_FMRX\_ENDPOINTID**](ksproperty-fmrx-endpointid.md)

-   [**KSPROPERTY\_FMRX\_ボリューム**](ksproperty-fmrx-volume.md)

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


FM ラジオを有効または、設定を無効になっている、 [ **KSPROPERTY\_FMRX\_状態**](ksproperty-fmrx-state.md) wave フィルターのプロパティ。 FM ボリュームとルーティング (エンドポイントの選択) によって制御されます、 [ **KSPROPERTY\_FMRX\_ボリューム**](ksproperty-fmrx-volume.md)と[ **KSPROPERTY\_FMRX\_ENDPOINTID** ](ksproperty-fmrx-endpointid.md)トポロジ フィルターのプロパティ。 基本的なサポート、 **KSPROPERTY\_FMRX\_ボリューム**プロパティは、最小のボリューム、最大のボリュームとボリュームの範囲を返す必要があります。

新しい[ **KSNODETYPE\_FM\_RX** ](ksnodetype-fm-rx.md)システムでは、他のオーディオ エンドポイントがあり、すべてのオーディオのエンドポイント プロパティがサポートしているトポロジ ノードのエンドポイントが実装されます。 このエンドポイントで定義されている回線のモジュラー ジャック プロパティもサポートしています。、 [KSPROPSETID\_ジャック](kspropsetid-jack.md)プロパティ セット。 このエンドポイントは起動時に接続されていない状態です。 FM ラジオをキャプチャすると、ドライバーでサポートされて、このエンドポイントがアクティブになります FM ラジオが有効にするとします。 ピン留め、キャプチャの作成、 **KSNODETYPE\_FM\_RX**トポロジのノードでは、FM 受信者から経由で送信されるオーディオ キャプチャします。

 

 





