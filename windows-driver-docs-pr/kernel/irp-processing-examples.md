---
title: IRP 処理の例
description: IRP 処理の例
ms.assetid: 1bf555c7-87fd-43c2-ab74-aa6f9133f808
keywords:
- Irp WDK カーネル、処理の例
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e260d544a234589bf768669db5902d5685adfbc4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381392"
---
# <a name="irp-processing-examples"></a>IRP 処理の例





次のセクションでは、2 つのプロトタイプのドライバーの Irp を処理する方法について説明します。 大容量記憶装置デバイスの最下位レベルのドライバーのプロトタイプは 1 つです。 中間レベルのプロトタイプは、他の*ミラー ドライバー*、上の記憶域ドライバー スタックの最下位レベルのドライバーが存在します。 (ミラー ドライバーが複数のドライバーをすべての書き込み要求を複製および代替が重複しているドライブ間で要求を読み取り)。

[最下位レベルのドライバーの Irp の処理](processing-irps-in-a-lowest-level-driver.md)

[中間レベルのドライバーは Irp の処理](processing-irps-in-an-intermediate-level-driver.md)

作成および詳細について Irp の送信については、次を参照してください。 [Irp – チート シートの処理のさまざまな方法](https://go.microsoft.com/fwlink/?linkid=834615)します。

