---
title: HYPER-V 拡張可能なスイッチ ポートにパケットを転送
description: HYPER-V 拡張可能なスイッチ ポートにパケットを転送
ms.assetid: C8DA9064-21EE-45F4-BE6D-D24851C5480B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8e442f6952efd52db3152a61760e725ee0674ae
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528716"
---
# <a name="forwarding-packets-to-hyper-v-extensible-switch-ports"></a>HYPER-V 拡張可能なスイッチ ポートにパケットを転送


このページでは、転送拡張機能、HYPER-V 拡張可能スイッチが 1 つまたは複数のポートにパケットを転送する方法について説明します。 この種類の拡張機能は、拡張可能スイッチの外部ネットワーク アダプターに接続されている個々 のネットワーク アダプターにパケットを転送することができますも。

**注**  だけで拡張可能スイッチ転送拡張機能または拡張可能スイッチ自体は拡張可能スイッチ ポートにパケットを転送できます。

 

**注**  このページは、情報とでのダイアグラムに精通していることを前提としています。 [Hyper-v 拡張可能スイッチの概要](overview-of-the-hyper-v-extensible-switch.md)と[ハイブリッド転送](hybrid-forwarding.md)します。

 

**注**  、拡張可能スイッチのインターフェイスで NDIS フィルター ドライバーと呼ばれる*拡張可能スイッチの拡張機能*と呼ばれるドライバー スタック、*拡張可能スイッチ ドライバー スタック*. 拡張機能の詳細については、[Hyper-v 拡張可能スイッチ拡張機能](hyper-v-extensible-switch-extensions.md)を参照してください。

 

