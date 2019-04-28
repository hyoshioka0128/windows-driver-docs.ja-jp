---
title: C (Windows デバッガーの用語集)
description: 用語集ページ - C
Robots: noindex, nofollow
ms.assetid: 295b05a3-e27f-4761-a562-7e87e25bfd3b
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67cafefd6e476c1274871599301a7769e495c07a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373958"
---
# <a name="c"></a>C


<span id="c___expression"></span><span id="C___EXPRESSION"></span>**C++ の式**  
C++ の式エバリュエーターによって評価される式。

<span id="c_call_stack"></span><span id="C_CALL_STACK"></span>**C の呼び出し履歴**  
参照呼び出し履歴。

<span id="call_stack"></span><span id="CALL_STACK"></span>**呼び出し履歴**  
スレッドによって行われる関数呼び出しを表すを格納している各スレッドのスタック フレームのセット。 関数呼び出しには、新しいスタック フレームが行われるたびは、スタックの一番上にプッシュされます。 その関数から制御が戻るときに、スタック フレームはスタックからポップします。

または単とに呼ばします。

<span id="callback_object"></span><span id="CALLBACK_OBJECT"></span>**コールバック オブジェクト**  
コールバック関数を入力し、コールバックの出力イベントのコールバック関数を参照してください。

<span id="checked_build"></span><span id="CHECKED_BUILD"></span>**チェック ビルド**  
各 NT ベースのオペレーティング システムの 2 つの異なるビルドが存在します。

-   (または) の Windows オペレーティング システムのエンドユーザーのバージョン。 詳細については、無料のビルドを参照してください。
-   Windows の役割をテストおよびデバッグに、オペレーティング システムとカーネル モード ドライバーの開発に役立つとしての (または)。 チェックのビルドには、追加エラー チェック、引数の検証およびデバッグ ビルドを無料でご利用いただけません情報が含まれています。 、システム ソフトウェアの問題の原因をトレースしやすきます。 チェックされているシステムかドライバーを分離し、予期しない動作が発生する、メモリ リークが発生または不適切なデバイスの構成で発生することができるドライバーの問題を追跡に役立ちます。

チェックのビルドには、追加の保護が用意されていますが、無料ビルドよりも多くのメモリとディスク領域が消費されます。 パラメーターのチェックと、診断メッセージの出力のための追加のコード パスが実行され、カーネル関数の一部の代替実装を使用するため、システムとドライバーのパフォーマンスが遅くなりますが。

Windows のチェック ビルドは、チェック ビルド環境の Windows Driver Kit (WDK) のいずれかで構築されたドライバーと混同しないでください。

<span id="child_symbol"></span><span id="CHILD_SYMBOL"></span>**子のシンボル**  
別のシンボルに含まれているシンボルです。 たとえば、構造体のメンバーのシンボルは、その構造体シンボルの子です。

<span id="client"></span><span id="CLIENT"></span>**クライアント**  
クライアント オブジェクトを参照してください。

<span id="client_object"></span><span id="CLIENT_OBJECT"></span>**クライアント オブジェクト**  
クライアント オブジェクトは、デバッガー エンジンとの対話に使用されます。 クライアントごとの状態を保持し、デバッガー エンジン API で最上位レベルのインターフェイスの実装を提供します。

<span id="client_thread"></span><span id="CLIENT_THREAD"></span>**クライアント スレッド**  
クライアント オブジェクトが作成されたスレッド。 一般に、クライアントのメソッドは、このスレッドからのみ呼び出すことがあります。 デバッガー エンジンでは、このスレッドを使用して、すべての呼び出しをクライアントに登録するコールバック オブジェクトを作成します。

<span id="code_breakpoint"></span><span id="CODE_BREAKPOINT"></span>**コードのブレークポイント**  
ソフトウェアのブレークポイントを参照してください。

<span id="crash_dump_file"></span><span id="CRASH_DUMP_FILE"></span>**クラッシュ ダンプ ファイル**  
特定のメモリ領域と、アプリケーションまたはオペレーティング システムに関連するその他のデータのスナップショットを含むファイル。 クラッシュ ダンプ ファイルを格納し、後で、アプリケーションまたはオペレーティング システムをデバッグするために使用します。

ユーザー モード クラッシュ ダンプ ファイルは、アプリケーションがクラッシュして、Windows 自体がクラッシュした場合、Windows の特殊なルーチンでカーネル モードのクラッシュ ダンプ ファイルを作成できるときに、Windows で作成できます。 クラッシュ ダンプ ファイルのさまざまな種類があります。

<span id="current_process"></span><span id="CURRENT_PROCESS"></span>**現在のプロセス**  
デバッガー エンジンが現在制御しているプロセス。 イベントの発生時に、現在のプロセスがイベント処理に設定されます。

<span id="current_target"></span><span id="CURRENT_TARGET"></span>**現在のターゲット**  
デバッガー エンジンが現在制御しているターゲット。 イベントの発生時に、現在のターゲットがイベントのターゲットに設定されます。

<span id="current_thread"></span><span id="CURRENT_THREAD"></span>**現在のスレッド**  
デバッガー エンジンが現在制御しているスレッド。 イベントの発生時に、現在のスレッドがイベント スレッドに設定されます。

 

 





