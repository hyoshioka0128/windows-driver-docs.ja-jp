---
title: フィルタリング レイヤー
description: フィルタリング レイヤー
ms.assetid: db2fd1dc-c080-4f12-8138-7e66c74adacd
keywords:
- WDK Windows フィルタ リング プラットフォームのレイヤーをフィルター処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c95414c2dc2483d7d7f62ed89f9a21d87d0754d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353336"
---
# <a name="filtering-layer"></a>フィルタリング レイヤー


A*レイヤーをフィルター処理*ネットワーク データに渡される、TCP/IP ネットワーク スタック内のポイントは、[フィルター エンジン](filter-engine.md)の現在のフィルターのセットに対して照合します。 ネットワーク スタックの各フィルターのレイヤーが一意で識別される[レイヤー識別子のフィルタ リング](https://docs.microsoft.com/windows-hardware/drivers/network/filtering-layer-identifiers)します。

ときに、[フィルター](filter.md)ネットワーク データをフィルターで指定されたフィルタ リング層で追加されて、フィルター エンジンに追加されます。 特定[データ フィールド](https://docs.microsoft.com/windows-hardware/drivers/network/data-field-identifiers)で利用可能なフィルター処理の各層でそのレイヤーで、フィルター エンジンに追加されているフィルター。 フィルター エンジンは、ネットワーク データを渡す場合、[コールアウト](callout.md)、追加の処理、およびこれらのデータ フィールドを含む[メタデータ](https://docs.microsoft.com/windows-hardware/drivers/network/metadata-fields)そのフィルタ リング層で提供されます。

[実行時のフィルター処理レイヤー識別子](https://docs.microsoft.com/windows-hardware/drivers/network/run-time-filtering-layer-identifiers)(FWPS\_*XXX*) コールアウト ドライバーのカーネル モードで使用します。 [管理フィルタ リング層識別子](https://docs.microsoft.com/windows-hardware/drivers/network/management-filtering-layer-identifiers)(FWPM\_*XXX*) を使って**Fwpm * Xxx*** で、ベース フィルター エンジン (BFE)、いずれかのユーザー モードからと対話する関数またはカーネル モード (たとえば、 [ **FwpmFilterAdd0**](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmfilteradd0))。

FWPS データ型は、対応する FWPM よりも小さい: FWPM フィルタ リング層識別子は Guid (128 ビット)、レイヤーの識別子をフィルタ リング FWPS は[ **Luid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/igpupvdev/ns-igpupvdev-_luid)(64 ビット)。 FWPS データ型のサイズを小さくは、整数の比較では、リアルタイムのトラフィックの GUID の比較よりも高速化し、カーネル メモリ FWPS 型をより効率的に処理するために、システムのパフォーマンスを向上します。

 

 





