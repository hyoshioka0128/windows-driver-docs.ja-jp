---
title: Memory Manager のサポートルーチン
description: Memory Manager のサポートルーチン
ms.assetid: 9cdcddd7-a086-415d-a7bd-5d149019b8b4
ms.date: 09/30/2019
ms.localizationpriority: medium
ms.openlocfilehash: 283a8f97a859aa3f3a73c2ab0a4b1631d0d5e9e3
ms.sourcegitcommit: c23a403b3ebea05bde96067b678a318ca9b0cabe
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71955810"
---
# <a name="memory-manager-support-routines"></a>Memory Manager のサポートルーチン

次の表に、カーネルモードのファイルシステムとファイルシステム (ミニフィルターおよびレガシ) フィルタードライバーで使用できるシステム指定のメモリ管理サポートルーチンのサブセットを示します。 これらのルーチンは、デバイスドライバーでは使用できません。

ここに記載されているルーチンに加えて、ファイルシステムとファイルシステムフィルタードライバーは、カーネルモードドライバーアーキテクチャリファレンスで記述され、 *ntifs*で宣言されている**Mm**_Xxx_ルーチンを呼び出すこともできます。

**ヘッダーファイル:** *ntifs*

** プレフィックス:Mm @ no__t-0_Xxx_

| 関数またはマクロ | 説明 |
| ----------------- | ----------- |
| **MmCanFileBeTruncated** | ファイルを切り捨てることができるかどうかを確認します。 |
| **MmDoesFileHaveUserWritableReferences** | ファイルオブジェクトの書き込み可能な参照の数を返します。 |
| **MmFlushImageSection** | ファイルのイメージセクションをフラッシュします。 |
| **MmForceSectionClosed** | 使用されなくなったファイルのデータセクションとイメージセクションを削除します。 |
| **MmGetMaximumFileSectionSize** | 現在のバージョンの Windows で使用可能なファイルセクションの最大サイズを返します。 |
| **MmIsRecursiveIoFault** | I/o 操作中に現在のページフォールトが発生しているかどうかを判断します。 |
| **MmPrefetchPages** | 最適な方法でセカンダリストレージからページのグループを読み取ります。 |
| **MmSetAddressRangeModified** | システムキャッシュの指定された範囲の現在有効なページを変更済みとしてマークします。 |
