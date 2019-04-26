---
title: フィルタリング レイヤー
description: フィルタリング レイヤー
ms.assetid: db2fd1dc-c080-4f12-8138-7e66c74adacd
keywords:
- WDK Windows フィルタ リング プラットフォームのレイヤーをフィルター処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3790778a96eed061c961f51df14e90c58f81b4b1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347368"
---
# <a name="filtering-layer"></a>フィルタリング レイヤー


A*レイヤーをフィルター処理*ネットワーク データに渡される、TCP/IP ネットワーク スタック内のポイントは、[フィルター エンジン](filter-engine.md)の現在のフィルターのセットに対して照合します。 ネットワーク スタックの各フィルターのレイヤーが一意で識別される[レイヤー識別子のフィルタ リング](https://msdn.microsoft.com/library/windows/hardware/ff549947)します。

ときに、[フィルター](filter.md)ネットワーク データをフィルターで指定されたフィルタ リング層で追加されて、フィルター エンジンに追加されます。 特定[データ フィールド](https://msdn.microsoft.com/library/windows/hardware/ff546312)で利用可能なフィルター処理の各層でそのレイヤーで、フィルター エンジンに追加されているフィルター。 フィルター エンジンは、ネットワーク データを渡す場合、[コールアウト](callout.md)、追加の処理、およびこれらのデータ フィールドを含む[メタデータ](https://msdn.microsoft.com/library/windows/hardware/ff559174)そのフィルタ リング層で提供されます。

[実行時のフィルター処理レイヤー識別子](https://msdn.microsoft.com/library/windows/hardware/ff570731)(FWPS\_*XXX*) コールアウト ドライバーのカーネル モードで使用します。 [管理フィルタ リング層識別子](https://msdn.microsoft.com/library/windows/hardware/ff557101)(FWPM\_*XXX*) を使って**Fwpm * Xxx*** で、ベース フィルター エンジン (BFE)、いずれかのユーザー モードからと対話する関数またはカーネル モード (たとえば、 [ **FwpmFilterAdd0**](https://msdn.microsoft.com/library/windows/desktop/aa364046))。

FWPS データ型は、対応する FWPM よりも小さい: FWPM フィルタ リング層識別子は Guid (128 ビット)、レイヤーの識別子をフィルタ リング FWPS は[ **Luid**](https://msdn.microsoft.com/library/windows/hardware/ff557080)(64 ビット)。 FWPS データ型のサイズを小さくは、整数の比較では、リアルタイムのトラフィックの GUID の比較よりも高速化し、カーネル メモリ FWPS 型をより効率的に処理するために、システムのパフォーマンスを向上します。

 

 





