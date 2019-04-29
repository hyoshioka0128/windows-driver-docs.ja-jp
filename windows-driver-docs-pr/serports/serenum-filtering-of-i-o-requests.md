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
ms.openlocfilehash: 54cb265b18808dd93928bd0d253b785a9eef4562
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387964"
---
# <a name="serenum-filtering-of-io-requests"></a>I/O 要求の Serenum によるフィルター処理





Serenum フィルター、フィルターに転送される I/O 要求の操作方法を次に示します。

-   プラグ アンド プレイと電源の要求に関連付けられている bus 関連の操作を処理します。
    -   フィルター操作を行いますが削除されると、存在する場合、PDO を削除します。
    -   Rs-232 ポートへの応答を列挙する[ **IRP\_MN\_クエリ\_デバイス\_リレーション**](https://msdn.microsoft.com/library/windows/hardware/ff551670)型の要求**BusRelations**.
-   Rs-232 ポートに関する情報を返す Serenum に固有のデバイス制御リクエストを完了します。

Serenum (PDO は rs-232 ポートに接続されている子デバイスを表します) PDO 宛ての I/O 要求をフィルター処理する方法を次に示します。

-   すべてのプラグ アンド プレイと電源ケーブルが完了する要求。

-   フィルターに全く流れませんデバイス制御の要求に関連付けられて、PDO の操作を行います。

-   Serenum 固有の内部デバイス制御要求を rs-232 ポートで bus リレーションを無効にするを完了します。

詳細については、以下を参照してください。

-   [Serenum ドライバー リファレンス](https://msdn.microsoft.com/library/windows/hardware/ff547040)

-   サンプル コード、 \\src\\カーネル\\serenum ディレクトリ Windows Driver Kit (WDK) で

 

 




