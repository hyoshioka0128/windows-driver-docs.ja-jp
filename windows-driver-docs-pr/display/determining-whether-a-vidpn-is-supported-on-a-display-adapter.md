---
title: ディスプレイ アダプターで VidPN サポートの判断
description: このトピックでは、ディスプレイのミニポート ドライバーが特定のビデオ存在するネットワーク (VidPN) は ディスプレイ アダプターでサポートされているかどうかを決定する方法について説明します。
ms.assetid: ebf001fb-e445-4534-8e89-60e1b06b2d6e
keywords:
- ビデオの存在するネットワーク WDK の表示、サポートされている場合を決定します。
- サポートされている場合を決定する、VidPN WDK の表示
- 機能 VidPN WDK を表示します。
- WDK の表示がサポートされている VidPN を決定します。
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: f132b5c7d3db0264e77ce5d615aef2dd2eff927f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384881"
---
# <a name="determining-vidpn-support-on-a-display-adapter"></a>ディスプレイ アダプターで VidPN サポートの判断


このトピックでは、ディスプレイのミニポート ドライバーが特定のビデオ存在するネットワーク (VidPN) は ディスプレイ アダプターでサポートされているかどうかを決定する方法について説明します。 このガイドを読む前に次のトピックの内容に精通する必要があります。

-   [ビデオの存在するネットワークの概要](introduction-to-video-present-networks.md)

-   [VidPN オブジェクトとインターフェイス](vidpn-objects-and-interfaces.md)

VidPN は*機能*次の条件を満たしている場合。

-   少なくとも 1 つのパスが含まれたトポロジがあります。 (パスは、ソースとターゲット間のアソシエーションです)。

-   ソースとターゲット、トポロジ内の各固定モードがあります。

VidPN は*ディスプレイ アダプターではサポートされて*次の条件のいずれかが true の場合。

-   これが機能していて、ディスプレイ アダプターで実装できます。 つまり、ディスプレイ アダプターの出力ビデオ コーデックは、トポロジであり、VidPN で指定された固定モードをサポートするために構成できます。

-   トポロジでは、少なくとも 1 つのパスがあるし、ディスプレイ アダプターで実装できる機能 VidPN するように拡張できます。 つまり、なります可能であれば、すべてのビデオの存在するソースとターゲットをピン留めされたモードをまだ持っていないの pin モードに、既に固定されているすべてのモードを変更することがなく。 さらに、結果として得られる機能 VidPN をディスプレイ アダプターで実装することがあります。

-   空のトポロジがあります。 考え方は、何も表示が常にでサポートされているディスプレイ アダプターです。

VidPN のトポロジが有効かどうかを VidPN がサポートされているかどうかを決定する部分の決定です。 ビデオに存在するソースは、トポロジによって指定されたビデオ存在するターゲットに言い換えると、接続できるでしょうか。 トポロジ内のすべてのビデオ存在するターゲットのモニターが接続されている要件ではないことに注意します。 トポロジを有効にして、モニターが接続されていない場合でも、VidPN をサポートできます。

VidPN manager の呼び出しに、 [ **DxgkDdiIsSupportedVidPn** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_issupportedvidpn)ディスプレイのミニポート ドライバー ディスプレイ アダプターの特定の VidPN をサポートするかどうかを確認します。 渡される引数の 1 つ**DxgkDdiIsSupportedVidPn**という目的 VidPN VidPN オブジェクトへのハンドルします。 **DxgkDdiIsSupportedVidPn**目的 VidPN のトポロジを検査する必要があり、メモが存在するビデオのソースと目的の VidPN 既に内のターゲットがピン留めするモードを実行する必要があります。 (このトピックで前述下手定義) に従って目的の VidPN がサポートされているかどうかを示すブール値を返すにする必要があります。 トポロジ、ソース モードのセット、およびターゲット モード、VidPN 一連の検査については、次を参照してください。 [VidPN オブジェクトとインターフェイス](vidpn-objects-and-interfaces.md)します。

 

 





