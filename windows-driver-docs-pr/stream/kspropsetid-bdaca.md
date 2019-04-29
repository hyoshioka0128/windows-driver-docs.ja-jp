---
title: KSPROPSETID\_BdaCA
description: KSPROPSETID\_BdaCA
ms.assetid: 2ceb54ff-f111-4cf7-8c8e-f9a4dce42d4e
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 790b4723cbffc05290e133012bc211f4bd822e74
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389234"
---
# <a name="kspropsetidbdaca"></a>KSPROPSETID\_BdaCA


## <span id="ddk_kspropsetid_bdaca_ks"></span><span id="DDK_KSPROPSETID_BDACA_KS"></span>


KSPROPSETID\_BdaCA は BDA 条件付きアクセス (CA) のプロパティ セット。 これらのノードの状態と関連付けられている CA モジュールとスマート カード リーダーの状態の権利コントロール メッセージ (ECM) マップ ノードをクエリに使用されます。 このプロパティ セットは、CA プラグインが表示および ECM マップのノードを使用して処理するプログラムへのアクセスを制御できる、ユーザー インターフェイス (UI) のクエリもできます。

次のプロパティを使用できます。

<span id="KSPROPERTY_BDA_ECM_MAP_STATUS"></span><span id="ksproperty_bda_ecm_map_status"></span>[**KSPROPERTY\_BDA\_ECM\_マップ\_状態**](ksproperty-bda-ecm-map-status.md)  
ECM のマップ ノードの状態を返します。

<span id="KSPROPERTY_BDA_CA_MODULE_STATUS"></span><span id="ksproperty_bda_ca_module_status"></span>[**KSPROPERTY\_BDA\_CA\_モジュール\_状態**](ksproperty-bda-ca-module-status.md)  
ECM のマップ ノードに関連付けられた CA モジュールのステータスを返します。

<span id="KSPROPERTY_BDA_CA_SMART_CARD_STATUS"></span><span id="ksproperty_bda_ca_smart_card_status"></span>[**KSPROPERTY\_BDA\_CA\_スマート\_カード\_状態**](ksproperty-bda-ca-smart-card-status.md)  
ECM のマップ ノードに関連付けられているスマート カード リーダーの状態を返します。

<span id="KSPROPERTY_BDA_CA_MODULE_UI"></span><span id="ksproperty_bda_ca_module_ui"></span>[**KSPROPERTY\_BDA\_CA\_モジュール\_UI**](ksproperty-bda-ca-module-ui.md)  
CA プラグインを表示できる UI を返します。

<span id="KSPROPERTY_BDA_CA_SET_PROGRAM_PIDS"></span><span id="ksproperty_bda_ca_set_program_pids"></span>[**KSPROPERTY\_BDA\_CA\_設定\_プログラム\_PID**](ksproperty-bda-ca-set-program-pids.md)  
特定のプログラムでは、パケットの識別子のリストを設定します。

<span id="KSPROPERTY_BDA_CA_REMOVE_PROGRAM"></span><span id="ksproperty_bda_ca_remove_program"></span>[**KSPROPERTY\_BDA\_CA\_削除\_プログラム**](ksproperty-bda-ca-remove-program.md)  
特定のプログラムにアクセスできなくなります。

### <a name="comments"></a>コメント

このプロパティ セット内のプロパティは、KSEVENTSETID 内のイベントに対応\_BdaCAEvent イベントのセット。 BDA ミニドライバーは、このイベントは、CA プラグインに通知するセット内のイベントを通知します。 これらの CA プラグイン KSPROPSETID で対応するプロパティをクエリし、\_BdaCA します。 BDA ミニドライバー信号これらのイベントか、重大な状態の変更が発生するたびにユーザーを操作します。 ユーザーにメッセージを表示するかをユーザーのトランザクションをネゴシエートする、BDA ミニドライバーはたとえば、ユーザーと対話します。 たとえば、ユーザーがスマート カード リーダーからスマート カードを削除時に重大な状態の変更です。

### <a name="see-also"></a>関連項目

[KSEVENTSETID\_BdaCAEvent](kseventsetid-bdacaevent.md)

 

 





