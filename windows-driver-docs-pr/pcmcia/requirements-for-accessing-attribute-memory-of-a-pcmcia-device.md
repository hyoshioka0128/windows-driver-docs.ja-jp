---
title: PCMCIA デバイスの属性メモリにアクセスするための要件
description: PCMCIA デバイスの属性メモリにアクセスするための要件
ms.assetid: 8af41eb0-c057-43c9-a50f-b7d88e1bed6a
keywords:
- 属性のメモリ バス WDK PCMCIA の要件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab5842d6563c014284cc57311aaaa2192af397df
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378311"
---
# <a name="requirements-for-accessing-attribute-memory-of-a-pcmcia-device"></a>PCMCIA デバイスの属性メモリにアクセスするための要件





このセクションでは、PCMCIA デバイスの属性のメモリへのアクセスの種類は次の要件について説明します。

<a href="" id="query-device-information"></a>**デバイス情報の照会**  
ドライバーは、通常、次のデバイス情報を照会します。

-   デバイスの id

-   容量またはドライバーを使用してデバイスを構成する速度などのデバイス パラメーター

-   MAC アドレスなどの静的なデータ

情報のクエリは通常読み取り専用、および頻度が比較的少ないが完了します。

<a href="" id="configure-a-device"></a>**デバイスを構成します。**  
一部のドライバーでは、属性のメモリ内の構成のレジスタへの書き込みアクセスが必要です。

ドライバーは通常、デバイスを頻度の低い構成します。

PCMCIA バス ドライバーが属性メモリでは、標準の PCMCIA 構成レジスタを管理することに注意してください。 ドライバーは、これらのレジスタに書き込む必要があります。 場合は、システムが予期しない動作が発生することができます。 システムのセットアップと、プラグ アンド プレイ マネージャなど INF ファイルのディレクティブでのサポート、 [ **INF LogConfig ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff547448) -を使用してこれらのレジスタを構成する必要があります。

<a href="" id="operate-a-device"></a>**デバイスを動作します。**  
PCMCIA デバイスによっては、属性のメモリ内にあるコントロール レジスタを使用します。 ドライバー、ISR. 内でこれらのレジスタに直接アクセスする必要があります通常 この種類のアクセスでは、[頻度] で比較的多くなりますでき、高速ダイレクト メモリ アクセスを必要とすることができます。

 

 





