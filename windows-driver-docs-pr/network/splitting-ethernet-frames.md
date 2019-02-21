---
title: イーサネット フレームの分割
description: イーサネット フレームの分割
ms.assetid: 7b857dee-2805-4004-8f31-452f0cff0e0c
keywords:
- ヘッダー データの分割 WDK、イーサネット フレームの分割
- イーサネット フレームの分割
- WDK のネットワークを分割するイーサネット フレーム
- イーサネット フレームの WDK ネットワー キング、イーサネット フレームの分割についての分割
- ヘッダー データ プロバイダー WDK の分割
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a01768105452ea638e2a5250761d0ca4fdb4c6b3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549589"
---
# <a name="splitting-ethernet-frames"></a>イーサネット フレームの分割





このセクションでは、プロバイダーの分割がイーサネット フレームの種類に応じて、ヘッダー データの分割プロバイダーに適用される特定のヘッダー データの分割要件について説明します。

**注**  イーサネット フレームの種類ごとに特定の要件を理解する以降のトピックを使用するこのトピックの「一般的な要件を読むことができます。 後半のトピックは、以前のトピックの要件をビルドします。 たとえば、フレームに IPv4 と UDP の情報が含まれている場合お読みください、 [IPv4 フレームの分割](splitting-ipv4-frames.md)と[UDP ペイロードにフレームを分割](splitting-frames-at-the-udp-payload.md)トピック。

 

ヘッダー データに準拠しているフレームの要件を指定された分割ヘッダー データ プロバイダーの分割を分割する場合は[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造があります、NDIS\_NBL\_フラグ\_HD\_分割フラグを設定、 **NblFlags**メンバー。 フラグのクリア ヘッダー データの分割プロバイダーがフレームを分割されていない場合、フレームを示す必要があります**NblFlags** :

-   NDIS\_NBL\_フラグ\_HD\_分割

-   NDIS\_NBL\_フラグ\_分割\_で\_上限\_レイヤー\_プロトコル\_ヘッダー

-   NDIS\_NBL\_フラグ\_分割\_で\_上限\_レイヤー\_プロトコル\_ペイロード

ヘッダー データの設定の詳細については、NET を分割の\_バッファー\_フラグの一覧およびその他の要件を示す値を受信しを参照してください[ヘッダー データの分割と受信の兆候](receive-indications-with-header-data-split.md)します。

ヘッダー データの分割プロバイダーがヘッダー データの分割プロバイダーの要件の外部で受信したフレームを分割できる場合があります。 このような場合は、プロバイダー分割する必要があることはありません IP ヘッダー、IPv4 のオプション、IPsec のヘッダー、IPv6 拡張ヘッダー、またはプロトコル レイヤー上のヘッダー、途中でイーサネット フレームの最初の MDL にように NDIS に指定された数以上のバイトが含まれていない場合、先読みのサイズ。 先読みサイズの詳細については、次を参照してください。 [OID\_GEN\_現在\_先読み](https://msdn.microsoft.com/library/windows/hardware/ff569574)します。

このセクションの内容:

[IPv4 のフレームの分割](splitting-ipv4-frames.md)

[IPv6 のフレームの分割](splitting-ipv6-frames.md)

[IP のフレームをフラグメント化分割](splitting-fragmented-ip-frames.md)

[上のレイヤー プロトコル ヘッダーの先頭のフレームの分割](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)

[TCP ペイロードのフレームの分割](splitting-frames-at-the-tcp-payload.md)

[UDP ペイロードにフレームの分割](splitting-frames-at-the-udp-payload.md)

[TCP と UDP 以外のフレームの分割](splitting-frames-other-than-tcp-and-udp.md)

 

 





