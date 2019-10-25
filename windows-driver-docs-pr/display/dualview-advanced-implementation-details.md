---
title: DualView の高度な実装の詳細
description: DualView の高度な実装の詳細
ms.assetid: 07fb7640-d723-4dc0-9403-9f70a75518f1
keywords:
- デュアルビュー WDK ビデオミニポート
- SingleView WDK ビデオミニポート
- 論理子リレーションシップ WDK ビデオミニポート
- 物理的な子関係 WDK ビデオミニポート
- 子デバイス WDK ビデオミニポート
- メモリ WDK デュアルビュー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5cd436932451a292f402cb3e4c89c0e28899252b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839745"
---
# <a name="dualview-advanced-implementation-details"></a>DualView の高度な実装の詳細


## <span id="ddk_dualview_advanced_implementation_details_gg"></span><span id="DDK_DUALVIEW_ADVANCED_IMPLEMENTATION_DETAILS_GG"></span>


最適なデュアルビュー実装では、セカンダリビューが有効または無効になっていることを認識する必要があります。 セカンダリビューが無効になっている場合、プライマリビューは、デュアルビューが有効になっていない場合と同様に動作します。 これは次のことを意味します。

-   プライマリディスプレイは、ビデオメモリのすべての部分にアクセスできます。

-   ラップトップコンピューターでは、プライマリディスプレイを任意の子ディスプレイデバイスに切り替えることができます。

### <a name="span-idvideo_memory_arrangementspanspan-idvideo_memory_arrangementspanspan-idvideo_memory_arrangementspanvideo-memory-arrangement"></a><span id="Video_Memory_Arrangement"></span><span id="video_memory_arrangement"></span><span id="VIDEO_MEMORY_ARRANGEMENT"></span>ビデオメモリの配置

最適なデュアルビュー実装では、メモリバッファー使用量が最適化され、セカンダリディスプレイが無効になっているときに、ビデオメモリ全体がプライマリディスプレイで使用されるようになります。 ただし、この最適化は省略可能です。使用するビデオメモリの割り当て方法は、ドライバーの作成者が完全に利用できます。

セカンダリビューが無効になっている場合、プライマリビューはビデオメモリのすべての部分にアクセスして、システムのパフォーマンスを最大化することができます。 ただし、セカンダリビューが有効になっている場合、ミニポートドライバーは、プライマリビューのメモリに対してのみ適切である必要があります。 代わりに、デュアルビューモードに変更する前に、ミニポートドライバーでセカンダリビューのビデオメモリを予約する必要があります。 Windows XP (およびそれ以降のバージョンのオペレーティングシステム) では、新しいビデオ要求、 [**IOCTL\_ビデオ\_スイッチ\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_switch_dualview)を使用して、ドライバー作成者がビデオメモリの配置を処理できるようになります。 Windows XP (およびそれ以降) が**Changedisplaysettings**関数の呼び出しを処理するとき (Windows SDK のドキュメントで説明されています)、その前に、デュアルビューに関連する各ビューに対して、\_VIDEO\_\_スイッチによる IOCTL 要求を送信します。モードの変更を試みます。 ドライバーは、その情報を使用して、ニーズに合わせてビデオメモリの配置を行うことができます。

次の図は、デュアルビューが無効になっているビデオメモリの配置を示しています。

![デュアルビューが無効になっているメモリの配置を示す図](images/memfig1.png)

次の図は、デュアルビューが有効になっているビデオメモリの推奨される配置を示しています。 各ビューには、独自の画面バッファーとオフスクリーンヒープがあります。

![デュアルビューが有効になっているメモリの配置を示す図](images/memfig2.png)

### <a name="span-idchild_relationshipsspanspan-idchild_relationshipsspanspan-idchild_relationshipsspanchild-relationships"></a><span id="Child_Relationships"></span><span id="child_relationships"></span><span id="CHILD_RELATIONSHIPS"></span>子リレーションシップ

一般的なモバイルビデオチップには、LCD、CRT、TV などの複数の子デバイスがあります。 次の図に示すように、SingleView モードでは、プライマリビューはこれらすべての子デバイスを所有しますが、セカンダリビューはそれらのすべてを所有していません。 ユーザーは、プライマリビューを子デバイス間で切り替えることができます。 一度にアクティブにできるデバイスは1つだけです。

![singleview モードを示す図](images/childfig1.png)

ただし、デュアルビューモードでは、各子を別のビューに割り当てることができます。この質問は、どのビューがどの子に関連付けられているかによって発生します。 ビューとデバイス間のリレーションシップについては、*物理的な子の関係*と、論理的な*子*の関係の観点から、2つの方法で説明できます。

*物理的な子の関係*は、アダプターのビデオチップとそのディスプレイデバイスの関係を反映しています。 システムが起動した後、ビデオチップとディスプレイデバイスの物理的な関係が変化することはありません。 上の図と次の図では、ビデオチップが、LCD、CRT、および TV ディスプレイデバイスを所有しています。このため、3つのディスプレイデバイスはすべて、ビデオチップの物理的な子です。

*論理子の関係*には、ビューとディスプレイデバイスの間の動的な関係が反映されます。 次の図では、デュアルビューが有効になっており、プライマリビュー (ビュー 1) が LCD デバイスを所有しています。一方、セカンダリビュー (ビュー 2) は、CRT デバイスと TV デバイスの両方を所有しています。 もう1つの方法は、LCD デバイスがプライマリビューの論理的な子であり、CRT デバイスと TV デバイスがセカンダリビューの論理的な子であることです。 ミニポートドライバーは、 [ **\_子\_状態要求を取得\_、IOCTL\_ビデオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_get_child_state)を通じて、論理的な子関係を報告します。

![ビューモードを示す図](images/childfig2.png)

1つの追加ポイントが残ります。 [デュアル] が有効になっている場合、プライマリビューで子を自動的に切り替えることができます。 SingleView モードでは、プライマリ (およびのみ) ビューに関連付けられている CRT のみがアクティブになります。 他のすべてのディスプレイデバイスは非アクティブです。 デュアルビューが有効になった後、前の図は、プライマリビューが LCD デバイスに表示されるようになったことを示しています。一方、CRT はセカンダリビューの子です。 このスイッチは、セカンダリビューがリムーバブルであることが原因で、ラップトップコンピューターで必要になる場合があります。これは、LCD デバイスをそのビューに関連付けることができないことを意味します。 このスイッチを使用するかどうか、およびミニポートドライバーをどのように管理するか。

 

 





