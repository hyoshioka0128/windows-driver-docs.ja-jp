---
title: Windows カーネル モードの HAL ライブラリ
description: Windows カーネル モードの HAL ライブラリ
ms.assetid: 5cfdbf1b-b856-4a0c-9f56-3879482819aa
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7713713e19ee43bb0f47a149c08456ad850f22f0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551165"
---
# <a name="windows-kernel-mode-hal-library"></a>Windows カーネル モードの HAL ライブラリ


Windows は、パーソナル コンピューターのさまざまな構成で実行されます。 各構成には、ハードウェアとオペレーティング システムの残りの部分の間でやり取りするソフトウェアのレイヤーが必要です。 この層は、ドライバーやオペレーティング システムからの (非表示にします)、低レベル ハードウェアの詳細を抽象化であるために、ハードウェア アブストラクション レイヤー (HAL) が呼び出されます。

開発者は、独自の HAL を記述することをお勧めします。 ハードウェアへのアクセスを必要がある場合、HAL ライブラリは、目的のために使用できるルーチンを提供します。 インターフェイスを持つ、HAL の文字が付いて直接ルーチン"**Hal**"HAL のルーチンの一覧を参照してください。[ハードウェア アブストラクション レイヤー (HAL) ライブラリ ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff546644)します。

 

 




