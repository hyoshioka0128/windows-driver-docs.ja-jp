---
title: R (Windows デバッガー用語集)
description: 用語集のページ-R
ms.assetid: 77bd1a66-39b3-4990-801e-4192a6e9cf47
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee55b85f9cb6a48a95cd8c0ac63d599c4de9c1f2
ms.sourcegitcommit: 48c4b6d3a504583d2f588ed892a4a281d4b58301
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2019
ms.locfileid: "70387073"
---
# <a name="r"></a>R


<span id="remote_debugging"></span><span id="REMOTE_DEBUGGING"></span>**リモートデバッグ**  
リモートデバッグは、リモート接続を使用してデバッグを実行する方法です。

ユーザーモードのデバッグは通常1台のコンピューターで行われるため、リモートユーザーモードのデバッグでは通常、2台のコンピューターが使用されます。 このシナリオでは、1台のコンピューターに対象アプリケーションとデバッグサーバーが含まれていますが、もう一方のコンピューターにはデバッグクライアントが含まれています。 別の方法として、ターゲットアプリケーションとプロセスサーバーを1台のコンピューターに、もう一方にスマートクライアントを設定する方法があります。

カーネルモードのデバッグは通常2台のコンピューターで行われるため、リモートカーネルモードのデバッグには3台のコンピューターが必要です。 ターゲットコンピューターは、デバッグ中のコンピューターです。 サーバーはターゲットに接続されています。これにはカーネルモードのデバッガーが含まれています。 クライアントは、セッションをリモートで制御しているコンピューターです。 通常、1台のコンピューターはデバッグ対象であり、もう1つはデバッグサーバーを含み、3番目のコンピューターはデバッグクライアントを含んでいます。

リモートデバッグには、リモートツールを使用する方法、KD 接続サーバーを使用する方法、またはリピータを使用する方法もあります。 選択する方法は、問題のコンピューターの構成と使用可能な接続によって異なります。

詳細については、「[リモートデバッグ](remote-debugging.md)」を参照してください。

<span id="register"></span><span id="REGISTER"></span>**取引**  
CPU 内の非常に高速な一時メモリ位置。

<span id="register_context"></span><span id="REGISTER_CONTEXT"></span>**コンテキストの登録**  
すべてのプロセッサのレジスタを含む完全なプロセッサの状態。

詳細については、「[**コンテキストの登録**](-thread--set-register-context-.md)」を参照してください。

<span id="retail_build"></span><span id="RETAIL_BUILD"></span>**製品版のビルド**  
無料ビルドを参照してください。

 

 





