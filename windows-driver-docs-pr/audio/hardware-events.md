---
title: ハードウェア イベント
description: ハードウェア イベント
ms.assetid: b91e02dd-0de4-4de3-ade6-778339ce47a8
keywords:
- オーディオ イベント WDK、ハードウェア
- WDM オーディオ イベント WDK
- ハードウェア イベント WDK オーディオ
- イベントの WDK オーディオ
- 手動で制御イベント WDK オーディオ
- ボリューム コントロール イベントの WDK オーディオ
- スイッチ イベント WDK オーディオをミュートします。
- ポート ドライバー WDK のオーディオ、イベント
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1e6884994244d9ef73f187eae05af53ce94c19c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360005"
---
# <a name="hardware-events"></a>ハードウェア イベント


## <span id="hardware_events"></span><span id="HARDWARE_EVENTS"></span>


一部のオーディオ デバイスは、ハードウェア ボリューム コントロール ノブ、ミュート スイッチ、または他の種類の手動のコントロールを提供します。 アプリケーションは、音量を調節するオーディオ ストリームを再生する方法を変更したりして、これらのコントロールでの変更に応答できます。 ミニポート ドライバーを使用して、ユーザーは、ハードウェアの制御を調整するときに、 [IPortEvents](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportevents)ポート ドライバー ハードウェア イベントが発生したことを通知するインターフェイス。 デバイスから、新しいコントロールの設定を読み取ることができるように、ポート、ドライバーはさらに、イベントのアプリケーションを通知します。

ミニポート ドライバーは、ポートのドライバーにクエリを実行、 **IPortEvents**時サービスを提供するインターフェイス、 **Init**呼び出し (を参照してください[ **IMiniportWavePci::Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepci-init)など) ポート ドライバーから。 Microsoft Windows 98 SE Windows Me、および Windows 2000 以降でそのクエリは成功します。 コード例では、Sb16 サンプル オーディオ アダプターで、Windows Driver Kit (WDK) を参照してください。

ポートのドライバーがドライバーを呼び出すときに[ **IMiniport::GetDescription** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiport-getdescription)メソッド、メソッドの出力を[ **PCFILTER\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ns-portcls-pcfilter_descriptor)デバイスをサポートするイベントをその他のものを指定する構造体。 オートメーションのテーブル内のイベントを指定できます、**ピン**と**ノード**PCFILTER のメンバー\_記述子、し、 **AutomationTable**メンバーこれは、フィルター自体のオートメーション テーブルをポイントします。 各イベントがで指定された、 [ **PCEVENT\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ns-portcls-pcevent_item)構造体。 ドライバーは、PCEVENT を設定する必要があります\_項目構造体の**設定**と**Id**メンバー [KSEVENTSETID\_AudioControlChange](https://docs.microsoft.com/windows-hardware/drivers/audio/kseventsetid-audiocontrolchange)と[**KSEVENT\_コントロール\_変更**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksevent-control-change)、ドライバーへのポインターを読み込む必要がありますと[ **EventHandler** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nc-portcls-pcpfnevent_handler)日常的な**ハンドラー**メンバー。 ドライバーは、PCEVENT を設定する必要がありますも\_項目\_フラグ\_BASICSUPPORT ビット、**フラグ**コントロール変更のイベントを示す基本的なメンバーをサポートし、PCEVENTを設定する必要がある\_項目\_フラグ\_ONESHOT や PCEVENT\_項目\_フラグ\_を 1 回限りまたは定期的な通知をサポートしていることを示すために bits を有効にします。

後でアプリケーションを呼び出すと、 **mixerOpen**ポート、ドライバーは、特定のイベントの通知を要求する (Microsoft Windows SDK のドキュメントで説明) を関数呼び出しのドライバーの**EventHandler**へのポインターとルーチンを[ **PCEVENT\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ns-portcls-_pcevent_request)構造体。 この構造体の**動詞**PCEVENT にメンバーが設定されている\_動詞\_を追加し、その**EventItem**メンバーを有効にするイベントを指定します。 PCEVENT\_要求の構造へのポインターも含まれています、 [ **KSEVENT\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksevent_entry)構造体には、ドライバーは、システムの非透過データとして扱う必要があります。 イベントを有効にした後、ハンドラーを呼び出す必要があります[ **IPortEvents::AddEventToEventList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportevents-addeventtoeventlist)で同じ KSEVENT\_エントリのポインター。 この呼び出しでは、ハンドラーは、イベントが有効になっていることを確認します。

ハードウェア イベントが発生して、ドライバーの割り込みサービス ルーチンが検出されて、ミュートまたはボリュームの変更には、ドライバーは、呼び出すことによってポート ドライバーにイベントを通知[ **IPortEvents::GenerateEventList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportevents-generateeventlist)イベントを記述するパラメーターのセットを使用します。 たとえば、次の呼び出しでは、ボリュームのライン出力ノードのコントロールの変更について説明します。

```cpp
    pPE->GenerateEventList(NULL, KSEVENT_CONTROL_CHANGE,
                           FALSE, ULONG(-1), TRUE, LINEOUT_VOL);
```

この呼び出し中には、ポート ドライバーは呼び出しパラメーターと一致するすべてのイベントのイベントの一覧を検索し、これらのイベントを監視するクライアントに通知を送信します。 PPE へのポインターは、この例では、 **IPortEvents**オブジェクトとライン出力\_VOL はボリュームのライン出力ノードに、ミニポート ドライバーを割り当てるノードの ID。 (のイベント セットの GUID と前の例の暗証番号 (pin) の ID を使用して) 指定されていないパラメーターは、ワイルドカードとして扱われ、常に、リスト内の対応するパラメーターと一致します。

 

 




