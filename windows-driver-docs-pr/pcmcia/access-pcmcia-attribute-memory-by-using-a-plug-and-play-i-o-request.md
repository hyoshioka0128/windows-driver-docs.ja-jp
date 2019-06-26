---
title: PnP I/O 要求を使用してアクセスのメモリ
description: プラグ アンド プレイの I/O 要求を使用して PCMCIA 属性メモリにアクセスする
ms.assetid: ee2f9d9f-9e2b-4ecf-ba6d-4baad3653301
keywords:
- 属性のメモリ バスの WDK PCMCIA、プラグ アンド プレイの I/O 要求します。
- プラグ アンド プレイ WDK PCMCIA バス
- PnP WDK PCMCIA バス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a59e862d6b311de6174417a7a930fcf5d82b82ec
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382603"
---
# <a name="access-pcmcia-attribute-memory-by-using-a-plug-and-play-io-request"></a>プラグ アンド プレイの I/O 要求を使用して PCMCIA 属性メモリにアクセスする





このセクションでは、PC カードまたは Cardbus カードのドライバーがプラグ アンド プレイ I/O 要求を使用して、属性のメモリにアクセスする方法について説明します。

ドライバーは、通常、デバイスを構成するのにか、デバイスから情報を取得するのにデバイスを初期化するためにこのメソッドを使用します。 I/O オーバーヘッドが許容されると、IRQL で、アクセスを行うことができる場合、ドライバーはこのメソッドを使用する必要があります&lt;ディスパッチ\_レベル。

ドライバーではこのメソッドを IRQL での実行中にのみ使用できます&lt;ディスパッチ\_レベル。

ドライバーは、次の一連の操作を実行します。

-   作成し、新しい IRP の初期化\_MJ\_PNP 要求。

    ドライバーでは、いずれかを指定します、 [ **IRP\_MN\_読み取り\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-read-config)または[ **IRP\_MN\_書き込み\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-write-config)マイナー関数。

-   スタックの次の位置を取得します。

-   次のメンバーを設定、 **Parameters.ReadWriteConfig**新しいスタックの場所で構造体。

    <a href="" id="whichspace"></a>**WhichSpace**  
    Pc カード値を示す\_属性\_メモリ。

    <a href="" id="buffer"></a>**バッファー**  
    アクセス、ドライバーによって割り当てられるページ メモリ バッファーへのポインター。 書き込み操作の場合は、バッファーには、構成領域に書き込むデータが含まれています。 読み取り操作の場合は、バッファーは、ゼロで埋められますバッファーです。 要求が完了すると、このバッファーは、デバイスから読み取る属性メモリのコピーを保持します。

    <a href="" id="offset"></a>**オフセット**  
    WORD の読み取りまたは書き込み操作の開始位置属性メモリのベースからのオフセットを指定します。

    <a href="" id="length"></a>**長さ**  
    要求のドライバーによって割り当てられるバッファーのバイト サイズを指定します。

-   完了ルーチンを設定します。

-   デバイス スタックの要求を送信します。

 

 





