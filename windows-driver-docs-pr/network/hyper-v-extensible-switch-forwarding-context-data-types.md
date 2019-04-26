---
title: Hyper-V 拡張可能スイッチ転送コンテキスト データの種類
description: Hyper-V 拡張可能スイッチ転送コンテキスト データの種類
ms.assetid: B5377411-C6F0-47BE-BD45-534AC784ED76
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7f1272b456789c535ca77582ef3cbc2e20e57db
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349575"
---
# <a name="hyper-v-extensible-switch-forwarding-context-data-types"></a>Hyper-V 拡張可能スイッチ転送コンテキスト データの種類


[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造に、HYPER-V 拡張可能スイッチのデータ パスを通過する各パケットには、アウト オブ バンド (OOB) データが含まれています。 このデータは、パケットが発信された場所、およびパケット配信のための 1 つまたは複数の宛先ポートからの発信元ポートを指定します。 この OOB データと呼ばれる、*転送コンテキスト拡張可能スイッチ*します。

パケットの内で拡張可能スイッチ転送コンテキストにアクセスする次のデータ型が宣言されている[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。

<a href="" id="ndis-switch-forwarding-detail-net-buffer-list-info"></a>[**NDIS\_SWITCH\_FORWARDING\_DETAIL\_NET\_BUFFER\_LIST\_INFO**](https://msdn.microsoft.com/library/windows/hardware/hh598211)  
これは、パケットの転送の特性を含む 64 ビットの和集合です。 このデータには、パケットが元のソース ポートおよびネットワーク アダプター接続の識別子が含まれています。 このデータには、コピー先のポートの配列で利用できる未使用の要素の数も含まれています。

拡張可能スイッチ拡張機能を使用してこのデータにアクセスできる、 [ **NET\_バッファー\_一覧\_切り替える\_転送\_詳細**](https://msdn.microsoft.com/library/windows/hardware/hh598259)マクロ。

<a href="" id="ndis-switch-forwarding-destination-array"></a>[**NDIS\_スイッチ\_転送\_先\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh598211)  
この構造体は、パケットの宛先ポート配列を定義します。 この配列内の各要素として書式設定、 [ **NDIS\_スイッチ\_ポート\_先**](https://msdn.microsoft.com/library/windows/hardware/hh598224)構造体。

[ **NDIS\_スイッチ\_転送\_先\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh598211)構造体には、現在の合計数を指定するメンバーが含まれています。配列で使用される要素の数と要素の数。

拡張可能スイッチ拡張機能は呼び出すことでこの配列を取得することができます、 [ *GetNetBufferListDestinations* ](https://msdn.microsoft.com/library/windows/hardware/hh598157)関数。 場合は、ドライバーを追加または変更には、複数の宛先ポートでのパケットの配列内の要素、呼び出す必要があります、 [ *UpdateNetBufferListDestinations* ](https://msdn.microsoft.com/library/windows/hardware/hh598303)関数。 この関数は、パケットの転送のコンテキストでのコピー先ポートの配列にそれらの変更をコミットします。

**注**  を 1 つだけの宛先ポートでのパケットに変更をコミットするには、ドライバーを呼び出す方が効率的、 [ *AddNetBufferListDestination* ](https://msdn.microsoft.com/library/windows/hardware/hh598133)関数。

 

<a href="" id="ndis-switch-port-destination"></a>[**NDIS\_スイッチ\_ポート\_変換先**](https://msdn.microsoft.com/library/windows/hardware/hh598224)  
この構造体は、パケットの宛先ポートを定義します。 1 つの宛先ポート、パケットの 1 つしかない[ **NDIS\_スイッチ\_ポート\_先**](https://msdn.microsoft.com/library/windows/hardware/hh598224)先ポートの配列内の要素。 複数の宛先ポートとパケットの場合は、配列内のこれらの要素の 1 つ以上です。

拡張機能が呼び出された後、拡張可能スイッチに[ *GetNetBufferListDestinations* ](https://msdn.microsoft.com/library/windows/hardware/hh598157)にパケットの宛先ポートの配列を取得するには、を使用して、配列内の個々の要素をアクセス[ **NDIS\_スイッチ\_ポート\_先\_で\_配列\_インデックス**](https://msdn.microsoft.com/library/windows/hardware/hh598225)マクロ。

 

 





