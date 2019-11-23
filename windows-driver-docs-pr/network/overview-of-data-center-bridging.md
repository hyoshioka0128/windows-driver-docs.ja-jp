---
title: データ センター ブリッジングの概要
description: データ センター ブリッジングの概要
ms.assetid: FEB3FDBB-8A3C-4907-A6D0-CB5E94BCFEFF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b5b7d6562551d0b4f3267d57a60f2a4aacfb4ba
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843747"
---
# <a name="overview-of-data-center-bridging"></a>データ センター ブリッジングの概要


IEEE 802.1 データセンターブリッジング (DCB) は、ローカルエリアネットワーク (LAN) および記憶域ネットワーク (SAN) テクノロジ用の統合802.3 イーサネットメディアインターフェイス (*ファブリック*) を定義する標準のコレクションです。 DCB は、現在の802.1 ブリッジング仕様を拡張して、データセンター内の同じネットワークファブリックにおける LAN ベースおよび SAN ベースのアプリケーションの共存をサポートします。 DCB は、パケットの損失を防ぐリンクレベルのポリシーを定義することで、ファイバーチャネル over Ethernet (FCoE) や iSCSI などのテクノロジもサポートしています。

DCB は、統合されたデータセンターファブリック内でネットワークデバイスを相互運用する方法を指定する、次の802.1 ドラフト標準で構成されています。

<a href="" id="priority-based-flow-control--pfc-"></a>優先順位ベースのフロー制御 (PFC)  
PFC は、IEEE 802.1 Qbb draft 標準で指定されています。 この標準は、DCB インターフェイスのフレームワークの一部です。

PFC では、輻輳に起因するパケット損失を大幅に削減することで、データの信頼性の高い配信がサポートされます。 これにより、FCoE などの損失の影響を受けるプロトコルは、同一の統合されたファブリックを介して、従来の損失を区別しないプロトコルと共存させることができます。

PFC は、直接接続されているピア間のリンクレベルのフロー制御メカニズムを指定します。 PFC は IEEE 802.3 の一時停止フレームに似ていますが、代わりに個別の 802.1 p 優先度レベルで動作します。 これにより、受信者は任意の優先度レベルでトランスミッタを一時停止できます。

PFC の詳細については、「[優先順位ベースのフロー制御 (pfc)](priority-based-flow-control--pfc.md)」を参照してください。

<a href="" id="enhanced-transmission-selection--ets-"></a>拡張転送の選択 (送信)  
TSA は、IEEE 802.1 Qaz draft 標準で指定されている伝送選択アルゴリズム () です。 この標準は、DCB インターフェイスのフレームワークの一部です。

変更すると、異なる IEEE 802.1 p 優先度レベルに割り当てられているトラフィッククラス間に帯域幅が割り当てられます。 各 traffic クラスには、直接接続されているピア間のデータリンクで使用可能な帯域幅の割合が割り当てられます。 トラフィッククラスで割り当てられた帯域幅が使用されていない場合は、トラフィッククラスが使用していない帯域幅を他のトラフィッククラスが使用できるようにします。

設定の詳細については、「 [Enhanced 伝送選択 (送信) アルゴリズム](enhanced-transmission-selection--ets--algorithm.md)」を参照してください。

<a href="" id="data-center-bridging-exchange--dcbx--protocol"></a>Data Center ブリッジング Exchange (DCBX) プロトコル  
Data Center ブリッジング Exchange (DCBX) プロトコルは、IEEE 802.1 Qaz draft standard でも指定されています。 DCBX では、2つの directconnected ピア間で DCB 構成パラメーターを交換できます。 これにより、これらのピアは、サービスの品質 (QoS) パラメーターを調整および調整して、接続を介したデータ転送を最適化することができます。

DCBX は、ネットワークアダプター (*ローカルピア*) とリモートピア間の競合する QoS パラメーター設定を検出するためにも使用されます。 ローカルおよびリモートの QoS パラメーター設定に基づき、ミニポートドライバーは競合を解決し、一連の動作 QoS パラメーターを派生します。 ネットワークアダプターは、これらの操作パラメーターを使用して、リモートピアにパケットを優先的に送信します。 ドライバーが動作している NDIS QoS パラメーター設定を解決する方法の詳細については、「[運用 Ndis Qos パラメーターの解決](resolving-operational-ndis-qos-parameters.md)」を参照してください。

DCBX は、DCB (TLV) の設定で構成されます。この設定は、リンク層検出プロトコル (LLDP) パケットを介して実行されます。 LLDP は、IEEE 802.1 AB-2005 標準で指定されています。

  DCBX は、ローカルピアが特定の時点で1つのリモートピアからの構成パラメーターのみを保持**することを**指定します。 その結果、ネットワークアダプターで保持されるのは、ローカル、リモート、および運用 NDIS の1つの QoS パラメーターのセットだけです。

 

各トラフィッククラスと PFC 構成設定は、IEEE 802.1 p 優先度レベルに関連付けられています。 優先度レベルは、パケットの 802.1 Q タグ内の3ビット値として指定されます。 NDIS パケットの場合、802.1 p 優先度レベルは、パケットの[**net\_buffer\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造に関連付けられている[**ndis\_net\_buffer\_List\_8021Q\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_net_buffer_list_8021q_info)構造体の**userpriority**メンバーによって指定されます。

優先度レベルの詳細については、「 [IEEE 802.1 p Priority levels](ieee-802-1p-priority-levels.md)」を参照してください。

 

 





