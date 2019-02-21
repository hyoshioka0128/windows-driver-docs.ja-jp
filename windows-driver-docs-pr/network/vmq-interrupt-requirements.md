---
title: VMQ 割り込みの要件
description: VMQ 割り込みの要件
ms.assetid: 7ECC9031-D41B-4664-963D-F1C20B297B7C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7230021daa6b10cbc4599c22fe86d9d165ff449
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551216"
---
# <a name="vmq-interrupt-requirements"></a>VMQ 割り込みの要件


仮想マシン キュー (VMQ) 機能をサポートしているミニポート ドライバーでは、次の割り込み配賦の要件もサポートする必要があります。

-   ミニポート ドライバーには、MSI をサポートする必要があります。 ドライバーを設定する必要があります、 **NDIS\_受信\_フィルター\_MSI\_X\_サポートされている**フラグ、 **SupportedQueueProperties**メンバー、 [ **NDIS\_受信\_フィルター\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)構造体。

    ドライバーはこの構造を返します、 [ **NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)構造体ドライバーがその呼び出しで使用する、 [ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)関数。

-   ミニポート ドライバーを呼び出す必要があります、 [ **NdisGetRssProcessorInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff562669)ベクトルの割り込みを割り当てるためのプロセッサ情報を取得します。 レジストリ キーまたは割り込み割り当ての他のソースから取得した情報に依存する必要があります。

    [**NdisGetRssProcessorInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff562669) RSS および VMQ のミニポート ドライバーが使用できるプロセッサのセットに関する情報を返します。 この情報は、 [ **NDIS\_RSS\_プロセッサ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff567274)構造体。

-   ミニポート ドライバーで指定されている各プロセッサの割り込みの 1 つだけのベクターを割り当てる必要があります、 [ **NDIS\_RSS\_プロセッサ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff567274)構造体。

    ミニポート ドライバーでは、他のイベントを送信または受信パケットの操作に関連していない以下の 2 つのベクトルの割り込みを割り当てる必要があります。 など、ドライバーでは、リンクのステータス イベント、IDT を割り当てる可能性があります。

-   ミニポート ドライバーでは、次の表で定義されている MSI X 割り込みのベクトルの最小数をサポートする必要があります。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">キューの数</th>
    <th align="left">必要な MSI X 割り込みベクトルの最小数</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>1–16</p></td>
    <td align="left"><p>1–16</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>17–64</p></td>
    <td align="left"><p>16–32</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>65 以上</p></td>
    <td align="left"><p>32 個以上</p></td>
    </tr>
    </tbody>
    </table>

     

 

 





