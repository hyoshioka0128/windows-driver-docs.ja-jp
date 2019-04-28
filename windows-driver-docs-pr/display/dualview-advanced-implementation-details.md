---
title: DualView の高度な実装の詳細
description: DualView の高度な実装の詳細
ms.assetid: 07fb7640-d723-4dc0-9403-9f70a75518f1
keywords:
- デュアル WDK ビデオのミニポート
- SingleView WDK ビデオのミニポート
- 論理上の子リレーション WDK のビデオのミニポート
- 物理子リレーション WDK のビデオのミニポート
- 子デバイス WDK のビデオのミニポート
- メモリ WDK デュアル ビュー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e685b11746d2a58440d7634b1303727b1cd3f59
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361279"
---
# <a name="dualview-advanced-implementation-details"></a>DualView の高度な実装の詳細


## <span id="ddk_dualview_advanced_implementation_details_gg"></span><span id="DDK_DUALVIEW_ADVANCED_IMPLEMENTATION_DETAILS_GG"></span>


理想的なデュアル実装がそのセカンダリ ビューを有効または無効に認識する必要があります。 セカンダリのビューを無効にする、デュアル ビューを有効になってない場合と同様にプライマリ ビューは動作します。 これは次のことを意味します。

-   プライマリ ディスプレイのビデオ メモリのすべての部分にアクセスできます。

-   ラップトップ コンピューターでは、子のディスプレイ デバイスのいずれかにプライマリ ディスプレイを切り替えることができます。

### <a name="span-idvideomemoryarrangementspanspan-idvideomemoryarrangementspanspan-idvideomemoryarrangementspanvideo-memory-arrangement"></a><span id="Video_Memory_Arrangement"></span><span id="video_memory_arrangement"></span><span id="VIDEO_MEMORY_ARRANGEMENT"></span>ビデオ メモリの配置

実装では、理想的なデュアル、セカンダリの表示が無効になっているプライマリ ディスプレイで全体のビデオ メモリが使用されるメモリ バッファー使用率が最適化されています。 この最適化が省略可能、ただし;ドライバー ライターの責任で使用するビデオ メモリ割り当ての戦略が完全にです。

セカンダリのビューを無効にすると、プライマリ ビューは、システムのパフォーマンスを最大化するビデオ メモリのすべての部分にアクセスできる必要があります。 セカンダリのビューを有効にすると、ただし、ミニポート ドライバーする必要がありますいないだけ適切なプライマリ ビューのメモリ。 代わりに、ミニポート ドライバーでは、デュアル モードに変更する前に、セカンダリのビューのビデオ メモリを予約する必要があります。 Windows XP 以降 (およびそれ以降のオペレーティング システム バージョンの続行)、新しいのビデオ要求がある[ **IOCTL\_ビデオ\_スイッチ\_デュアル**](https://msdn.microsoft.com/library/windows/hardware/ff568151)にビデオ メモリ配置を処理するドライバー開発者を支援します。 ときに Windows XP (とそれ以降) への呼び出しを処理、 **ChangeDisplaySettings**関数 (Windows SDK のドキュメントで説明)、IOCTL 送信\_ビデオ\_スイッチ\_デュアル要求前にそれぞれデュアル ビュー関連のビューは、モードを変更しようとします。 ドライバーは、その情報を使用して、必要性の前のビデオ メモリを手配します。

次の図は、デュアル ビューを無効になっていると、ビデオ メモリの並べ替え方法を示しています。

![デュアル ビューを無効になっているとメモリの並べ替え方法を示す図](images/memfig1.png)

次の図は、デュアル ビューを有効になっているとビデオ メモリの推奨される方法を示します。 各ビューには、独自の画面バッファーとオフスクリーン ヒープがあります。

![デュアル ビューを有効になっているとメモリの並べ替え方法を示す図](images/memfig2.png)

### <a name="span-idchildrelationshipsspanspan-idchildrelationshipsspanspan-idchildrelationshipsspanchild-relationships"></a><span id="Child_Relationships"></span><span id="child_relationships"></span><span id="CHILD_RELATIONSHIPS"></span>子リレーションシップ

一般的なモバイル ビデオ チップでは、LCD、CRT、テレビなどの複数の子デバイスがあります。 SingleView モードで次の図に示すようにプライマリ ビューを所有するすべての子デバイス、セカンダリのビューは、いずれを所有しているときにします。 ユーザーは、1 つの子デバイスから別のプライマリ ビューを切り替えることができます。 一度にアクティブにできるデバイスの 1 つだけです。

![図に示す singleview モード](images/childfig1.png)

デュアル モードでただし、それぞれの子割り当てることができます。 別のビューどのビューに関連付けられている子の疑問が浮かびます。 ビューとデバイス間の関係は、2 つの方法で記述できます: の観点で*物理子リレーション*の観点と*論理上の子リレーション*します。

*物理子リレーション*アダプターのビデオ チップとディスプレイ、デバイス間のリレーションシップが反映されます。 でシステムが起動した後、ビデオ チップとディスプレイ デバイスの物理関係しない変更します。 上記の図および次の図では、ビデオのチップを所有する LCD、CRT およびテレビは、デバイスを表示そのため、すべての 3 つのディスプレイ デバイスは、ビデオのチップの物理の子です。

*論理上の子リレーション*ビュー、および表示デバイス間の動的なリレーションシップが反映されます。 次の図にデュアル ビューが有効になってと状況がセカンダリのビュー (ビュー 2) は、CRT とテレビの両方のデバイスを所有しているときに、プライマリ ビュー (ビューの 1) が、LCD デバイスを所有しています。 これを別の方法は、LCD デバイスは、CRT と TV のデバイスはセカンダリのビューの論理的な子プライマリ ビューの論理子をします。 ミニポート ドライバーにより、論理上の子関係を報告する、 [ **IOCTL\_ビデオ\_取得\_子\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567801)要求。

![デュアル モードを示す図します。](images/childfig2.png)

追加のポイントのままになります。 デュアル ビューが有効になっているときにプライマリ ビューは子を自動的に切り替えることがあります。 SingleView モードでのみ CRT、プライマリ (で唯一) のビューに関連付けられたはアクティブです。 その他のすべてのディスプレイ デバイスは、アクティブなは。 デュアル ビューが有効にすると、上記の図は、プライマリ ビューは、CRT はセカンダリのビューの子、LCD デバイスを表示する切り替えを示します。 このスイッチのラップトップ コンピューターのために必要な場合があります、LCD デバイスがそのビューに関連付けすることはできませんので、セカンダリの表示が取り外し可能、という事実が原因です。 このスイッチを作成するのには、完全にミニポート ドライバーの管理下にある方法とかどうか。

 

 





