---
title: I/O 要求の Serenum によるフィルター処理
description: I/O 要求の Serenum によるフィルター処理
ms.assetid: 773688b8-3d5a-48ed-8f20-368cf35fa6e2
keywords:
- Serenum ドライバー WDK、I/O 要求のフィルタ リング
- I/O 要求の WDK Serenum をフィルター処理
- WDK シリアル デバイスを要求する I/O のフィルター処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 128f189dd6971d3645bc6562edd036a4b80d4c43
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356763"
---
# <a name="serenum-filtering-of-io-requests"></a>I/O 要求の Serenum によるフィルター処理

Serenum フィルター、フィルターに転送される I/O 要求の操作方法を次に示します。

- プラグ アンド プレイと電源の要求に関連付けられている bus 関連の操作を処理します。
    -   フィルター操作を行いますが削除されると、存在する場合、PDO を削除します。
    -   Rs-232 ポートへの応答を列挙する[ **IRP\_MN\_クエリ\_デバイス\_リレーション**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)型の要求**BusRelations**.
- Rs-232 ポートに関する情報を返す Serenum に固有のデバイス制御リクエストを完了します。

Serenum (PDO は rs-232 ポートに接続されている子デバイスを表します) PDO 宛ての I/O 要求をフィルター処理する方法を次に示します。

- すべてのプラグ アンド プレイと電源ケーブルが完了する要求。

- フィルターに全く流れませんデバイス制御の要求に関連付けられて、PDO の操作を行います。

- Serenum 固有の内部デバイス制御要求を rs-232 ポートで bus リレーションを無効にするを完了します。

詳細については、以下を参照してください。

- [ntddser.h header](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/)

- サンプル コード、 \\src\\カーネル\\serenum ディレクトリ Windows Driver Kit (WDK) で
