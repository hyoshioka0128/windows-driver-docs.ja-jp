---
title: R (Windows デバッガーの用語集)
description: 用語集ページ - R
Robots: noindex, nofollow
ms.assetid: 77bd1a66-39b3-4990-801e-4192a6e9cf47
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86867e78f0da56f9458801e53829532a5f3c6ea1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335539"
---
# <a name="r"></a>R


<span id="remote_debugging"></span><span id="REMOTE_DEBUGGING"></span>**リモート デバッグ**  
リモート デバッグは、リモート接続を使用してデバッグを実行する方法です。

1 台のコンピューターは、ユーザー モードのデバッグは実行は通常、ため 2 つのマシン ユーザー モードのリモート デバッグ通常使用します。 このシナリオで 1 台のコンピューターが含まれています、ターゲット アプリケーションとデバッグ サーバーの場合は、その他のコンピューターにデバッグのクライアントが含まれています。 別の方法では、対象のアプリケーションと 1 台のコンピューター上のプロセス サーバーと他のスマート クライアントがあります。

以降、カーネル モードのデバッグは、通常 2 つのマシンで行われます、カーネル モードのリモート デバッグ、3 つのマシンが必要です。 対象のコンピュータは、デバッグ中のコンピューターです。 ターゲット サーバーを接続します。カーネル モードのデバッガーが含まれています。 クライアントは、セッションをリモートで制御されるコンピューターです。 通常、1 台のコンピューターにデバッグの対象も別に、デバッグのサーバーが含まれています。、、3 番目のデバッグのクライアントが含まれています。

さらに、リモート デバッグの他のメソッドがある: リモート ツールを使用して、KD 接続のサーバーを使用して、または repeater を使用します。 選択する必要がある方法は、問題のコンピューターと利用可能な接続の構成によって異なります。

詳細については、次を参照してください。[リモート デバッグ](remote-debugging.md)します。

<span id="register"></span><span id="REGISTER"></span>**登録**  
CPU の非常に高速な一時メモリ位置。

<span id="register_context"></span><span id="REGISTER_CONTEXT"></span>**コンテキストに登録します。**  
すべてのプロセッサのレジスタを含む完全なプロセッサの状態。

詳細については、次を参照してください。 [**登録コンテキスト**](-thread--set-register-context-.md)します。

<span id="retail_build"></span><span id="RETAIL_BUILD"></span>**製品版ビルド**  
無料のビルドを参照してください。

 

 





