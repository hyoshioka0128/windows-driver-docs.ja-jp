---
title: Windows カーネルモード HAL ライブラリ
description: Windows カーネルモード HAL ライブラリ
ms.assetid: 5cfdbf1b-b856-4a0c-9f56-3879482819aa
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a9d1e723dfef0cb4e6e8709244e8f8cc4aad1c0f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358057"
---
# <a name="windows-kernel-mode-hal-library"></a>Windows カーネルモード HAL ライブラリ


Windows は、パーソナル コンピューターのさまざまな構成で実行されます。 各構成には、ハードウェアとオペレーティング システムの残りの部分の間でやり取りするソフトウェアのレイヤーが必要です。 この層は、ドライバーやオペレーティング システムからの (非表示にします)、低レベル ハードウェアの詳細を抽象化であるために、ハードウェア アブストラクション レイヤー (HAL) が呼び出されます。

開発者は、独自の HAL を記述することをお勧めします。 ハードウェアへのアクセスを必要がある場合、HAL ライブラリは、目的のために使用できるルーチンを提供します。 インターフェイスを持つ、HAL の文字が付いて直接ルーチン"**Hal**"HAL のルーチンの一覧を参照してください。[ハードウェア アブストラクション レイヤー (HAL) ライブラリ ルーチン](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546644(v=vs.85))します。

 

 




