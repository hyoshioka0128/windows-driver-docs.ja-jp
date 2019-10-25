---
title: ハードウェア イベント
description: ハードウェア イベント
ms.assetid: b91e02dd-0de4-4de3-ade6-778339ce47a8
keywords:
- オーディオイベント WDK、ハードウェア
- WDM オーディオイベント WDK
- ハードウェアイベント WDK オーディオ
- イベント WDK オーディオ
- 手動制御イベントの WDK オーディオ
- ボリュームコントロールイベント WDK オーディオ
- ミュートスイッチイベントの WDK オーディオ
- ポートドライバー WDK オーディオ、イベント
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6505652340196f9e0bf554e8c184bbcb91aec714
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833352"
---
# <a name="hardware-events"></a>ハードウェア イベント


## <span id="hardware_events"></span><span id="HARDWARE_EVENTS"></span>


一部のオーディオデバイスでは、ハードウェアボリュームコントロールのノブ、ミュートスイッチ、またはその他の種類の手動コントロールが提供します。 アプリケーションは、ボリュームを調整するか、オーディオストリームの再生方法を変更することによって、これらのコントロールの変更に応答できます。 ユーザーがハードウェア制御を調整すると、ミニポートドライバーは[Iportevents](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportevents)インターフェイスを使用して、ハードウェアイベントが発生したことをポートドライバーに通知します。 さらに、ポートドライバーは、デバイスから新しいコントロール設定を読み取ることができるように、イベントをアプリケーションに通知します。

ミニポートドライバーは、 **Init**呼び出しを行うときに**iportevents**インターフェイスのポートドライバーに対してクエリを実行できます (たとえば、ポートドライバーからの[**IMiniportWavePci:: init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-init)を参照してください)。 Microsoft Windows 98 SE、Windows Me、および Windows 2000 以降では、このクエリは成功します。 コード例については、Windows Driver Kit (WDK) の Sb16 サンプルオーディオアダプターに関する記述を参照してください。

ポートドライバーがドライバーの[**IMiniport:: GetDescription**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiport-getdescription)メソッドを呼び出すと、メソッドは、デバイスでサポートされているイベントを特に指定する[**PCFILTER\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcfilter_descriptor)構造体を出力します。 イベントは、PCFILTER\_記述子の**ピン**および**ノード**メンバーのオートメーションテーブルで指定できます。また、 **AutomationTable**メンバーでは、フィルター自体のオートメーションテーブルを指します。 各イベントは[**pcevent\_ITEM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcevent_item)構造体によって指定されます。 ドライバーは PCEVENT\_項目構造体の**set**および**Id**メンバーを[KSEVENTSETID\_audiocontrolchange](https://docs.microsoft.com/windows-hardware/drivers/audio/kseventsetid-audiocontrolchange)および KSEVENT に設定する必要があります。これにより[ **\_\_変更が制御**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksevent-control-change)され、ドライバーへのポインターを読み込む必要があります。**ハンドラー**メンバーへの[**EventHandler**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nc-portcls-pcpfnevent_handler)ルーチン。 ドライバーでは、コントロール変更イベントの基本的なサポートを示すために、**フラグ**メンバーに pcevent\_ITEM\_フラグ\_basicsupport bit を設定する必要があります。また、pcevent\_ITEM\_フラグ\_ONESHOT と/に設定する必要があります。または PCEVENT\_ITEM\_\_フラグを有効にすると、1回の繰り返しまたは繰り返しの通知をサポートしていることを示すことができます。

アプリケーションが後で**mixerOpen**関数 (Microsoft Windows SDK ドキュメントで説明されています) を呼び出して特定のイベントの通知を要求した場合、ポートドライバーは、を指すポインターを使用して、 [**ドライバーの EventHandler ルーチンを呼び出します。PCEVENT\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-_pcevent_request)構造体。 この構造体の**動詞**メンバーは pcevent\_verb\_に設定されています。また、 **EventItem**メンバーは、有効にするイベントを指定します。 PCEVENT\_要求構造体には、ドライバーが不透明なシステムデータとして扱う必要がある[**KSEVENT\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksevent_entry)構造へのポインターも含まれています。 イベントを有効にした後、ハンドラーは同じ KSEVENT\_エントリポインターを使用して[**Iportevents:: AddEventToEventList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportevents-addeventtoeventlist)を呼び出す必要があります。 この呼び出しでは、イベントが有効であることがハンドラーによって確認されます。

ハードウェアイベントが発生し、ドライバーの割り込みサービスルーチンによってミュートまたはボリュームの変更が検出されると、ドライバーは、イベントを説明するパラメーターのセットを使用して[**Iportevents:: GenerateEventList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportevents-generateeventlist)を呼び出して、イベントをポートドライバーに通知します。 たとえば、次の呼び出しでは、lineout ノードでのコントロールの変更について説明しています。

```cpp
    pPE->GenerateEventList(NULL, KSEVENT_CONTROL_CHANGE,
                           FALSE, ULONG(-1), TRUE, LINEOUT_VOL);
```

この呼び出しの間、ポートドライバーは、呼び出しパラメーターと一致するすべてのイベントをイベント一覧から検索し、これらのイベントを監視しているクライアントに通知を送信します。 この例では、pPE は**Iportevents**オブジェクトへのポインターであり、LINEOUT\_VOL は、ミニポートドライバーが LINEOUT ノードに割り当てるノード ID です。 指定されていないパラメーター (前の例のイベントセット GUID や pin ID など) は、ワイルドカードとして扱われ、リスト内の対応するパラメーターと常に一致します。

 

 




