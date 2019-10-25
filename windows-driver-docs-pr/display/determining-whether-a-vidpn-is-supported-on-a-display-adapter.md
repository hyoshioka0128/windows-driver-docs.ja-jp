---
title: ディスプレイアダプターでの VidPN サポートの決定
description: このトピックでは、ディスプレイミニポートドライバーが、ディスプレイアダプターで特定のビデオの存在するネットワーク (VidPN) がサポートされているかどうかを確認する方法について説明します。
ms.assetid: ebf001fb-e445-4534-8e89-60e1b06b2d6e
keywords:
- ビデオの現在のネットワークの WDK ディスプレイ、サポートされているかどうかの確認
- VidPN WDK 表示、サポートされているかどうかの確認
- 機能的な VidPN WDK ディスプレイ
- VidPN がサポートされている WDK ディスプレイの決定
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: d35fdb8cd02c485131a69f5e18d173fdc66156ca
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839749"
---
# <a name="determining-vidpn-support-on-a-display-adapter"></a>ディスプレイアダプターでの VidPN サポートの決定


このトピックでは、ディスプレイミニポートドライバーが、ディスプレイアダプターで特定のビデオの存在するネットワーク (VidPN) がサポートされているかどうかを確認する方法について説明します。 この資料を読む前に、次のトピックで説明されている内容について理解しておく必要があります。

-   [ビデオの現在のネットワークの概要](introduction-to-video-present-networks.md)

-   [VidPN オブジェクトとインターフェイス](vidpn-objects-and-interfaces.md)

次の条件を満たす場合、VidPN は*機能*します。

-   これには、少なくとも1つのパスを持つトポロジがあります。 (パスは、ソースとターゲットの間の関連付けです)。

-   トポロジ内の各ソースとターゲットにはピン留めされたモードがあります。

次のいずれかの条件に該当する場合、*表示アダプターで VidPN がサポートさ*れます。

-   これは機能し、ディスプレイアダプターに実装できます。 つまり、表示アダプターのビデオ出力コーデックは、トポロジと、VidPN によって指定された固定モードをサポートするように構成できます。

-   これには、少なくとも1つのパスを持つトポロジがあり、これを表示アダプターに実装できる機能的な VidPN に拡張することができます。 つまり、既にピン留めされているモードを変更しなくても、まだモードがピン留めされていないすべてのビデオのソースとターゲットのモードをピン留めすることができます。 さらに、結果として得られる機能の VidPN をディスプレイアダプターに実装することもできます。

-   空のトポロジがあります。 表示アダプターでは、何も表示しないことが常にサポートされています。

VidPN がサポートされているかどうかを判断する際には、VidPN のトポロジが有効かどうかを判断することがあります。 つまり、ビデオが存在するソースは、トポロジで指定されているビデオの現在のターゲットに接続できますか。 トポロジ内のすべてのビデオに存在するターゲットがモニターに接続されている必要はありません。 トポロジは有効であり、接続されているモニターがない場合でも、VidPN をサポートできます。

特定の VidPN がディスプレイアダプターでサポートされているかどうかを確認するために、VidPN マネージャーは[**DxgkDdiIsSupportedVidPn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_issupportedvidpn)を呼び出します。 **DxgkDdiIsSupportedVidPn**に渡される引数の1つは、目的の vidpn と呼ばれる vidpn オブジェクトへのハンドルです。 **DxgkDdiIsSupportedVidPn**は目的の vidpn のトポロジを検査する必要があります。また、目的の vidpn にピン留めされたモードが既に存在するビデオのソースとターゲットを確認する必要があります。 次に、目的の VidPN がサポートされているかどうかを示すブール値を返す必要があります (このトピックで前述した定義に従ってください)。 トポロジ、ソースモードセット、および VidPN のターゲットモードセットの検査の詳細については、「 [Vidpn オブジェクトとインターフェイス](vidpn-objects-and-interfaces.md)」を参照してください。

 

 





