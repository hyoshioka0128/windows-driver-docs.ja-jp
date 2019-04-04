---
title: Hyper-V 拡張可能スイッチ送信および受信フラグ
description: Hyper-V 拡張可能スイッチ送信および受信フラグ
ms.assetid: FBA506EC-4E9F-4964-9C9C-FF4910DDA908
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ca974256b6d9ea1e83a3e9f52896a88848fb8e4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578914"
---
# <a name="hyper-v-extensible-switch-send-and-receive-flags"></a>Hyper-V 拡張可能スイッチ送信および受信フラグ


**注**  このページは、情報とでのダイアグラムに精通していることを前提としています。 [Hyper-v 拡張可能スイッチの概要](overview-of-the-hyper-v-extensible-switch.md)と[ハイブリッド転送](hybrid-forwarding.md)します。

 

HYPER-V 拡張可能スイッチのデータ パスの上に移動するパケット トラフィックが、次のように拡張機能によって得られます。

-   イングレス データのパスからパケットを取得する拡張機能とその[ *FilterSendNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff549966)関数が呼び出されます。 拡張機能は、呼び出すことによって拡張機能を基になる、イングレス データ パスにパケットを転送[ **NdisFSendNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff562616)します。 フィルター処理および転送拡張機能も削除できますパケット イングレス データのパスから呼び出すことによって[ **NdisFSendNetBufferListsComplete**](https://msdn.microsoft.com/library/windows/hardware/ff562618)します。

-   出口データ パスからパケットを取得する拡張機能とその[ *FilterReceiveNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff549960)関数が呼び出されます。 拡張機能が出口のデータ パスでの拡張機能を呼び出すことによって関連するパケットを転送[ **NdisFIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff561820)します。 フィルター処理および転送拡張機能も削除できますパケット エグレス データのパスから呼び出すことによって[ **NdisFReturnNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff562613)します。

次のフラグを設定することがあります、 *SendFlags*パラメーターの[ *FilterSendNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff549966)または[ **NdisFSendNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff562616):

<a href="" id="ndis-send-flags-switch-single-source"></a>**NDIS\_送信\_フラグ\_スイッチ\_単一\_ソース**  
このフラグが設定のリンク リストにすべてのパケット場合[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体が同じ HYPER-V 拡張可能スイッチの発信元ポートから発生しました。

NDIS を呼び出すと[ *FilterSendNetBufferLists*](https://msdn.microsoft.com/library/windows/hardware/ff549966)、拡張可能スイッチの拡張可能なインターフェイスが同じ発信元ポートから複数のパケットをグループ化する場合にこのフラグが設定されます。 最高のパフォーマンスを拡張機能にこのグループ化を維持し、を呼び出すときに、このフラグを設定[ **NdisFSendNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff562616)します。 発生元またはリンクの一覧にパケットを複製、拡張機能を追加することも[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体の場合は、拡張機能を使用して、同じソースとして、その他のポートリスト内のパケットです。

**注**  場合のリンク リストには、各パケット[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体が同じソース ポートを使用して、拡張機能を設定する必要があります、**NDIS\_送信\_完了\_フラグ\_スイッチ\_単一\_ソース**フラグ、 *SendCompleteFlags*パラメーターの[ **NdisFSendNetBufferListsComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff562618)送信要求の完了時にします。

 

<a href="" id="ndis-send-flags-switch-destination-group"></a>**NDIS\_送信\_フラグ\_スイッチ\_先\_グループ**  
このフラグが設定のリンク リストにすべてのパケットの場合[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造は、同じ拡張可能スイッチの宛先ポートに転送します。

転送拡張機能は、このフラグを使用して、リンクの一覧については[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)各パケットの判別した後、イングレス データ パスに転送する構造体宛先ポートです。 このフラグは消費し、エグレス データのパスをパケットを転送する前に、拡張可能スイッチの基になるミニポート端で削除します。

キャプチャおよび拡張機能をフィルター処理は、このフラグを使用できません。

**注**  転送拡張機能では、非 NVGRE パケットのパケットの宛先ポートのみを決定します。 パケットが、NVGRE パケットの場合は、HYPER-V ネットワーク仮想化 (HNV) のコンポーネントは、パケットの宛先ポートを決定し、パケットを転送します。 詳細については、[ハイブリッド転送](hybrid-forwarding.md)を参照してください。

 

最適なパフォーマンスを転送拡張機能はこのフラグを設定を同じ宛先ポートに転送する場合は、リンク リストのすべてのパケット。 このフラグを設定して、コンテキストを転送する拡張可能スイッチに、宛先ポートと同じ要素をリンク リスト内のすべてのパケットがあること、拡張機能が受信します。

**注**  転送拡張機能は、複数のターゲットを持つパケットのリンクの一覧については、このフラグのポートを設定しない必要があります。

 

次のフラグを設定することがあります、 *ReceiveFlags*パラメーターの[ *FilterReceiveNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff549960)または[ **NdisFIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff561820):

<a href="" id="ndis-receive-flags-switch-single-source"></a>**NDIS\_受信\_フラグ\_スイッチ\_単一\_ソース**  
このフラグが設定のリンク リストにすべてのパケット場合[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体が同じ HYPER-V 拡張可能スイッチの発信元ポートから発生しました。

NDIS を呼び出すと[ *FilterReceiveNetBufferLists*](https://msdn.microsoft.com/library/windows/hardware/ff549960)、拡張可能スイッチが、同じソース ポートから複数のパケットをグループ化する場合にこのフラグが設定されます。 最高のパフォーマンスを拡張機能にこのグループ化を維持し、を呼び出すときに、このフラグを設定[ **NdisMIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff563598)します。 発生元またはリンクの一覧にパケットを複製、拡張機能の追加もする必要があります[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)パケットがある同じ場合、構造体のソースとして、他のポートリスト内のパケットです。

**注**  場合のリンク リストには、各パケット[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体を使用して、同じ発信元ポート、拡張機能を設定する必要があります、**NDIS\_返す\_フラグ\_スイッチ\_単一\_ソース**フラグ、 *ReturnFlags* のパラメーター[*FilterReturnNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff549964)受信要求が完了したとき。 拡張機能このフラグを設定する必要があります、 *ReturnFlags*を呼び出す場合は、パラメーター [ **NdisFReturnNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff562613)取得されなかった戻りのパケットを複製します。

 

<a href="" id="ndis-receive-flags-switch-destination-group"></a>**NDIS\_受信\_フラグ\_スイッチ\_先\_グループ**  
このフラグが設定のリンク リストにすべてのパケットの場合[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造は、同じ拡張可能スイッチの宛先ポートに転送します。

NDIS を呼び出すと[ *FilterReceiveNetBufferLists*](https://msdn.microsoft.com/library/windows/hardware/ff549960)にはこのフラグを設定、拡張可能スイッチが 1 つの宛先を持つ複数のパケットをグループ化する場合のポート。 最高のパフォーマンスを拡張機能にこのグループ化を維持し、を呼び出すときに、このフラグを設定[ **NdisMIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff563598)します。 発生元またはリンクの一覧にパケットを複製、拡張機能の追加もする必要があります[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体の場合は、パケットがある同じ送信先ポートとして、一覧で他のパケットをします。

**注**  拡張機能を呼び出すと[ **NdisFIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff561820)、これを設定する必要がありますしない、 **NDIS\_受信\_フラグ\_リソース**フラグ、 *ReceiveFlags*パラメーター。 拡張可能スイッチのインターフェイスはこのフラグを無視し、呼び出すことによって、受信を示す値を完了[ *FilterReturnNetBufferLists*](https://msdn.microsoft.com/library/windows/hardware/ff549964)します。

 

 

 





