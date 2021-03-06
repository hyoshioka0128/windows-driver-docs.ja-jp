---
title: タイム トラベル デバッグ - トレースの記録
description: 時間を記録する方法を説明するトレースを移動します。
ms.date: 09/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 720e14b0493deab84b02f55d646e1f91511b687b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357101"
---
![クロックが表示された短い時間旅行ロゴ](images/ttd-time-travel-debugging-logo.png)

#  <a name="time-travel-debugging---record-a-trace"></a>タイム トラベル デバッグ - トレースの記録 

このセクションでは、タイム トラベルのデバッグ (TTD) トレースに記録する方法について説明します。 WinDbg のプレビューでトレースを記録する 2 つの方法はあります*起動実行可能ファイル (詳細)* と*プロセスにアタッチする*します。 


## <a name="launch-executable-advanced"></a>(詳細) を実行可能ファイルを起動します。

実行可能ファイルの起動を TTD トレースの記録は、次の手順に従います。

1. WinDbg のプレビューで次のように選択します。**ファイル** > **デバッグを開始** > **起動の実行可能ファイル (詳細)** します。

2. ユーザー モードの実行可能ファイルの記録、または選択するパスを入力**参照**実行可能ファイルに移動します。 WinDbg のプレビューで、実行可能ファイルの起動 メニューの使用については、次を参照してください。 [WinDbg Preview - ユーザー モードのセッションを開始](windbg-user-mode-preview.md)します。

    ![実行可能ファイル (高度な) 画面を起動する チェック ボックスを記録の開始を示す WinDbg プレビューのスクリーン ショット](images/ttd-start-recording.png)


3. チェック、**タイム トラベルのデバッグとプロセスを記録**実行可能ファイルを起動するときにトレースを記録するボックスです。 

4. をクリックして**OK**を実行可能ファイルを起動し、記録を開始します。 

5. トレースが記録されていることを示す記録ダイアログ ボックスが表示されます。

    ![オプションを取り消すとポップアップが表示された停止やデバッグにも記録 TTD](images/ttd-recording-pop-up.png)

6. 参照してください[を記録する方法](#HOWTORECORD)について記録します。


## <a name="attach-to-a-process"></a>プロセスにアタッチします。

プロセスにアタッチするを TTD トレースの記録は、次の手順に従います。

1. WinDbg のプレビューで次のように選択します。**ファイル** > **デバッグを開始** > **プロセスにアタッチ**します。

2. トレースするユーザー モード プロセスを選択します。 操作に関する情報の*プロセスにアタッチする*WinDbg のプレビューでのメニューを参照してください[WinDbg Preview - ユーザー モードのセッションを開始](windbg-user-mode-preview.md)します。

    ![チェック ボックスをオンの記録の開始を示す WinDbg プレビューのスクリーン ショット](images/ttd-start-recording-attach-to-process.png)


3. チェック、**タイム トラベル デバッグ レコード プロセス**ボックス実行可能ファイルを起動するときにトレースを作成します。 

4. クリックして**アタッチ**記録を開始します。 

5. トレースが記録されていることを示す記録ダイアログ ボックスが表示されます。

    ![オプションを取り消すとポップアップが表示された停止やデバッグにも記録 TTD](images/ttd-recording-pop-up-attach.png)

6. 参照してください[を記録する方法](#HOWTORECORD)について記録します。

## <a name="span-idhowtorecordspanspan-idhowtorecordspanhow-to-record"></a><span id="HOWTORECORD"></span><span id="howtorecord"></span>記録する方法

1. これは、デバッグする問題が発生する必要があるため、プロセスを記録中です。 問題のあるファイルを開くかによって発生する関心のあるイベントが発生するためにアプリの特定のボタンをクリックできます。 

2. 記録のダイアログ ボックスが表示されているときに次のことができます。

    - **停止し、デバッグ**-これを選択する記録を停止は、トレース ファイルを作成およびデバッグを開始するために、トレース ファイルを開きます。 
    - **キャンセル**-これを選択する、記録を停止し、トレース ファイルを作成します。 後でトレース ファイルを開くことができます。 
   
3. 記録が完了すると、アプリを閉じるかヒット**停止し、デバッグ**します。

   > [!NOTE]
   > 両方*停止し、デバッグ*と*キャンセル*は関連付けられているプロセスを終了します。 
   >   

4. 記録されるアプリケーションが終了すると、トレース ファイルが閉じられたとに書き出さディスクになります。 これは、場合しますも、プログラムがクラッシュした場合。

5. トレース ファイルが開かれたときに、デバッガーは、トレース ファイルを自動的にインデックスします。 インデックス作成により、メモリ値の外観の ups をより正確かつ高速化します。 このインデックス作成プロセスでは、大きなトレース ファイルがかかります。

    ```dbgcmd
    ...
    00007ffc`61f789d4 c3              ret
    0:000> !index
    Indexed 1/1 keyframes
    Successfully created the index in 96ms.
    ```
   > [!NOTE]
   > キーフレームは、インデックス作成のために使用されるトレース内の場所です。 キーフレームが自動的に生成されます。 大規模なトレースは、複数のキーフレームが含まれます。 トレースのインデックスが、キーフレームの数が表示されます。 
   >   
 
6. この時点では、トレース ファイルの先頭にし、前方に移動する準備ができて、時間の旧バージョンとは。

    > [!TIP]
    > ブレークポイントの使用は、関心のあるいくつかのイベントでコードが実行を一時停止する一般的なアプローチです。  TTD に一意でブレークポイントを設定して、トレースが記録された後にそのブレークポイントがヒットするまでの時点に戻りできます。 、ブレークポイントを設定する最適な場所を特定、問題が発生した後、プロセスの状態を検証する機能は、追加のデバッグ ワークフローを使用します。 ブレークポイントを使用して、過去の例は、次を参照してください。[タイム トラベルのデバッグ - サンプル アプリのチュートリアル](time-travel-debugging-walkthrough.md)します。

## <a name="next-steps"></a>次の手順

したので、記録された、TTD トレースを再生することができます、トレースのバックアップまたは共同作業者で共有することなど、トレース ファイルを使用します。 詳細については、これらのトピックを参照してください。

[タイム トラベル デバッグ - トレースの再生](time-travel-debugging-replay.md)

[タイム トラベル デバッグ - トレース ファイルの使用](time-travel-debugging-trace-file-information.md)

[タイム トラベル デバッグ - トラブルシューティング](time-travel-debugging-troubleshooting.md)

[旅行のデバッグ時間 - サンプル アプリのチュートリアル](time-travel-debugging-walkthrough.md)



## <a name="see-also"></a>関連項目

[旅行時間 - デバッグの概要](time-travel-debugging-overview.md)

---






