---
title: シリアル デバイスの制御要求
description: シリアル デバイスの制御要求
ms.assetid: 12dab038-e4da-47b5-ada8-e1c7ee980cde
keywords:
- WDK シリアル デバイスは、デバイスの制御を要求します。
- WDK シリアル デバイスを要求するデバイスの制御
- シリアル ドライバー WDK では、デバイス制御の要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3bd13858c56d71b65443e3858ef418df7e94dde
ms.sourcegitcommit: 6a0636c33e28ce2a9a742bae20610f0f3435262c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/17/2019
ms.locfileid: "65836322"
---
# <a name="serial-device-control-requests"></a>シリアル デバイスの制御要求

シリアル 16550 UART と互換性のあるインターフェイスをサポートするシリアル デバイスの操作を制御するデバイス制御の要求を提供します。

シリアル サポート**IOCTL\_シリアル\_XXX**次のタスクを実行するクライアントが使用できることを要求します。

- Get および set レジスタを制御し、信号を制御します。

- Get と行の制御の設定とモデムのコントロール。

- FIFO コントロールを設定します。

- 取得し、ハンドシェイクおよびフロー制御操作とパラメーターを設定します。

- Get と set は、イベントを待機します。

- 内部バッファーを消去するデバイスをリセットして受信バッファー サイズを設定します。

- 取得し、読み取りに使用され、書き込み要求のタイムアウトを設定します。

- 取得し、パフォーマンスの統計情報をクリアします。

- ステータス情報を取得します。

- デバイスのプロパティを取得します。

シリアル サポート**IOCTL\_シリアル\_内部\_XXX**次のタスクを実行する、信頼されたカーネル モードのクライアントを使用できることを要求します。

- デバイスの基本設定を設定し、以前の設定を復元します。

- 無効にし、デバイスの待機またはスリープ解除操作を有効にします。

高度な操作の詳細については[COM ポート](configuration-of-com-ports.md)、Microsoft Windows SDK の Windows ベースのサービスでサポートされている通信リソースに関する情報を参照してください。

シリアル I/O 要求の詳細については、次を参照してください。、[シリアル ポート](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_serports/)のトピックを参照します。

詳細については、IOCTL\_シリアル\_XXX と IOCTL\_シリアル\_内部\_XXX 要求を参照してください、 [ntddser.h](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ntddser/)ヘッダー。
