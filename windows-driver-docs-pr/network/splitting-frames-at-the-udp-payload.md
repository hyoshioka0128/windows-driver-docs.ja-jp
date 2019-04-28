---
title: UDP ペイロードでのフレームの分割
description: UDP ペイロードでのフレームの分割
ms.assetid: 10116077-89d2-4d07-9807-46b6281e9851
keywords:
- WDK のネットワー キング、UDP ペイロードを分割するイーサネット フレーム
- UDP ペイロード WDK のヘッダー データの分割
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d7bab3ef1e3245fd42b2516e7e5818d9634be25
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382202"
---
# <a name="splitting-frames-at-the-udp-payload"></a>UDP ペイロードでのフレームの分割





ヘッダー データの分割をサポートする NDIS ミニポート アダプターでは、UDP のフレームの上にレイヤー プロトコル ヘッダーを分割のフレームをサポートする必要があります。 ただし、NIC は、UDP ペイロードの先頭のフレームを分割する必要がありますまずします。

NIC できない場合、結果のヘッダーのバッファーがある最大ヘッダー サイズより大きい長さ UDP フレームに分割することがあります。 ヘッダーの最大サイズを超えたときに、フレームを分割の詳細については、次を参照してください。[ヘッダーのバッファーを割り当てる](allocating-the-header-buffer.md)します。

NIC には、UDP ペイロードにフレームを分割できません、か NIC 上のレイヤー プロトコル ヘッダーの先頭のフレームに分割する必要があります、フレームを分割する必要があります。 上のレイヤー プロトコル ヘッダーの先頭のフレームの分割の詳細については、次を参照してください。[上のレイヤー プロトコル ヘッダーの先頭のフレームの分割](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)します。

プロバイダーが UDP ペイロードを指定された位置のフレームを分割する場合は、ヘッダー データの分割[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体は、NDIS をいる必要があります\_NBL\_フラグ\_IS\_UDP および NDIS\_NBL\_フラグ\_分割\_で\_上限\_レイヤー\_プロトコル\_ペイロードのフラグのセット、 **NblFlags**メンバー。 ヘッダー データの設定の詳細については、NET を分割の\_バッファー\_フラグの一覧を参照してください[設定 NET\_バッファー\_情報を一覧表示](setting-net-buffer-list-information.md)します。

 

 