転送拡張機能をインストールして、拡張可能スイッチ ドライバー スタックで有効にすると場合、は、拡張可能スイッチのイングレス データ パスを取得する各パケットの転送に関する決定を行う責任を負います。 この情報に基づいて意思決定を転送、拡張機能を追加宛先ポートのパケットのアウト オブ バンド (OOB) データのコピー先のポートの配列に[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。 パケットが完了したらそのトラバーサル拡張可能スイッチのインターフェイスは、拡張可能スイッチ データ パスの指定の宛先ポートへのパケットします。

**注**  場合、転送拡張機能がインストールされていないか、有効になっている、拡張可能スイッチ決定を行います、転送パケットの受信データのパスから取得します。 スイッチのパケットの OOB データに宛先ポートを追加する[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)拡張可能スイッチのエグレス データ パケットを転送する前に構造体パス。

 

**注**  パケットが、NVGRE パケットの場合は、転送拡張機能が先ポートの配列に宛先ポートを追加できます。 ただし、拡張可能スイッチの HYPER-V ネットワーク仮想化 (HNV) のコンポーネントは、宛先ポートを確認して、パケットを転送する責任を負います。 詳細については、[ハイブリッド転送](hybrid-forwarding.md)を参照してください。

 

転送拡張機能は、イングレス データのパスから取得したパケットにのみ、ポートの送信先を追加できます。 出口データ パスをパケットの転送後にフィルター処理および転送拡張機能は拡張可能スイッチ ポートにパケット配信を除外できます。 詳細については、[拡張可能スイッチの宛先ポートへのパケット配送の除外](excluding-packet-delivery-to-extensible-switch-destination-ports.md)を参照してください。

内のパケットの OOB データ[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造の場合は、宛先ポートに含まれるため、データ、 [ **NDIS\_スイッチ\_転送\_先\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh598210)構造体。 配列内の各要素は、宛先ポートを定義し、として書式設定、 [ **NDIS\_スイッチ\_ポート\_先**](https://msdn.microsoft.com/library/windows/hardware/hh598224)構造体。

転送拡張機能を管理する次の HYPER-V 拡張可能スイッチ ハンドラー関数を呼び出すことができます、 [ **NDIS\_スイッチ\_転送\_先\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh598210)構造とその[ **NDIS\_スイッチ\_ポート\_先**](https://msdn.microsoft.com/library/windows/hardware/hh598224)要素。

<a href="" id="addnetbufferlistdestination"></a>[*AddNetBufferListDestination*](https://msdn.microsoft.com/library/windows/hardware/hh598133)  
この関数は追加する 1 つの宛先ポート、 [ **NDIS\_スイッチ\_転送\_先\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh598210)パケットの OOB 内の構造データ。

<a href="" id="getnetbufferlistdestinations"></a>[*GetNetBufferListDestinations*](https://msdn.microsoft.com/library/windows/hardware/hh598157)  
この関数へのポインターを返します、 [ **NDIS\_スイッチ\_転送\_先\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh598210)パケットの OOB データに構造体。

<a href="" id="grownetbufferlistdestinations"></a>[*GrowNetBufferListDestinations*](https://msdn.microsoft.com/library/windows/hardware/hh598158)  
この関数をさらに先ポート要素は追加、 [ **NDIS\_スイッチ\_転送\_先\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh598210)のパケットの構造OOB データ。

<a href="" id="updatenetbufferlistdestinations"></a>[*UpdateNetBufferListDestinations*](https://msdn.microsoft.com/library/windows/hardware/hh598303)  
この関数は、拡張機能が追加または除外パケットの 1 つまたは複数の宛先ポートに加えられた変更をコミットします。 これらの変更がコミットするには、 [ **NDIS\_スイッチ\_転送\_先\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh598210)パケットの OOB データに構造体。

ときに、転送拡張機能の[ *FilterSendNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff549966)関数が呼び出されると、 *NetBufferList*パラメーターのリンクリストへのポインターを格納する[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。 各構造体には、受信データのパスから取得したパケットを指定します。

各[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)転送拡張機能は、この一覧内の構造は、次の手順に従って、パケットの宛先ポートを追加します。

1.  拡張機能は、さまざまな種類の条件に基づいて、パケットの転送の決定を行います。 これらの条件を以下に示します。

    -   パケットのソース ポートおよびネットワーク アダプターの接続に基づくポリシーの条件。 転送拡張機能を使用してこの情報を取得する、 [ **NET\_バッファー\_一覧\_スイッチ\_転送\_詳細**](https://msdn.microsoft.com/library/windows/hardware/hh598259)マクロ。

    -   拡張可能スイッチ ポートのパケットのペイロード データに基づくポリシーの条件。 たとえば、拡張可能スイッチ ポートのポリシーは 4 (IPv4) パケットの IP バージョンのみの配信を許可するフィルターを含めることができます。

    **注**  パケットを転送するため、拡張可能スイッチの HNV のコンポーネントは、パケットが、NVGRE パケットの場合は、します。 ただし、転送拡張機能では、独自のイングレスとエグレスのパスでポリシーの条件を適用できます。 詳細については、[ハイブリッド転送](hybrid-forwarding.md)を参照してください。

     

2.  判断した場合、拡張機能を 1 つまたは複数の拡張可能スイッチ ポートにパケットを転送することができます、パケットの OOB データに宛先ポートを追加する必要があります。 この手順の詳細については、[を追加する拡張可能なスイッチ宛先ポート データ パケットに](adding-extensible-switch-destination-port-data-to-a-packet.md)を参照してください。

    **注**  パケットが、NVGRE パケットの場合は、転送拡張機能が、宛先ポートを追加する必要はありません。 詳細については、[ハイブリッド転送](hybrid-forwarding.md)を参照してください。

     

3.  拡張機能が拡張可能スイッチ ポートにパケットを転送することはできませんと判断した場合、パケットが破棄する必要があります。

    **注**  これは、パケットが、NVGRE パケットの場合は true ではありません。 詳細については、[ハイブリッド転送](hybrid-forwarding.md)を参照してください。

     

4.  呼び出す必要がありますが、拡張機能の追加、パケットの 1 つまたは複数の宛先ポートが場合、 [ **NdisFSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff562616)エグレス データ パス上のパケットを転送するようにします。

    **注**  パケットを転送するため、拡張可能スイッチの HNV のコンポーネントは、パケットが、NVGRE パケットの場合は、します。 詳細については、[ハイブリッド転送](hybrid-forwarding.md)を参照してください。

     

拡張可能スイッチのイングレスおよびエグレス データ パスの詳細については、[Hyper-v 拡張可能スイッチ データ パス](hyper-v-extensible-switch-data-path.md)を参照してください。

 

 





