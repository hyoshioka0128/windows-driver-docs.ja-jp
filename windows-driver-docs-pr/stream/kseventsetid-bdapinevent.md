---
title: KSEVENTSETID\_BdaPinEvent
description: KSEVENTSETID\_BdaPinEvent
ms.assetid: f81b9973-f4ae-4b39-a4e1-bbaff21c5d41
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fb8e3320e00b1f4985615b20460447d15b85a1f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329648"
---
# <a name="kseventsetidbdapinevent"></a>KSEVENTSETID\_BdaPinEvent


## <span id="ddk_kseventsetid_bdapinevent_ks"></span><span id="DDK_KSEVENTSETID_BDAPINEVENT_KS"></span>


KSEVENTSETID\_BdaPinEvent は BDA 暗証番号 (pin) のイベントのセット。 これは、フィルターまたは特定の pin に関連するイベントの通知を要求するアプリケーションに通知するために使用されます。

次のイベントを使用できます。

<span id="KSEVENT_BDA_PIN_CONNECTED"></span><span id="ksevent_bda_pin_connected"></span>[**KSEVENT\_BDA\_PIN\_接続済み**](ksevent-bda-pin-connected.md)  
Pin が接続されている場合に通知します。

<span id="KSEVENT_BDA_PIN_DISCONNECTED"></span><span id="ksevent_bda_pin_disconnected"></span>[**KSEVENT\_BDA\_PIN\_切断**](ksevent-bda-pin-disconnected.md)  
Pin が切断されたときに通知します。

### <a name="comments"></a>コメント

ネットワーク プロバイダーのフィルターは、このイベントは、これらのイベントが発生すると、pin に関連するイベントの通知の登録にセットを使用します。

BDA ミニドライバーはこのイベント セットを定義していないかどうかは、BDA サポート ライブラリは、暗証番号 (pin) がいずれかで作成されたときにサポートを追加、 **BdaCreatePin**または**BdaInitFilter**関数。

BDA ミニドライバーは、このイベントのセットをその独自のハンドラーを定義する場合、ミニドライバーはこのイベントのフィルターまたは以前の通知を要求するプラグインに通知するセット内のイベントを通知する責任を負います。

 

 





