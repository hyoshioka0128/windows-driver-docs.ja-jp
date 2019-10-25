---
title: フィルタリング レイヤー
description: フィルタリング レイヤー
ms.assetid: db2fd1dc-c080-4f12-8138-7e66c74adacd
keywords:
- フィルターレイヤー WDK Windows フィルタリングプラットフォーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f31bf376e8c4f0a4137ae21fed2fc9d22724ffd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840487"
---
# <a name="filtering-layer"></a>フィルタリング レイヤー


フィルター*レイヤー*は、現在のフィルターセットと照合するためにネットワークデータが[フィルターエンジン](filter-engine.md)に渡される、tcp/ip ネットワークスタック内のポイントです。 ネットワークスタック内の各フィルターレイヤーは、一意の[フィルターレイヤー識別子](https://docs.microsoft.com/windows-hardware/drivers/network/filtering-layer-identifiers)によって識別されます。

[フィルターがフィルター](filter.md)エンジンに追加されると、指定したフィルター処理レイヤーに追加され、ネットワークデータがフィルター処理されます。 特定の[データフィールド](https://docs.microsoft.com/windows-hardware/drivers/network/data-field-identifiers)は、そのレイヤーのフィルターエンジンに追加されたフィルターによって処理されるように、各フィルターレイヤーで使用できるようになります。 フィルターエンジンは、追加処理のためにネットワークデータを[コールアウト](callout.md)に渡す場合、これらのデータフィールドと、そのフィルターレイヤーで使用できる[メタ](https://docs.microsoft.com/windows-hardware/drivers/network/metadata-fields)データを含みます。

[実行時のフィルターレイヤー識別子](https://docs.microsoft.com/windows-hardware/drivers/network/run-time-filtering-layer-identifiers)(fwps\_*XXX*) は、カーネルモードのコールアウトドライバーによって使用されます。 [管理フィルターレイヤー識別子](https://docs.microsoft.com/windows-hardware/drivers/network/management-filtering-layer-identifiers)(FWPM\_*XXX*) は、ユーザーモードまたはカーネルモード (たとえば[**FwpmFilterAdd0**](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmfilteradd0)) からベースフィルターエンジン (BFE) と対話する**FWPM<em>XXX</em>** 関数によって使用されます。

FWPS データ型は、対応する FWPM よりも小さくなります。 FWPM フィルターレイヤー識別子は Guid (128 ビット) であるのに対し、FWPS フィルターレイヤー識別子は[**luid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/igpupvdev/ns-igpupvdev-_luid)(64 ビット) です。 FWPS データ型のサイズを小さくすると、リアルタイムトラフィックの GUID 比較よりも整数比較が高速になるため、システムパフォーマンスが向上します。また、カーネルメモリは FWPS タイプをより効率的に処理します。

 

 





