---
title: シリアル デバイスの制御要求
description: シリアル デバイスの制御要求
ms.assetid: 12dab038-e4da-47b5-ada8-e1c7ee980cde
keywords:
- シリアルデバイス WDK、デバイス制御要求
- デバイスコントロールが WDK シリアルデバイスを要求する
- Serial driver WDK、デバイス制御要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e55a2fe562876c41ddc1ff34dab7732f278cad0d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845394"
---
# <a name="serial-device-control-requests"></a>シリアル デバイスの制御要求

Serial は、16550 UART 互換インターフェイスをサポートするシリアルデバイスの操作を制御するためのデバイスコントロール要求を提供します。

Serial では、クライアントが次のタスクを実行するために使用できる、**シリアル\_XXX 要求の IOCTL\_** をサポートしています。

- コントロールのレジスタとコントロールのシグナルを取得および設定します。

- 線コントロールとモデムコントロールを取得および設定します。

- FIFO コントロールを設定します。

- ハンドシェイクとフロー制御操作およびパラメーターを取得して設定します。

- 待機イベントを取得して設定します。

- 内部バッファーを削除し、受信バッファーサイズを設定して、デバイスをリセットします。

- 読み取り要求と書き込み要求に使用されるタイムアウトを取得して設定します。

- パフォーマンス統計情報を取得してクリアします。

- ステータス情報を取得します。

- デバイスのプロパティを取得します。

Serial は、信頼されたカーネルモードクライアントが次のタスクを実行するために使用できる、 **\_シリアル\_内部\_XXX**要求の IOCTL をサポートしています。

- デバイスの基本設定を設定し、以前の設定を復元します。

- デバイスの待機/ウェイク操作を無効にして有効にします。

[COM ポート](configuration-of-com-ports.md)の高レベル操作の詳細については、Microsoft Windows SDK で Windows ベースサービスによってサポートされる通信リソースに関する情報を参照してください。

シリアル i/o 要求の詳細については、[シリアルポート](https://docs.microsoft.com/windows-hardware/drivers/ddi/_serports/)のリファレンスに関するトピックを参照してください。

IOCTL\_SERIAL\_XXX および IOCTL\_SERIAL\_内部\_XXX 要求の詳細については、 [ntddser](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/ntddser/)ヘッダーを参照してください。
