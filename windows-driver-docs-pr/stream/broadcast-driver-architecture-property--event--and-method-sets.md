---
title: ドライバーのアーキテクチャのプロパティ、イベント、およびメソッドのセットをブロードキャストします。
description: ドライバーのアーキテクチャのプロパティ、イベント、およびメソッドのセットをブロードキャストします。
ms.assetid: 4323c19a-e47d-4ec6-a39c-3f2e95c526e4
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c1f6c9ddf7941cc9cd6a2b8a0f68d76d1b1cc9d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529283"
---
# <a name="broadcast-driver-architecture-property-event-and-method-sets"></a>ドライバーのアーキテクチャのプロパティ、イベント、およびメソッドのセットをブロードキャストします。


## <span id="ddk_broadcast_driver_architecture_property_event_and_method_sets_ks"></span><span id="DDK_BROADCAST_DRIVER_ARCHITECTURE_PROPERTY_EVENT_AND_METHOD_SETS_KS"></span>


このセクションでは、BDA ミニドライバーを実装するプロパティ、イベント、およびメソッドのセットを説明します。 これらのセットが定義されている*bdamedia.h*します。 BDA ミニドライバーは、いくつかのプロパティと BDA サポート ライブラリ内の既定の実装にこれらのセット内のメソッドをディスパッチできます。 詳細については、[ドライバー アーキテクチャ ミニドライバーのブロードキャスト](https://msdn.microsoft.com/library/windows/hardware/ff556588)、ミニドライバーが関数の BDA サポート ライブラリを使用して、これらのセットの既定の処理を提供する方法にを参照してください。

次のセクションでは、BDA プロパティ、イベント、およびメソッドのセットの詳細についてを提供します。

<span id="KSPROPSETID_BdaAutodemodulate"></span><span id="kspropsetid_bdaautodemodulate"></span><span id="KSPROPSETID_BDAAUTODEMODULATE"></span>[KSPROPSETID\_BdaAutodemodulate](kspropsetid-bdaautodemodulate.md)  
BDA autodemodulate プロパティでは、自動的に変調された信号の特性を確認および復調が行われずできる信号復調器ノード コントロールを設定します。

<span id="KSPROPSETID_BdaCA"></span><span id="kspropsetid_bdaca"></span><span id="KSPROPSETID_BDACA"></span>[KSPROPSETID\_BdaCA](kspropsetid-bdaca.md)  
BDA 条件付きアクセスのプロパティは、クエリを表示する状態またはユーザーのいずれかのインターフェイス (UI) の利用資格のコントロール メッセージ (ECM) マップ ノードを設定します。

<span id="KSEVENTSETID_BdaCAEvent"></span><span id="kseventsetid_bdacaevent"></span><span id="KSEVENTSETID_BDACAEVENT"></span>[KSEVENTSETID\_BdaCAEvent](kseventsetid-bdacaevent.md)  
BDA 条件付きアクセスのイベント セットには、状態または取得して表示する UI の存在についての変更のいずれかの条件付きアクセス (CA) プラグインに通知します。

<span id="KSMETHODSETID_BdaChangeSync"></span><span id="ksmethodsetid_bdachangesync"></span><span id="KSMETHODSETID_BDACHANGESYNC"></span>[KSMETHODSETID\_BdaChangeSync](ksmethodsetid-bdachangesync.md)  
BDA 変更の同期メソッドのセットは、一度にすべてをフィルターまたはそのピンとノードで複数の変更をコミットします。

<span id="KSMETHODSETID_BdaDeviceConfiguration"></span><span id="ksmethodsetid_bdadeviceconfiguration"></span><span id="KSMETHODSETID_BDADEVICECONFIGURATION"></span>[KSMETHODSETID\_BdaDeviceConfiguration](ksmethodsetid-bdadeviceconfiguration.md)  
BDA デバイスの構成方法のセットは、接続されているフィルターの実際のトポロジを構成します。

<span id="KSPROPSETID_BdaDigitalDemodulator"></span><span id="kspropsetid_bdadigitaldemodulator"></span><span id="KSPROPSETID_BDADIGITALDEMODULATOR"></span>[KSPROPSETID\_BdaDigitalDemodulator](kspropsetid-bdadigitaldemodulator.md)  
BDA デジタル復調器プロパティは、コントロール変調された信号の特性を自動的に判断できない信号復調器のノードを設定します。

<span id="KSPROPSETID_BdaFrequencyFilter"></span><span id="kspropsetid_bdafrequencyfilter"></span><span id="KSPROPSETID_BDAFREQUENCYFILTER"></span>[KSPROPSETID\_BdaFrequencyFilter](kspropsetid-bdafrequencyfilter.md)  
BDA 周波数のフィルター プロパティは、受信側のトポロジでの RF チューナー ノードをコントロールに設定します。

<span id="KSPROPSETID_BdaLNBInfo"></span><span id="kspropsetid_bdalnbinfo"></span><span id="KSPROPSETID_BDALNBINFO"></span>[KSPROPSETID\_BdaLNBInfo](kspropsetid-bdalnbinfo.md)  
BDA 低ノイズ ブロック (LNB) のプロパティ セットは、衛星アンテナの LNB デバイスに関する情報が、RF チューナーを提供します。

<span id="KSPROPSETID_BdaNullTransform"></span><span id="kspropsetid_bdanulltransform"></span><span id="KSPROPSETID_BDANULLTRANSFORM"></span>[KSPROPSETID\_BdaNullTransform](kspropsetid-bdanulltransform.md)  
BDA null 変換のプロパティ セットをそのままの信号を渡すためのノードを通知します。

<span id="KSPROPSETID_BdaPIDFilter"></span><span id="kspropsetid_bdapidfilter"></span><span id="KSPROPSETID_BDAPIDFILTER"></span>[KSPROPSETID\_BdaPIDFilter](kspropsetid-bdapidfilter.md)  
BDA パケット識別子 (PID) のフィルター プロパティは、PID フィルター ノードのコントロールを設定します。 PID フィルター ノードは、受信したブロードキャスト ストリームから不要なストリームをフィルター処理します。

<span id="KSPROPSETID_BdaPinControl"></span><span id="kspropsetid_bdapincontrol"></span><span id="KSPROPSETID_BDAPINCONTROL"></span>[KSPROPSETID\_BdaPinControl](kspropsetid-bdapincontrol.md)  
BDA 暗証番号 (pin) のコントロールのプロパティ セットは、ピン留めすることから、pin のプロパティを取得します。

<span id="KSEVENTSETID_BdaPinEvent"></span><span id="kseventsetid_bdapinevent"></span><span id="KSEVENTSETID_BDAPINEVENT"></span>[KSEVENTSETID\_BdaPinEvent](kseventsetid-bdapinevent.md)  
BDA 暗証番号 (pin) のイベント セットには、他のフィルターまたは pin に関連するイベントのプラグインに通知します。

<span id="KSPROPSETID_BdaSignalStats"></span><span id="kspropsetid_bdasignalstats"></span><span id="KSPROPSETID_BDASIGNALSTATS"></span>[KSPROPSETID\_BdaSignalStats](kspropsetid-bdasignalstats.md)  
BDA 信号の統計情報のプロパティ セットは、制御ノードまたは pin からシグナルの統計情報を取得します。 Pin からシグナルの統計情報を取得する設定、 **NodeId** KSP のメンバー\_− 1 のノードの構造体。

<span id="KSPROPSETID_BdaTableSection"></span><span id="kspropsetid_bdatablesection"></span><span id="KSPROPSETID_BDATABLESECTION"></span>[KSPROPSETID\_BdaTableSection](kspropsetid-bdatablesection.md)  
BDA テーブル セクションのプロパティ セットは、ノードの出力にデータを提供するときに使用するノードにテーブル セクションを提供します。

<span id="KSPROPSETID_BdaTopology"></span><span id="kspropsetid_bdatopology"></span><span id="KSPROPSETID_BDATOPOLOGY"></span>[KSPROPSETID\_BdaTopology](kspropsetid-bdatopology.md)  
BDA トポロジ プロパティの設定では、ノードの機能とフィルター内の接続を取得します。

<span id="KSPROPSETID_BdaVoidTransform"></span><span id="kspropsetid_bdavoidtransform"></span><span id="KSPROPSETID_BDAVOIDTRANSFORM"></span>[KSPROPSETID\_BdaVoidTransform](kspropsetid-bdavoidtransform.md)  
BDA void transform プロパティは、ノードが起動し、動作が停止したときにコントロールを設定します。

**注**   BDA プロパティ、イベント、およびメソッドのセットは、Windows XP で以降。 これらのセットは、そのプラットフォームに DirectX 9.0 以降がインストールされている場合にのみ、Windows 2000 プラットフォームで使用できます。

 

 

 





