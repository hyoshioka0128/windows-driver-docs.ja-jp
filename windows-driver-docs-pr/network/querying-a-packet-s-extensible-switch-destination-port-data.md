---
title: パケットの拡張可能スイッチの宛先ポートのデータを照会します。
description: パケットの拡張可能スイッチの宛先ポートのデータを照会します。
ms.assetid: 57D82C5E-3758-492C-A1DA-B7BC3DBE2E7A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29801591a0c6991162e44a04c5e48d9c2d679196
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530231"
---
# <a name="querying-a-packets-extensible-switch-destination-port-data"></a>パケットの拡張可能スイッチの宛先ポートのデータを照会します。


各 HYPER-V 拡張可能スイッチの宛先ポートがで指定された、 [ **NDIS\_切り替える\_ポート\_先**](https://msdn.microsoft.com/library/windows/hardware/hh598224)内の要素、 [ **NDIS\_スイッチ\_転送\_先\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh598210)構造体。 この配列は、の帯域外 (OOB) コンテキストのパケットの転送に含まれている[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。 このコンテキストの詳細については、[Hyper-v 拡張可能スイッチの転送コンテキスト](hyper-v-extensible-switch-forwarding-context.md)を参照してください。

拡張可能スイッチ拡張機能の呼び出し、 [ *GetNetBufferListDestinations* ](https://msdn.microsoft.com/library/windows/hardware/hh598157)へのポインターを取得する関数、 [ **NDIS\_切り替える\_転送\_先\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh598210)でパケットの構造体[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。 個別[ **NDIS\_スイッチ\_ポート\_先**](https://msdn.microsoft.com/library/windows/hardware/hh598224)この構造内の要素を使用してアクセスできる、 [ **NDIS\_スイッチ\_ポート\_先\_で\_配列\_インデックス**](https://msdn.microsoft.com/library/windows/hardware/hh598225)マクロ。

パフォーマンスを向上させるには、転送拡張機能を呼び出すことができます、 [ *GrowNetBufferListDestinations* ](https://msdn.microsoft.com/library/windows/hardware/hh598158)関数の代わりに[ *GetNetBufferListDestinations*](https://msdn.microsoft.com/library/windows/hardware/hh598157)へのポインターを取得する、 [ **NDIS\_スイッチ\_転送\_先\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh598210)構造体. 拡張機能は宛先ポートのパケットの OOB データに追加の配列の要素が必要であると判断した場合、します。 詳細については、[を追加する拡張可能なスイッチ宛先ポート データ パケットに](adding-extensible-switch-destination-port-data-to-a-packet.md)を参照してください。

**注**  だけで、拡張可能スイッチのエグレス データのパスから取得したパケットには宛先ポートの情報にが含まれます。 詳細については、[Hyper-v 拡張可能スイッチのデータ パス](hyper-v-extensible-switch-data-path.md)を参照してください。

 

 

 





