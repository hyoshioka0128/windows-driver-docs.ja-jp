---
title: KSNODETYPE\_テレフォニー\_双方向
description: KSNODETYPE\_テレフォニー\_双方向のノードが電話の呼び出しの両方の側 (双方向) を表します。
ms.assetid: 748AC39F-0C15-44A3-BF7B-109A1CB7D145
keywords:
- KSNODETYPE_TELEPHONY_BIDI オーディオ デバイス
topic_type:
- apiref
api_name:
- KSNODETYPE_TELEPHONY_BIDI
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b074cdf5a6c501fdea8713461012769e3ce45362
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333123"
---
# <a name="ksnodetypetelephonybidi"></a>KSNODETYPE\_テレフォニー\_双方向


KSNODETYPE\_テレフォニー\_双方向のノードが電話の呼び出しの両方の側 (双方向) を表します。

デバイスをサポートし、携帯電話のテレフォニー、KSNODETYPE 場合\_テレフォニー\_双方向エンドポイント プロバイダーごとに (実行プログラム) が必要です。

## <a name="span-idcellulartelephonyspanspan-idcellulartelephonyspancellular-telephony"></a><span id="CELLULAR_TELEPHONY__"></span><span id="cellular_telephony__"></span>携帯電話のテレフォニー


ラジオ スタックでは、特定のハードウェア パスに電話の呼び出しのインスタンスを接続するには、プロバイダー Id (実行プログラム Id) と呼び出しの種類 (パケット/回線) の概念があります。

ドライバーは、wave フィルターには、プロバイダー Id を関連付けます。 このプロバイダーの Id は、関連付けられている携帯電話がストリーミング エンドポイントにも設定されます。 実行時に、wave フィルターのプロバイダー Id は変更はできません。 使用して、ドライバーからのプロバイダー Id をクエリは、オーディオ スタック[ **KSPROPERTY\_テレフォニー\_PROVIDERID**](ksproperty-telephony-providerid.md)します。 その後、そのプロバイダー Id のすべての呼び出しは、特定のウェーブ フィルターに送信されます。

**最初と最後の携帯電話の呼び出し**

開始と停止呼び出しが送信することによって行われます[ **KSPROPERTY\_テレフォニー\_CALLCONTROL** ](ksproperty-telephony-callcontrol.md)プロバイダーのウェーブのフィルター処理します。 このプロパティは、呼び出しの種類 (パケット切り替え/回線交換) の通信は、ドライバーの管理操作 (有効または無効にする) を呼び出します。 呼び出しの種類には、呼び出しの制御操作が無効にする場合は無視されます。

呼び出しを有効にすると、KSNODETYPE を関連付けられている\_テレフォニー\_双方向のジャックの状態がアクティブになったに、状態を更新、ドライバーと、呼び出しによって*テレフォニー\_CALLSTATE\_有効*. 呼び出しが終了し、エンドポイントのジャックの状態に接続されていない変更して、呼び出しの状態に更新されます*テレフォニー\_CALLSTATE\_無効*します。

 

 





