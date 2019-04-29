---
title: KSEVENTSETID\_BdaCAEvent
description: KSEVENTSETID\_BdaCAEvent
ms.assetid: e748a8a1-9aa4-41da-8cc2-02beb89a8887
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3dfbec8c4ca8ab6ea88ea93142f49a9312a92438
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329606"
---
# <a name="kseventsetidbdacaevent"></a>KSEVENTSETID\_BdaCAEvent


## <span id="ddk_kseventsetid_bdacaevent_ks"></span><span id="DDK_KSEVENTSETID_BDACAEVENT_KS"></span>


KSEVENTSETID\_BdaCAEvent は BDA 条件付きアクセス (CA) のイベントのセット。 これは、CA プラグインの CA モジュールおよび権利コントロール メッセージ (ECM) マップのノードに関連付けられているスマート カード リーダーの状態の変化の通知に使用されます。 このイベント セットには、CA プラグイン プログラム情報の変更およびそれらのプラグインを取得および表示する必要がありますユーザー インターフェイス (UI) の存在に関する通知もできます。

次のイベントを使用できます。

<span id="KSEVENT_BDA_PROGRAM_FLOW_STATUS_CHANGED"></span><span id="ksevent_bda_program_flow_status_changed"></span>[**KSEVENT\_BDA\_プログラム\_フロー\_状態\_CHANGED**](ksevent-bda-program-flow-status-changed.md)  
プログラム情報の状態を変更した場合に通知します。

<span id="KSEVENT_BDA_CA_MODULE_STATUS_CHANGED"></span><span id="ksevent_bda_ca_module_status_changed"></span>[**KSEVENT\_BDA\_CA\_モジュール\_状態\_CHANGED**](ksevent-bda-ca-module-status-changed.md)  
ECM のマップ ノードに関連付けられた CA モジュールの状態の変更の通知します。

<span id="KSEVENT_BDA_CA_SMART_CARD_STATUS_CHANGED"></span><span id="ksevent_bda_ca_smart_card_status_changed"></span>[**KSEVENT\_BDA\_CA\_スマート\_カード\_状態\_CHANGED**](ksevent-bda-ca-smart-card-status-changed.md)  
ECM のマップ ノードに関連付けられているスマート カード リーダーの状態の変更の通知します。

<span id="KSEVENT_BDA_CA_MODULE_UI_REQUESTED"></span><span id="ksevent_bda_ca_module_ui_requested"></span>[**KSEVENT\_BDA\_CA\_モジュール\_UI\_要求**](ksevent-bda-ca-module-ui-requested.md)  
CA プラグインを取得して表示できる UI の存在を通知します。

### <a name="comments"></a>コメント

このイベントのセット内の各イベントは、KSPROPSETID でプロパティに対応\_BdaCA プロパティ セット。 CA プラグインは、BDA コンポーネントでのイベントが発生したときに通知するように要求します。 BDA ミニドライバーは、このイベントは、CA プラグインに通知するセット内のイベントを通知します。 これらの CA プラグイン KSPROPSETID で対応するプロパティをクエリし、\_BdaCA します。 BDA ミニドライバー信号これらのイベントか、重大な状態の変更が発生するたびにユーザーを操作します。 ユーザーにメッセージを表示するかをユーザーのトランザクションをネゴシエートする、BDA ミニドライバーはたとえば、ユーザーと対話します。 たとえば、ユーザーがスマート カード リーダーからスマート カードを削除時に重大な状態の変更です。

### <a name="see-also"></a>関連項目

[KSPROPSETID\_BdaCA](kspropsetid-bdaca.md)

 

 





