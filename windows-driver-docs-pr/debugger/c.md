---
title: C (Windows デバッガー用語集)
description: 用語集のページ-C
ms.asseti: 295b05a3-e27f-4761-a562-7e87e25bfd3b
ms.date: 12/17/2019
ms.localizationpriority: medium
ms.openlocfilehash: 59a373ee3195d2717d7b6577894a99104355693e
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209454"
---
# <a name="c"></a>C


<span id="c___expression"></span><span id="C___EXPRESSION"></span>**C++条件**  
C++式エバリュエーターによって評価できる式。

<span id="c_call_stack"></span><span id="C_CALL_STACK"></span>**C 呼び出し履歴**  
「呼び出し履歴」を参照してください。

<span id="call_stack"></span><span id="CALL_STACK"></span>**呼び出し履歴**  
スレッドによって行われた関数呼び出しを表すを格納している各スレッドのスタックフレームのセット。 関数呼び出しが行われるたびに、新しいスタックフレームがスタックの一番上にプッシュされます。 この関数が戻ると、スタックフレームがスタックからポップされます。

または単にと呼ばれることもあります。

<span id="callback_object"></span><span id="CALLBACK_OBJECT"></span>**コールバックオブジェクト**  
「イベントコールバック」、「入力コールバック」、および「出力コールバック」を参照してください。

<span id="checked_build"></span><span id="CHECKED_BUILD"></span>**チェックされたビルド**  

チェックを行ったビルドは、Windows では提供されなくなりました。 ドライバーの検証ツールや GFlags などのツールを使用してドライバーコードを確認します。

チェックされたビルドには、無料のビルドでは利用できない追加のエラーチェック、引数の検証、およびデバッグ情報が含まれていました。

チェックを行うビルドは追加の保護を提供しますが、無料のビルドよりも多くのメモリとディスク領域を消費します。 診断メッセージのパラメーターチェックと出力によって追加のコードパスが実行され、カーネル関数の代替実装が使用されるため、システムとドライバーのパフォーマンスが低下します。

Windows のチェックされたビルドは、Windows Driver Kit (WDK) のチェックされたビルド環境のいずれかでビルドされたドライバーと混同しないようにしてください。

<span id="child_symbol"></span><span id="CHILD_SYMBOL"></span>**子シンボル**  
別の記号に含まれる記号。 たとえば、構造体のメンバーのシンボルは、その構造体のシンボルの子になります。

<span id="client"></span><span id="CLIENT"></span>**client**  
「クライアントオブジェクト」を参照してください。

<span id="client_object"></span><span id="CLIENT_OBJECT"></span>**クライアントオブジェクト**  
クライアントオブジェクトは、デバッガーエンジンとの対話に使用されます。 これは、クライアントごとの状態を保持し、デバッガーエンジン API の最上位レベルのインターフェイスの実装を提供します。

<span id="client_thread"></span><span id="CLIENT_THREAD"></span>**クライアントスレッド**  
クライアントオブジェクトが作成されたスレッド。 一般に、クライアントのメソッドは、このスレッドからのみ呼び出すことができます。 デバッガーエンジンは、このスレッドを使用して、クライアントに登録されているコールバックオブジェクトへのすべての呼び出しを行います。

<span id="code_breakpoint"></span><span id="CODE_BREAKPOINT"></span>**コードのブレークポイント**  
「ソフトウェアブレークポイント」を参照してください。

<span id="crash_dump_file"></span><span id="CRASH_DUMP_FILE"></span>**クラッシュダンプファイル**  
特定のメモリ領域のスナップショットと、アプリケーションまたはオペレーティングシステムに関連するその他のデータを含むファイル。 クラッシュダンプファイルを保存し、後でアプリケーションまたはオペレーティングシステムをデバッグするために使用できます。

アプリケーションがクラッシュしたときに Windows によってユーザーモードのクラッシュダンプファイルを作成できます。また、Windows 自体がクラッシュしたときに、カーネルモードのクラッシュダンプファイルを特別な Windows ルーチンで作成できます。 クラッシュダンプファイルには、いくつかの種類があります。

<span id="current_process"></span><span id="CURRENT_PROCESS"></span>**現在のプロセス**  
デバッガーエンジンが現在制御しているプロセス。 イベントが発生すると、現在のプロセスがイベントプロセスに設定されます。

<span id="current_target"></span><span id="CURRENT_TARGET"></span>**現在のターゲット**  
デバッガーエンジンが現在制御しているターゲット。 イベントが発生すると、現在のターゲットがイベントターゲットに設定されます。

<span id="current_thread"></span><span id="CURRENT_THREAD"></span>**現在のスレッド**  
デバッガーエンジンが現在制御しているスレッド。 イベントが発生すると、現在のスレッドがイベントスレッドに設定されます。

 

 





