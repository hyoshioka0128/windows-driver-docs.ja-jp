---
title: データ センター ブリッジングの概要
description: データ センター ブリッジングの概要
ms.assetid: FEB3FDBB-8A3C-4907-A6D0-CB5E94BCFEFF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2d945df6ce4df8239e7174ab70116953e2611b8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380581"
---
# <a name="overview-of-data-center-bridging"></a>データ センター ブリッジングの概要


IEEE 802.1 データ センター ブリッジング (DCB) は、統合型を定義する標準のコレクションを 802.3 イーサネット メディア インターフェイス、または*fabric*、ローカル エリア ネットワーク (LAN) および記憶域エリア ネットワーク (SAN) のテクノロジ。 DCB は、データ センター内で同じネットワーク ファブリック経由での LAN および SAN ベースのアプリケーションの共存をサポートする仕様をブリッジ現在 802.1 を拡張します。 DCB には、パケット損失を防ぐためリンク レベルのポリシーを定義することで Fibre Channel over Ethernet (FCoE)、iSCSI などのテクノロジもサポートしています。

DCB は、どのネットワーク デバイスを相互運用、統合されたデータ センター ファブリック内で指定する次の 802.1 ドラフト標準で構成されます。

<a href="" id="priority-based-flow-control--pfc-"></a>優先順位に基づくフロー制御 (PFC)  
PFC は IEEE 802.1 qbb で指定されたドラフト標準。 この標準は、DCB インターフェイス用のフレームワークの一部です。

PFC は、混雑により、パケット損失を大幅に減らすことで、データの信頼性の高い配信をサポートします。 これにより、FCoE、同じ統合ファブリック経由で損失を区別しない従来のプロトコルと共存させるなど、損失するプロトコルです。

PFC は、直接接続されているピア間のリンク レベルのフロー制御メカニズムを指定します。 PFC は、IEEE 802.3 PAUSE フレームに似ていますが、代わりに個々 の 802.1p の優先度レベルで動作します。 これにより、受信側が任意の優先度レベルでの送信を一時停止できます。

PFC の詳細については、次を参照してください。[優先度に基づくフロー制御 (PFC)](priority-based-flow-control--pfc.md)します。

<a href="" id="enhanced-transmission-selection--ets-"></a>強化された転送の選択 (ETS)  
ETS は IEEE 802.1 qaz で指定されている伝送選択アルゴリズム (TSA) ドラフト標準。 この標準は、DCB インターフェイス用のフレームワークの一部です。

ETS では、さまざまな IEEE 802.1p の優先度レベルに割り当てられているトラフィック クラス間の帯域幅を割り当てます。 トラフィック クラスごとには、directlyconnected ピア間のデータ リンクで使用できる帯域幅の割合が割り当てられます。 トラフィック クラスでは、その割り当てられた帯域幅を使用しない場合、ETS、トラフィック クラスを使用していない利用可能な帯域幅を使用するには、その他のトラフィック クラスを使用します。

ETS の詳細については、次を参照してください。 [Enhanced Transmission Selection (ETS) アルゴリズム](enhanced-transmission-selection--ets--algorithm.md)します。

<a href="" id="data-center-bridging-exchange--dcbx--protocol"></a>データ センター ブリッジング Exchange (DCBX) プロトコル  
IEEE 802.1 qaz で、Data Center Bridging Exchange (DCBX) プロトコルが指定されてもドラフト標準。 DCBX は、2 つの directlyconnected ピア間で交換される DCB 構成パラメーターを使用できます。 これにより、これらのピアに適応し、接続経由でデータ転送を最適化するためにサービスの品質 (QoS) パラメーターを調整できます。

DCBX はネットワーク アダプター間の競合している QoS パラメーター設定を検出するためにも使用されます (*ローカル ピア*) とリモート ピア。 ローカルおよびリモートの QoS パラメーターの設定に基づき、ミニポート ドライバーは、競合を解決し、一連の運用上の QoS パラメーターを派生します。 ネットワーク アダプターでは、リモート ピアにパケットの優先順位の送信のこれらのオペレーションのパラメーターを使用します。 ドライバーがその運用上の NDIS QoS パラメーター設定を解決する方法の詳細については、次を参照してください。[運用上の NDIS QoS パラメーターを解決する](resolving-operational-ndis-qos-parameters.md)します。

リンク層探索プロトコル (LLDP) パケットで実行される DCB 型の値の長さ (TLV) 設定 DCBX で構成されます。 LLDP が IEEE 802.1AB で指定された-2005 standard。

**注**  DCBX では、ローカル ピアが、特定の時点で 1 つだけのリモート ピアからの構成パラメーターを保持することを指定します。 その結果、ネットワーク アダプターは、ローカル、リモート、および運用上の NDIS QoS パラメーターの 1 つだけのセットを保持します。

 

各トラフィック クラスの ETS と PFC 構成設定は、IEEE 802.1p の優先度レベルに関連付けられます。 優先度レベルは、パケットの内の 3 ビット値として指定 802.1 q タグ。 NDIS パケットの場合、802.1 p の優先度レベルがで指定された、 **UserPriority**のメンバー、 [ **NDIS\_NET\_バッファー\_一覧\_8021Q\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff566565)構造に関連付けられたパケットの[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。

優先度レベルの詳細については、次を参照してください。 [IEEE 802.1p の優先度レベル](ieee-802-1p-priority-levels.md)します。

 

 





