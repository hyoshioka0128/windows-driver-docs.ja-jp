---
title: Windows によって開かれる最上位のコレクション (システムで使用)
description: Windows によって開かれる最上位のコレクション (システムで使用)
ms.assetid: e489ce46-379e-4ba9-a0e3-5848b1f4a17b
keywords:
- 最上位のコレクション WDK HID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 310793a6853c78fd7382274cb7353d697d9c4dd4
ms.sourcegitcommit: f8c3585ec7b1bdfcd65f7f2cc9aa688655de4d20
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/15/2020
ms.locfileid: "81396312"
---
# <a name="top-level-collections-opened-by-windows-for-system-use"></a>Windows によって開かれる最上位のコレクション (システムで使用)

Windows では、システム使用のために次の[最上位レベルのコレクション](top-level-collections.md)が開きます。

| デバイスの種類            | [使用状況] ページ | 使用状況 ID | Windows クライアント                                                                                     | アクセス モード |
|------------------------|:----------:|:--------:|----------------------------------------------------------------------------------------------------|-------------|
| ポインター                | 0x01       | 0x01     | Win32 サブシステム                                                                                    | ［排他］   |
| マウス                  | 0x01       | 0x02     | Win32 サブシステム                                                                                    | ［排他］   |
| ジョイ               | 0x01       | 0x04     | DirectInput                                                                                        | Shared      |
| ゲームパッド               | 0x01       | 0x05     | DirectInput                                                                                        | Shared      |
| キーボード               | 0x01       | 0x06     | Win32 サブシステム                                                                                    | ［排他］   |
| キーパッド                 | 0x01       | 0x07     | Win32 サブシステム                                                                                    | ［排他］   |
| システム コントロール         | 0x01       | 0x80     | Win32 サブシステム                                                                                    | Shared      |
| コンシューマーオーディオコントロール | 0x0C       | 0x01     | Microsoft Windows XP の Windows 2000 および hidserv (SVC ホストサービスの1つ) での hidserv | Shared      |
