---
title: I/O 要求の Serenum によるフィルター処理
description: I/O 要求の Serenum によるフィルター処理
ms.assetid: 773688b8-3d5a-48ed-8f20-368cf35fa6e2
keywords:
- Serenum.sys ドライバー WDK、i/o 要求フィルター
- I/o 要求フィルター WDK の Serenum.sys
- i/o 要求をフィルタする WDK シリアルデバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bdcce5256b7ac05fe328a3e6c4b6beb9eb4db56
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845395"
---
# <a name="serenum-filtering-of-io-requests"></a>I/O 要求の Serenum によるフィルター処理

次に、フィルターに送られる、Serenum.sys が i/o 要求をフィルター処理する方法について説明します。

- プラグアンドプレイと電源要求に関連付けられているバス関連の操作を処理します。
    -   PDO が存在する場合は、フィルターを削除します。
    -   IRP\_に応答して RS-232 ポートを列挙します。 [ **\_クエリ\_デバイス\_関係**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)の種類が**busrelations**であることを要求します。
- RS-232 ポートに関する情報を返す、Serenum.sys 固有のデバイス制御要求を完了します。

次に、Serenum.sys が PDO に送信される i/o 要求をフィルター処理する方法について説明します (PDO は、RS-232 ポートに接続されている子デバイスを表します)。

- すべてのプラグアンドプレイと電源要求を完了します。

- PDO に関連付けられているフィルターにデバイス制御要求を再ルーティングします。

- RS-232 ポートのバス関係を無効にする、Serenum.sys 固有の内部デバイス制御要求を完了します。

詳細については、以下を参照してください。

- [ntddser ヘッダー](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/)

- Windows Driver Kit (WDK) の \\src\\カーネル\\serenum.sys ディレクトリのサンプルコード
