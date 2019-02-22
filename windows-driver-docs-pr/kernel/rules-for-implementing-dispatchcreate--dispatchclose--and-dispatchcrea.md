---
title: DispatchCreate、DispatchClose、および DispatchCreateClose ルーチンを実装するための規則
description: DispatchCreate、DispatchClose、および DispatchCreateClose ルーチンを実装するための規則
ms.assetid: 4ce37675-92a6-41c2-b386-6570c989e56c
keywords:
- ディスパッチ ルーチンの WDK カーネル、DispatchCreate ルーチン
- ディスパッチ ルーチンの WDK カーネル、DispatchClose ルーチン
- ディスパッチ ルーチンの WDK カーネル、DispatchCreateClose ルーチン
- DispatchCreateClose ルーチン
- DispatchClose ルーチン
- DispatchCreate ルーチン
- Irp_mj_create 用 I/O 関数のコード
- 未完了の I/O 関数のコード
- ディスパッチ ルーチン WDK カーネルを作成します。
- ディスパッチ ルーチン WDK カーネルを閉じる
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5c955c734e5c0a1166f59367f44eaa952004712
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528858"
---
# <a name="rules-for-implementing-dispatchcreate-dispatchclose-and-dispatchcreateclose-routines"></a>DispatchCreate、DispatchClose、および DispatchCreateClose ルーチンを実装するための規則





実装する場合、次の点を留意してください*DispatchCreate*、 *DispatchClose*、および*DispatchCreateClose*ルーチン。

-   少なくとも、ルーチンは、次の操作を行う必要があります。
    1.  設定、**状態**フィールドを適切な NTSTATUS、通常の状態で入力 IRP の I/O 状態ブロックの\_成功します。
    2.  設定、**情報**をゼロに入力 IRP の I/O 状態ブロックのフィールド。
    3.  呼び出す**IoCompleteRequest** IRP と*PriorityBoost* IO の\_いいえ\_インクリメントします。
    4.  戻り値の設定、NTSTATUS、**状態**IRP の I/O 状態ブロックのフィールド。
-   最上位レベルまたは中間のドライバー、ルーチンは、基になるデバイスのまたはドライバーのデザインとそのデバイスの性質に応じて、要求を閉じたり、作成を処理する追加の作業を行う必要があります。

-   作成要求論理的または物理的なデバイスを表すファイル オブジェクトを開くには、最上位レベルのドライバーを確認する必要があります、 **FileObject.FileName** 、I/O スタックの場所と、完了ステータスの IRP\_成功した場合Unicode 文字列に**FileName**長さは 0。 ステータスの IRP を完了する必要がありますそれ以外の場合、\_無効な\_パラメーター。

-   最下位レベルのドライバーのルーチンが呼び出されるは、次のより高いレベルのドライバーを呼び出すときにだけ**IoAttachDeviceToDeviceStack**、 **IoGetDeviceObjectPointer**、または**IoAttachDevice**. 複数層のドライバーのチェーンの最下位レベルのドライバーは、作成または終了要求の処理に必要な最低限を頻繁に発生します。

 

 




