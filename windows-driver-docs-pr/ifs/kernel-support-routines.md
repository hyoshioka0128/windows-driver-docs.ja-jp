---
title: カーネルサポートルーチン
description: カーネルサポートルーチン
ms.assetid: aa4a1a16-06df-4795-ac26-5728e6f2df11
ms.date: 09/30/2019
ms.localizationpriority: medium
ms.openlocfilehash: 2316874463bdd7e66397f2edbed1b2f0f6825de4
ms.sourcegitcommit: c23a403b3ebea05bde96067b678a318ca9b0cabe
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71955802"
---
# <a name="kernel-support-routines"></a>カーネルサポートルーチン

次の表は、システムによって提供されるカーネルサポートルーチンのうち、カーネルモードのファイルシステムとファイルシステム (ミニフィルターおよびレガシ) フィルタードライバーで使用できるものの一部を示しています。システムで使用するために予約されています。 次のルーチンは、デバイスドライバーでは使用できません。

ここに記載されているルーチンに加えて、ファイルシステムとファイルシステムフィルタードライバーは、「カーネルモードドライバーアーキテクチャリファレンス」セクションで説明されている、ntifs で宣言されているすべての**Ke**_Xxx_ルーチンを呼び出すこともでき*ます。* .

**ヘッダーファイル:** *ntifs*

** プレフィックス:Ke @ no__t-0_Xxx_

| 関数またはマクロ | 説明 |
| ----------------- | ----------- |
| **KeAcquireQueuedSpinLock** | システム用に予約されています。 |
| **KeAttachProcess** | 使われていません。 代わりに**Kestackattachprocess**を使用してください。 |
| **KeDetachProcess** | 使われていません。 代わりに**Keunstackattachprocess**を使用してください。 |
| **KeInitializeMutant** | システム用に予約されています。 「 **KeInitializeMutex**」を参照してください。 |
| **KeInitializeQueue** | スレッドがエントリを待機できるキューオブジェクトを初期化します。 |
| **KeInsertHeadQueue** | エントリをすぐに使用してスレッド待機を満たすことができない場合は、指定されたキューの先頭にエントリを挿入します。|
| **KeInsertQueue** | エントリをすぐに使用してスレッド待機を満たすことができない場合は、指定されたキューの末尾にエントリを挿入します。 |
| **KeReadStateMutant** | システム用に予約されています。 「 **KeReadStateMutex**」を参照してください。 |
| **KeReadStateQueue** | システム用に予約されています。 |
| **KeReleaseMutant** | システム用に予約されています。 「 **KeReleaseMutex**」を参照してください。 |
| **KeReleaseQueuedSpinLock** | システム用に予約されています。 |
| **KeRemoveQueue** | 呼び出し元のスレッドに、指定されたキューオブジェクトからデキューされたエントリへのポインターを与えるか、またはキューオブジェクトのタイムアウト間隔 (オプション) を呼び出し元が待機できるようにします。 |
| **KeRundownQueue** | キューオブジェクトをクリーンアップし、キューに入っているエントリをフラッシュします。 |
| **KeSetIdealProcessorThread** | システム用に予約されています。 |
| **KeStackAttachProcess** | 現在のスレッドをターゲットプロセスのアドレス空間にアタッチします。 |
| **KeTryToAcquireQueuedSpinLock** | システム用に予約されています。 |
| **KeUnstackDetachProcess** | プロセスのアドレス空間から現在のスレッドをデタッチし、直前のアタッチ状態を復元します。 このルーチンは細心の注意を払って使用してください。 (「解説」を参照してください)。 |
