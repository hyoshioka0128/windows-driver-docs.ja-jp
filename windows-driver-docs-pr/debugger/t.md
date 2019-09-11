---
title: T (Windows デバッガー用語集)
description: 用語集のページ-T
ms.assetid: e17a63eb-a002-4e72-86a9-8176bf5f75d0
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9a3e3e0c7502f333517ff36a2b202344c6533cc
ms.sourcegitcommit: 48c4b6d3a504583d2f588ed892a4a281d4b58301
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2019
ms.locfileid: "70387025"
---
# <a name="t"></a>T


<span id="target"></span><span id="TARGET"></span>**接続**  
ターゲットアプリケーション、ターゲットコンピューター、またはダンプターゲット。

*デバッグ対象*と呼ばれることもあります。

<span id="target_application"></span><span id="TARGET_APPLICATION"></span>**ターゲットアプリケーション**  
ユーザーモードでデバッグされているアプリケーション。

<span id="target_computer"></span><span id="TARGET_COMPUTER"></span>**ターゲットコンピューター**  
カーネルモードでデバッグされているコンピューター。

<span id="target_id"></span><span id="TARGET_ID"></span>**ターゲット ID**  
ターゲットの一意の識別子。

<span id="target_process"></span><span id="TARGET_PROCESS"></span>**ターゲットプロセス**  
ユーザーモードのデバッグで、ターゲットアプリケーションの一部であるオペレーティングシステムプロセス。

カーネルモードのデバッグで、カーネルを表す仮想プロセス。

<span id="target_thread"></span><span id="TARGET_THREAD"></span>**ターゲットスレッド**  
ユーザーモードデバッグで、ターゲットアプリケーションのオペレーティングシステムスレッド。

カーネルモードのデバッグで、プロセッサを表す仮想スレッド。

<span id="thread_context"></span><span id="THREAD_CONTEXT"></span>**スレッドコンテキスト**  
スレッドを切り替えるときに Windows によって保持される状態。 これはレジスタコンテキストに似ていますが、レジスタコンテキストの一部であるものの、スレッドコンテキストの一部ではない追加のカーネル専用プロセッサ状態がある点が異なります。 この追加の状態は、カーネルモードのデバッグ中にレジスタとして使用できます。

詳細については、「スコープとシンボルグループ」を参照してください。

<span id="transport_layer"></span><span id="TRANSPORT_LAYER"></span>**トランスポート層**  
これにより、リモートデバッグ中のホストとターゲットコンピューター間の通信が制御されます。

<span id="trap"></span><span id="TRAP"></span>**陥る**  
「バグチェック」を参照してください。

<span id="type"></span><span id="TYPE"></span>**各種**  
「シンボルの種類」を参照してください。

 

 





