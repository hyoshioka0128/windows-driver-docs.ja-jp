---
title: メインの I/O パス
description: メインの I/O パス
ms.assetid: 643842e4-a75e-4d86-a1f7-d1a4468b5e17
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5addbfc40365043d8cfed8f03674968192b7cca9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355570"
---
# <a name="main-io-path"></a>メインの I/O パス


Storport で提供するアーキテクチャの機能強化の 1 つは、HwBuildIo ルーチンです。 この Storport ミニポートのドライバー エントリ ポイントはオプションですが、強くお勧めします。 LSI\_U3 ドライバーは、この機能強化を活用 LsiU3BuildIo ルーチンを実装します。 このエントリ ポイントは、ロックなしの HwStartIo ルーチンが保持し、このルーチンが Scsiport ベース ミニポート ドライバーの場合、HwStartIo ルーチンで行われていた処理を実行できます共有メモリを変更しない限り、前に呼び出されます。 これにより、ほとんどのマルチプロセッサ システムで並列に実行する別の I/O 要求を開始するために必要な処理ができます。

LsiU3StartIo ルーチンでは、I/O 要求をキューのドライバーのタグを割り当てます。 これは、Storport で LUN ごとに、アダプターではなくキューのタグを割り当てるために必要です。 アダプターのハードウェアは、256 の未処理 I/o 数の最大数に制限されます。

 

 




