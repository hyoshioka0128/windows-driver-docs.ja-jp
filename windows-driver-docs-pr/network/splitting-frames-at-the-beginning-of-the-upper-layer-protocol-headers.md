---
title: 上位層プロトコル ヘッダーの先頭のフレームの分割
description: 上部レイヤー プロトコル ヘッダーの先頭のフレームの分割
ms.assetid: 2559ac20-46dc-4116-9d12-b2cd634e501b
keywords:
- ネットワーク、上位層プロトコルの先頭に WDK を分割するイーサネット フレーム
- 上位層プロトコル WDK ヘッダー以外のデータの分割します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 769476ae9cece501fc773eaf2773e1c100461afa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392904"
---
# <a name="splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers"></a>上部レイヤー プロトコル ヘッダーの先頭のフレームの分割





*上位層プロトコル*は TCP、UDP、ICMP などの IP トランスポート プロトコルです。

**注**  IPsec、上のレイヤー-プロトコル ヘッダー データの分割の要件とは見なされません。 IPsec のフレームの分割の詳細については、次を参照してください。 [IPsec フレームの分割](splitting-ipsec-frames.md)します。

 

NIC が、指定された上限-レイヤー プロトコル ヘッダーの先頭に、イーサネット フレームを分割するかどうかは[ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376) MDLs を正確に 2 つを含める必要があります。 最初の MDL を表すバッファーは、イーサネット フレーム (MAC ヘッダー) の最初のバイトを始める必要があり、上のレイヤー プロトコル ヘッダーの最初のバイトを示す 2 つ目の MDL バッファーを開始する必要があります。

**注**  NIC は、TCP または UDP ペイロードで TCP および UDP のフレームを分割できます。 詳細については、次を参照してください。 [TCP ペイロードで分割フレーム](splitting-frames-at-the-tcp-payload.md)と[UDP ペイロードにフレームを分割](splitting-frames-at-the-udp-payload.md)します。

 

プロバイダーが、指定された上限-レイヤー プロトコル ヘッダーの先頭のフレームを分割する場合は、ヘッダー データの分割[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造があります、NDIS\_NBL\_フラグ\_分割\_で\_上限\_レイヤー\_プロトコル\_ヘッダー フラグを設定、 **NblFlags**メンバー。 ヘッダー データの設定の詳細については、NET を分割の\_バッファー\_フラグの一覧を参照してください[設定 NET\_バッファー\_情報を一覧表示](setting-net-buffer-list-information.md)します。

NIC 結果のヘッダーのバッファーがある最大ヘッダー サイズよりも長い場合フレームを分割する必要があります。 ヘッダーの最大サイズを超えたときに、フレームを分割の詳細については、次を参照してください。[ヘッダーのバッファーを割り当てる](allocating-the-header-buffer.md)します。

 

 





