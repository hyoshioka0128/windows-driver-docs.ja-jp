---
title: 受信済みイーサネット フレームの表示
description: 受信済みイーサネット フレームの表示
ms.assetid: 39f35a54-1d80-4a14-b48c-2dbbfde9c86f
keywords:
- WDK のイーサネット ネットワーク
- フレームの WDK ネットワーク
- イーサネット フレーム WDK ネットワー キングの TCP/IP トランスポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15adc2eebb1980445ecdd39c90f6a6a880236749
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581926"
---
# <a name="indicating-received-ethernet-frames"></a>受信済みイーサネット フレームの表示





Windows の TCP/IP プロトコル ドライバーには、一連のイーサネット フレームを受信するための要件が課されます。 発信されるすべてのドライバーが受信イーサネット フレームの表示または変更の基になる兆候が表示されるドライバーは、TCP/IP を適用する一般的な要件をサポートする必要があります。 これらのドライバーでは、イーサネット ミニポート ドライバー、MUX の中間ドライバーを含めるし、フィルター ドライバー。

**注**  ドライバーがこれらの要件を遵守しない場合を予期しない動作可能性があります (TCP/IP トランスポート、MUX 中間ドライバー、フィルター ドライバーなど) のドライバーに関連します。

 

イーサネットが発信されたドライバーの受信の表示、次の要件をサポートする必要があります。

-   ドライバーを割り当てる必要があります、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)受信したイーサネット フレームの構造体。 各**NET\_バッファー\_一覧**構造体で定義されている、アウト オブ バンド (OOB) データを含める必要があります、 **NetBufferListInfo**のメンバー、 **NET\_バッファー\_一覧**特定の使用に必要な。

-   ドライバーを割り当てる必要があります、 [ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)フレームの構造体し、をリンク、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。 イーサネット ミニポートには、1 つずつ割り当てる必要があります**NET\_バッファー**構造体を**NET\_バッファー\_一覧**構造を示す場合にデータを受信しました。 この制限は、イーサネットのみに適用されます。 パスを受信します。 ネイティブの 802.11 ワイヤレス LAN インターフェイスなど、他のメディア タイプに適用可能でないです。 または、[全般] で NDIS。

-   特定の状況で NDIS 6.1 以降、 [ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)構造は、受信したイーサネット フレームに対して複数のメモリ記述子リスト (MDLs) と関連付けることができます。 場合でも、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体は、1 つを含める必要があります**NET\_バッファー**複数 MDLs を使用して、構造体別のバッファーに受信したパケット データを分割するドライバーをできます。

    たとえば、ヘッダー データの分割インターフェイスをサポートするイーサネットのドライバーは、1 つに関連付けられている複数の MDLs のリンク リストを使用して受信したイーサネット フレームを分割[ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)構造体。 詳細については、次を参照してください。[ヘッダー データの分割](header-data-split.md)します。

    単純さとパフォーマンスの理由から、強くお勧めヘッダー データの分割をサポートしていないドライバーがそれぞれに 1 つだけ MDL を使用[ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)構造体。

    **注**  Windows Vista では、NDIS 6.0 の各[ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)構造体は、1 つだけ MDL を含める必要があります。

     

-   ドライバーの最初の MDL 数以上のバイトを先読みサイズに指定された NDIS として含まれていない場合は、IP ヘッダー、IPv4 のオプション、IPsec のヘッダー、IPv6 拡張ヘッダー、または、上位層プロトコル ヘッダーの途中で受信したイーサネット フレームを分割する必要があります。

NDIS プロトコルとフィルター ドライバー受け取る必要がありますでイーサネット フレームの分割のサポートがない場合、このような分割フレームは、上記のリスト項目内で定義されている制限に準拠します。 制限は、プロトコルとフィルター ドライバーが Windows の将来のバージョンと互換性があることを確認します。

 

 





