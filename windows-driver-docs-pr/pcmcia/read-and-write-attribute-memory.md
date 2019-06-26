---
title: 属性メモリの読み取りと書き込み
description: 属性メモリの読み取りと書き込み
ms.assetid: 8e430057-b68a-4edc-8755-1d7255412269
keywords:
- PCMCIA WDK バス、属性のメモリ
- WDK PCMCIA のバスのメモリ、読み取りと書き込みを属性します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc8a12e30b47c83c1d3fc112e0099481745fa595
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382621"
---
# <a name="read-and-write-attribute-memory"></a>属性メモリの読み取りと書き込み





このセクションでは、できる PCMCIA ドライバーの読み取りおよび PCMCIA のメモリ カードに属性のメモリを書き込みの方法について説明します。

Windows 2000 と以降のオペレーティング システムは、構成領域として PC カードまたは CardBus カードのメモリの属性を処理します。

一般に、属性のメモリにアクセスするドライバーは、する必要があります作成 IRP の主要な関数のコードを使用して IRP\_MJ\_PNP とマイナーの関数コード[ **IRP\_MN\_読み取り\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-read-config)または[ **IRP\_MN\_書き込み\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-write-config)します。

必要に応じて、ドライバーを永続的なメモリ ウィンドウを使用して直接属性メモリにアクセスできます。 参照してください[アクセス PCMCIA 属性メモリを介して、永続的なメモリ ウィンドウ](https://docs.microsoft.com/windows-hardware/drivers/pcmcia/access-pcmcia-attribute-memory-through-a-permanent-memory-window)の詳細。

PCMCIA メモリ カードのドライバーは、次の操作を実行します。

-   作成して、新しい IRP を初期化します。

-   スタックの次の位置を取得します。

-   新しいスタックの場所の次のメンバーを設定します。
    -   **ReadWriteConfig.WhichSpace**メンバー pc カードの値を指定する\_属性\_メモリ。
    -   **バッファー**メンバーが、ドライバーによって割り当てられた、非ページのバッファーの読み取りまたは書き込み操作を指しています。 書き込み操作の場合は、バッファーには、構成領域に書き込むデータが含まれています。 読み取り操作の場合は、バッファーは、ゼロで埋められますバッファーです。 IRP の完了時に、このバッファーは、デバイスから読み取る属性メモリのコピーに設定されます。
    -   **オフセット**メンバーがバイトの読み取りまたは書き込み操作の開始位置属性メモリ ベースからのオフセットを指定します。
    -   **長さ**メンバーがバイト単位で指定されたバッファーのサイズを指定**バッファー**します。
-   完了ルーチンを設定します。

-   ドライブ スタック ダウン要求を送信します。

IRQL でドライバーを実行する必要があります&lt;ディスパッチ\_ダウン ドライバー スタックは、この要求を送信するレベル。

 

 





