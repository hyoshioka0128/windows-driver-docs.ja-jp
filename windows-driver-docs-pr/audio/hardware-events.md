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
ms.openlocfilehash: 80ab7daffaa0d727dc11618042067e8d7505c249
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537971"
---
# <a name="hardware-events"></a>ハードウェア イベント


## <span id="hardware_events"></span><span id="HARDWARE_EVENTS"></span>


一部のオーディオ デバイスは、ハードウェア ボリューム コントロール ノブ、ミュート スイッチ、または他の種類の手動のコントロールを提供します。 アプリケーションは、音量を調節するオーディオ ストリームを再生する方法を変更したりして、これらのコントロールでの変更に応答できます。 ミニポート ドライバーを使用して、ユーザーは、ハードウェアの制御を調整するときに、 [IPortEvents](https://msdn.microsoft.com/library/windows/hardware/ff536884)ポート ドライバー ハードウェア イベントが発生したことを通知するインターフェイス。 デバイスから、新しいコントロールの設定を読み取ることができるように、ポート、ドライバーはさらに、イベントのアプリケーションを通知します。

ミニポート ドライバーは、ポートのドライバーにクエリを実行、 **IPortEvents**時サービスを提供するインターフェイス、 **Init**呼び出し (を参照してください[ **IMiniportWavePci::Init**](https://msdn.microsoft.com/library/windows/hardware/ff536734)など) ポート ドライバーから。 Microsoft Windows 98 SE Windows Me、および Windows 2000 以降でそのクエリは成功します。 コード例では、Sb16 サンプル オーディオ アダプターで、Windows Driver Kit (WDK) を参照してください。

ポートのドライバーがドライバーを呼び出すときに[ **IMiniport::GetDescription** ](https://msdn.microsoft.com/library/windows/hardware/ff536765)メソッド、メソッドの出力を[ **PCFILTER\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff537694)デバイスをサポートするイベントをその他のものを指定する構造体。 オートメーションのテーブル内のイベントを指定できます、**ピン**と**ノード**PCFILTER のメンバー\_記述子、し、 **AutomationTable**メンバーこれは、フィルター自体のオートメーション テーブルをポイントします。 各イベントがで指定された、 [ **PCEVENT\_項目**](https://msdn.microsoft.com/library/windows/hardware/ff537692)構造体。 ドライバーは、PCEVENT を設定する必要があります\_項目構造体の**設定**と**Id**メンバー [KSEVENTSETID\_AudioControlChange](https://msdn.microsoft.com/library/windows/hardware/ff537122)と[**KSEVENT\_コントロール\_変更**](https://msdn.microsoft.com/library/windows/hardware/ff537128)、ドライバーへのポインターを読み込む必要がありますと[ **EventHandler** ](https://msdn.microsoft.com/library/windows/hardware/ff536374)日常的な**ハンドラー**メンバー。 ドライバーは、PCEVENT を設定する必要がありますも\_項目\_フラグ\_BASICSUPPORT ビット、**フラグ**コントロール変更のイベントを示す基本的なメンバーをサポートし、PCEVENTを設定する必要がある\_項目\_フラグ\_ONESHOT や PCEVENT\_項目\_フラグ\_を 1 回限りまたは定期的な通知をサポートしていることを示すために bits を有効にします。

後でアプリケーションを呼び出すと、 **mixerOpen**ポート、ドライバーは、特定のイベントの通知を要求する (Microsoft Windows SDK のドキュメントで説明) を関数呼び出しのドライバーの**EventHandler**へのポインターとルーチンを[ **PCEVENT\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff537693)構造体。 この構造体の**動詞**PCEVENT にメンバーが設定されている\_動詞\_を追加し、その**EventItem**メンバーを有効にするイベントを指定します。 PCEVENT\_要求の構造へのポインターも含まれています、 [ **KSEVENT\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/ff561853)構造体には、ドライバーは、システムの非透過データとして扱う必要があります。 イベントを有効にした後、ハンドラーを呼び出す必要があります[ **IPortEvents::AddEventToEventList** ](https://msdn.microsoft.com/library/windows/hardware/ff536886)で同じ KSEVENT\_エントリのポインター。 この呼び出しでは、ハンドラーは、イベントが有効になっていることを確認します。

ハードウェア イベントが発生して、ドライバーの割り込みサービス ルーチンが検出されて、ミュートまたはボリュームの変更には、ドライバーは、呼び出すことによってポート ドライバーにイベントを通知[ **IPortEvents::GenerateEventList** ](https://msdn.microsoft.com/library/windows/hardware/ff536889)イベントを記述するパラメーターのセットを使用します。 たとえば、次の呼び出しでは、ボリュームのライン出力ノードのコントロールの変更について説明します。

```cpp
    pPE->GenerateEventList(NULL, KSEVENT_CONTROL_CHANGE,
                           FALSE, ULONG(-1), TRUE, LINEOUT_VOL);
```

この呼び出し中には、ポート ドライバーは呼び出しパラメーターと一致するすべてのイベントのイベントの一覧を検索し、これらのイベントを監視するクライアントに通知を送信します。 PPE へのポインターは、この例では、 **IPortEvents**オブジェクトとライン出力\_VOL はボリュームのライン出力ノードに、ミニポート ドライバーを割り当てるノードの ID。 (のイベント セットの GUID と前の例の暗証番号 (pin) の ID を使用して) 指定されていないパラメーターは、ワイルドカードとして扱われ、常に、リスト内の対応するパラメーターと一致します。

 

 




