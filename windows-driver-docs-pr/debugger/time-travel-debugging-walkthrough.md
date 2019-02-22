---
title: 旅行のデバッグ時間 - サンプル アプリのチュートリアル
description: このセクションには、小規模な C++ アプリの説明が含まれています。
ms.date: 09/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6e6156cc4ca85c58dfc909d3494d1df61a934a22
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552015"
---
![クロックが表示された短い時間旅行ロゴ](images/ttd-time-travel-debugging-logo.png)

#  <a name="time-travel-debugging---sample-app-walkthrough"></a>旅行のデバッグ時間 - サンプル アプリのチュートリアル

このラボでは、タイム トラベル デバッグ (TTD)、コードの不具合の小さなサンプル プログラムを使用してについて説明します。 デバッグを特定し、ルートを TTD が使用される、問題が発生します。 この小さなプログラムで問題が見つけやすいより複雑なコードでの一般的な手順を使用できます。 この一般的な手順は、ようにまとめることができます。

1. 失敗したプログラムの時間旅行トレースをキャプチャします。
2. 使用して、 [dx (表示デバッガー オブジェクト モデルの式)](dx--display-visualizer-variables-.md)記録に格納されている例外イベントを検索するコマンド。 
3. 使用して、 [! tt (タイム トラベル)](time-travel-debugging-extension-tt.md)トレースの例外イベントの位置に移動するコマンド。
4. 問題のエラーが発生したコード内を後方に向かってまでトレース シングル ステップでは、その時点からには、スコープに渡されます。
5. エラーが発生したコードのスコープ内では、ローカル値を確認し、正しくない値を含む可能性のある変数の仮説を開発します。
6. 正しくない値で変数のメモリ アドレスを決定します。
7. メモリ アクセス (ba) ブレークポイントを設定、ba を使用して、問題のある変数のアドレスに[(アクセスで中断)](ba--break-on-access-.md)コマンド。
8. 問題のある変数のメモリ アクセスの最後のポイントにバックアップを実行する g: を使用します。
9. かどうか、その場所またはいくつかの手順には、コードの不具合のポイントを参照してください。 そうである場合、完了です。
元がその他のいくつかの変数に不適切な値で場合は、2 番目の変数のブレークポイントのアクセスに別の中断を設定します。 
10. 上で実行するバックアップ最後のメモリ アクセス ポイント、2 つ目の問題のある変数 g: を使用します。 その場所または前に、いくつかの手順にはコードの欠陥が含まれているかどうかを参照してください。 そうである場合、完了です。
11. このプロセスのウォークにエラーが発生した不適切な値を設定するコードがあるまでを繰り返します。
 
この手順で説明する一般的な手法は、コードの問題の広範なセットに適用、独自のアプローチが必要になる固有のコードの問題があります。 チュートリアルで、手法では、展開、デバッグ ツール セットを提供する必要があり、TTD トレースでできることの一部を示しています。


## <a name="span-idlabobjectivesspanspan-idlabobjectivesspanspan-idlabobjectivesspanlab-objectives"></a><span id="Lab_objectives"></span><span id="lab_objectives"></span><span id="LAB_OBJECTIVES"></span>ラボの目的

このラボを完了すると、次のコード内での問題を検索するタイム トラベルのトレースでの一般的な手順を使用することができます。 


## <a name="span-idlabsetupspanspan-idlabsetupspanspan-idlabsetupspanlab-setup"></a><span id="Lab_setup"></span><span id="lab_setup"></span><span id="LAB_SETUP"></span>ラボのセットアップ

次のハードウェア ラボを完成させることができる必要があります。

-   ラップトップまたはデスクトップ コンピューター (ホスト) Windows 10 を実行しています。 

次のソフトウェアのラボを完成させることができる必要があります。

-   WinDbg のプレビュー。 WinDbg のプレビューをインストールする方法の詳細については、次を参照してください[WinDbg Preview のインストール。](https://docs.microsoft.com/windows-hardware/drivers/debugger/windbg-install-preview)
-   Visual Studio でサンプル C++ コードをビルドします。 

ラボでは、次の 3 つのセクションにします。

-   [セクション 1:サンプル コードをビルドします。](#build)
-   [セクション 2:"DisplayGreeting"サンプルのトレースを記録します。](#record)
-   [セクション 3:コードの問題を識別するために記録するトレース ファイルを分析します。](#analyze)


## <a name="span-idbuildspansection-1-build-the-sample-code"></a><span id="build"></span>セクション 1:サンプル コードをビルドします。

*セクション 1 では、Visual Studio を使用してサンプル コードを作成します。*

**Visual Studio でサンプル アプリを作成します。**

1.  Microsoft Visual studio で次のようにクリックします**ファイル** &gt; **新規** &gt; **プロジェクト/ソリューション。** ビジュアルの  **C++** テンプレート。 
    
    Win32 コンソール アプリケーションを選択します。

    プロジェクト名を指定*DisplayGreeting*  をクリック**OK**します。

2. Security Development Lifecycle (SDL) チェックをオフにします。

    ![win32 アプリケーション ウィザード アプリケーションの設定](images/ttd-time-travel-walkthrough-application-wizard-application-settings.png) 

3. をクリックして**完了**します。

3. Visual Studio で DisplayGreeting.cpp ペインには、次のテキストを貼り付けます。

    ```cpp
    // DisplayGreeting.cpp : Defines the entry point for the console application.
    //

    #include "stdafx.h"
    #include <array>
    #include <stdio.h>
    #include <string.h>

    void GetCppConGreeting(wchar_t* buffer, size_t size)
    {
       wchar_t const* const message = L"HELLO FROM THE WINDBG TEAM. GOOD LUCK IN ALL OF YOUR TIME TRAVEL DEBUGGING!";
 
       wcscpy_s(buffer, size, message);
    }

    int main()
    {
        std::array <wchar_t, 50> greeting{};
        GetCppConGreeting(greeting.data(), sizeof(greeting));

        wprintf(L"%ls\n", greeting.data());

        return 0;
    }
    ```

4.  Visual Studio で、次のようにクリックします。**プロジェクト** &gt; **DisplayGreeting プロパティ**します。 をクリックして**C/C++** と**コード生成**します。

    次のプロパティを設定します。

    | 設定              |  Value                        |
    |----------------------|-------------------------------|
    | セキュリティ チェック       | セキュリティ チェックを無効にする (/GS-) |
    | 基本ランタイム チェック |  Default                      |

 
   > [!NOTE]
   > これらの設定は推奨されませんが、コーディングの時間を短縮する、または特定のテスト環境を容易にするために、これらの設定を使用してをアドバイスだれかがシナリオを考えてみましょうことは。
   >  

5.  Visual Studio で、次のようにクリックします。**ビルド** &gt; **ソリューションのビルド**します。

    すべてうまくいけば、windows のビルドは、ビルドが成功したことを示すメッセージを表示する必要があります。

6.  **ビルドされたサンプル アプリ ファイルを見つける**

    ソリューション エクスプ ローラーで右クリック、 *DisplayGreeting*順に選択して**ファイル エクスプ ローラーでフォルダーを開く**します。
    
    サンプルのコンパイル済み実行可能ファイルとシンボル pdb ファイルを含むデバッグ フォルダーに移動します。 移動するなど、 *C:\Projects\DisplayGreeting\Debug*プロジェクトが含まれているフォルダーがある場合、します。 

7. **コードの不具合でサンプル アプリを実行します。**

    サンプル アプリを実行する、exe ファイルをダブルクリックします。

    ![エラー状態のアプリ ダイアログ ボックス](images/ttd-time-travel-walkthrough-faulting-app-dialog-box.png) 

    このダイアログ ボックスが表示されたら、**プログラムの終了**

    ![エラー状態のアプリ ダイアログ ボックス](images/ttd-time-travel-walkthrough-program-not-working-dialog-box.png) 
    
    このチュートリアルの次のセクションでは、この例外が発生している理由を判断できるかどうかに表示するサンプル アプリの実行を記録します。 


## <a name="span-idrecordspansection-2-record-a-trace-of-the-displaygreeting-sample"></a><span id="record"></span>セクション 2:"DisplayGreeting"サンプルのトレースを記録します。

*セクション 2 では、不適切な動作のサンプル"DisplayGreeting"アプリのトレースを記録します*

サンプル アプリの起動を TTD トレースの記録は、次の手順に従います。 TTD トレースの記録の概要については、次を参照してください[タイム トラベルのデバッグ - トレース レコード。](time-travel-debugging-record.md)

1. 時間を記録することができるように管理者として実行 WinDbg プレビューでは、トレースを移動します。

2. WinDbg のプレビューで次のように選択します。**ファイル** > **デバッグを開始** > **起動の実行可能ファイル (詳細)** します。

3. ユーザー モードの実行可能ファイルの記録、または選択するパスを入力**参照**実行可能ファイルに移動します。 WinDbg のプレビューで実行可能ファイル メニューの起動処理の詳細については、次を参照してください。 [WinDbg Preview - ユーザー モードのセッションを開始](windbg-user-mode-preview.md)します。

    ![実行可能ファイル (高度な) 画面を起動する チェック ボックスを記録の開始を示す WinDbg プレビューのスクリーン ショット](images/ttd-time-travel-walkthrough-recording-app.png)

4. チェック、**タイム トラベルのデバッグとプロセスを記録**実行可能ファイルを起動するときにトレースを記録するボックスです。 

5. をクリックして**OK**を実行可能ファイルを起動し、記録を開始します。 

6. トレースが記録されていることを示す記録ダイアログ ボックスが表示されます。 その後間もなく、アプリケーションがクラッシュします。

7. をクリックして**再試行**、コードが実行してみてください。

8. プログラムがクラッシュし、トレース ファイルを閉じていて、out に書き込まれるディスクとなります。 

    ![Screen shot of WinDbg Preview showing output with 1/1 keyframes indexed](images/ttd-time-travel-walkthrough-windbg-indexed-frames.png)

9. デバッガーは自動的にトレース ファイルを開くし、インデックスが作成されます。 インデックス作成は、トレース ファイルの効率的なデバッグを有効にするプロセスです。 このインデックス作成プロセスでは、大きなトレース ファイルがかかります。

    ```dbgcmd
    0:000> !index
    Indexed 1/1 keyframes
    Successfully created the index in 95ms.
    ```
   
   > [!NOTE]
   > キーフレームは、インデックス作成のために使用されるトレース内の場所です。 キーフレームが自動的に生成されます。 大規模なトレースは、複数のキーフレームが含まれます。 
   >   
 
10. この時点では、トレース ファイルの先頭にし、前方に移動する準備ができて、時間の旧バージョンとは。

    したので、記録された、TTD トレースを再生することができます、トレースのバックアップまたは共同作業者で共有することなど、トレース ファイルを使用します。 トレース ファイルの使用の詳細については、次を参照してください[タイム トラベルのデバッグ - トレース ファイルの使用。](time-travel-debugging-trace-file-information.md)

このラボの次のセクションでは、コードを使って問題を検索するトレース ファイルを分析します。


## <a name="span-idanalyzespansection-3-analyze-the-trace-file-recording-to-identify-the-code-issue"></a><span id="analyze"></span>セクション 3:コードの問題を識別するために記録するトレース ファイルを分析します。

*セクション 3 では、コードの問題を識別するために記録するトレース ファイルを分析します。*

**WinDbg の環境を構成します。**

1.  シンボル パスに、ローカル シンボルの場所を追加し、次のコマンドを入力して、シンボルを再読み込みします。

    ```dbgcmd
    .sympath+ C:\Projects\DisplayGreeting\Debug
    .reload 
    ```

2.  ソース パスをローカルのコードの場所を追加するには、次のコマンドを入力します。

    ```dbgcmd
    .srcpath C:\Projects\DisplayGreeting\DisplayGreeting
    ```

3. リボンの WinDbg のプレビューのスタックやローカル変数の状態を表示できるようにするには、次のように選択します**ビュー**と**ローカル**と**ビュー**と**スタック**. 同時に、ソース コード、およびコマンド ウィンドウを表示できるように windows を整理します。

4.  WinDbg プレビュー リボンでは、次のように選択します。**ソース**と**ソース ファイルを開く**します。 DisplayGreeting.cpp ファイルを開きます。

**例外を調べる**

1. トレース ファイルが読み込まれたときに例外が発生した情報が表示されます。 

    ```dbgcmd
    2fa8.1fdc): Break instruction exception - code 80000003 (first/second chance not available)
    Time Travel Position: 15:0
    eax=68ef8100 ebx=00000000 ecx=77a266ac edx=69614afc esi=6961137c edi=004da000
    eip=77a266ac esp=0023f9b4 ebp=0023fc04 iopl=0         nv up ei pl nz na pe nc
    cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000206
    ntdll!LdrpInitializeProcess+0x1d1c:
    77a266ac 83bdbcfeffff00  cmp     dword ptr [ebp-144h],0 ss:002b:0023fac0=00000000
    ```
2. すべてのイベントは記録に一覧表示するのにには、dx コマンドを使用します。 例外イベントはイベントに表示されます。

    ```dbgcmd
    0:000> dx -r1 @$curprocess.TTD.Events
    ...
    [0x2c]           : Module Loaded at position: 9967:0
    [0x2d]           : Exception at 9BDC:0
    [0x2e]           : Thread terminated at 9C43:0
    ...
    
    ```

   > [!NOTE]
   > このチュートリアルでは、3 つのピリオドは余分な出力が削除されたことを示すために使用されます。 
   >


3. その TTD イベントに関する情報を表示する例外イベントをクリックします。 

    ```dbgcmd
    0:000> dx -r1 @$curprocess.TTD.Events[17]
    @$curprocess.TTD.Events[17]                 : Exception at 68:0
        Type             : Exception
        Position         : 68:0 [Time Travel]
        Exception        : Exception of type Hardware at PC: 0X540020
    ```


4. 例外データで例外フィールドさらにドリル ダウンをクリックします。 

    ```dbgcmd
    0:000> dx -r1 @$curprocess.TTD.Events[17].Exception
    @$curprocess.TTD.Events[17].Exception                 : Exception of type Hardware at PC: 0X540020
        Position         : 68:0 [Time Travel]
        Type             : Hardware
        ProgramCounter   : 0x540020
        Code             : 0xc0000005
        Flags            : 0x0
        RecordAddress    : 0x0
    ```

   例外データでは、CPU によってスローされたハードウェアの障害であることを示します。 アクセス違反であることを示します 0xc0000005 の例外コードも提供します。 これは、通常へのアクセスはありませんメモリへの書き込みを試行していたことを示します。

5. 例外イベントがトレースには、その位置に移動] で [タイム トラベル] リンクをクリックします。

    ```dbgcmd
    0:000> dx @$curprocess.TTD.Events[17].Exception.Position.SeekTo()
    Setting position: 68:0

    @$curprocess.TTD.Events[17].Exception.Position.SeekTo()
    (16c8.1f28): Break instruction exception - code 80000003 (first/second chance not available)
    Time Travel Position: 68:0
    eax=00000000 ebx=00cf8000 ecx=99da9203 edx=69cf1a6c esi=00191046 edi=00191046
    eip=00540020 esp=00effe4c ebp=00520055 iopl=0         nv up ei pl zr na pe nc
    cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000246
    00540020 ??              
    ```
    
    この出力で注目すべき 2 つの非常に異なるアドレスに、スタック、および基本ポインターが指していることはできます。

    ```dbgcmd
    esp=00effe4c ebp=00520055
    ```

    可能性をスタックの破損の可能性がある関数が返され、スタックが壊れています。 これを検証するには、CPU の状態が破損する前に移動して、スタックの破損が発生したときを判断できるかどうかに必要があります。


**ローカル変数を確認し、コードのブレークポイントを設定**

トレースで失敗した時点でするが一般的 fews 手順の最後のエラー処理コードで本当の原因の後にします。 時刻では、旅行を検索するには、一度に命令戻ることができますは、true の根本原因を調査します。


1. **ホーム**リボンの使用、**バックアップ手順に**ステップにコマンドが 3 つの命令をバックアップします。 この場合、windows のスタックとメモリを確認し続けてください。

    タイム トラベル位置がコマンド ウィンドウに表示され、レジスタにステップ実行するとは、3 つの命令をバックアップします。

    ```dbgcmd
    0:000> t-
    Time Travel Position: 67:40
    eax=00000000 ebx=00cf8000 ecx=99da9203 edx=69cf1a6c esi=00191046 edi=00191046
    eip=00540020 esp=00effe4c ebp=00520055 iopl=0         nv up ei pl zr na pe nc
    cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000246
    00540020 ??              ???

    0:000> t-
    Time Travel Position: 67:3F
    eax=00000000 ebx=00cf8000 ecx=99da9203 edx=69cf1a6c esi=00191046 edi=00191046
    eip=0019193d esp=00effe48 ebp=00520055 iopl=0         nv up ei pl zr na pe nc
    cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000246
    DisplayGreeting!main+0x4d:
    0019193d c3    

    0:000> t-
    Time Travel Position: 67:39
    eax=0000004c ebx=00cf8000 ecx=99da9203 edx=69cf1a6c esi=00191046 edi=00191046
    eip=00191935 esp=00effd94 ebp=00effe44 iopl=0         nv up ei pl nz ac po nc
    cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000212
    DisplayGreeting!main+0x45:
    ```

   > [!NOTE]
   > このチュートリアルでは、コマンドの出力は、UI のメニュー オプションではなくコマンド ライン コマンドを使用するコマンドラインの使用状況 基本設定を持つユーザーを許可するのに使用できるコマンドを示します。
   > 

2. この時点で、トレースで、スタックと基本ポインターがあるがあること、コードで、ポイントに近づける破損が発生したことが表示されるように、複数の意味のある値。

    ```dbgcmd
    esp=00effd94 ebp=00effe44
    ```

    関心のあるは、[ローカル] ウィンドウには、対象アプリからの値が含まれています。 ソース コード ウィンドウがトレースには、この時点で実行する準備が整っているコード行を強調表示です。

    ![スクリーン ショットの WinDbg プレビュー ローカル メモリ ASCII 出力およびソース コード ウィンドウのウィンドウの表示](images/ttd-time-travel-walkthrough-locals-window.png)

3. 近くの基本ポインターのメモリ アドレスの内容を表示する [メモリ] ウィンドウを開くことができますをさらに調査、 *0x00effe44*します。

4. メモリのリボンで、関連付けられている ASCII 文字を表示する次のように選択します。**テキスト**し**ASCII**します。

    ![winbbg プレビューが表示されたメモリ ascii 出力およびソース コード ウィンドウのスクリーン ショット](images/ttd-time-travel-walkthrough-memory-ascii.png)

5. 基本に命令を指すポインターではなく、メッセージ テキストをポイントします。 ここでない内容があるようにをここに、スタックが破損しているポイントの近くにあります。 さらに調査するためにブレークポイントを設定します。 


> [!NOTE]
> この非常に小さいサンプルでは非常に簡単で、コードを見るだけなりますが、問題を特定するために必要な時間を減らすためここで説明した手法を使用できます何百もの行のコードと数十個のサブルーチンがある場合。
>


**TTD とブレークポイント**

ブレークポイントの使用は、関心のあるいくつかのイベントでコードが実行を一時停止する一般的なアプローチです。  TTD を使用すると、ブレークポイントを設定して、戻す旅行、トレースが記録された後にブレークポイントをヒットするまでの時間にできます。 、ブレークポイントを設定する最適な場所を特定、問題が発生した後、プロセスの状態を検証する機能は、TTD に固有の追加のデバッグ ワークフローを使用します。 

**メモリ アクセスのブレークポイント**

メモリの場所にアクセスするときに発生するブレークポイントを設定することができます。 使用して、 **ba** (アクセスの切断) コマンドを次の構文を使用します。

```dbgcmd
ba <access> <size> <address> {options}
```

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">構成方法</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>E</p></td>
<td align="left"><p>(CPU では、アドレスから命令をフェッチ) したときに実行します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>r</p></td>
<td align="left"><p>(CPU の読み取りまたは書き込みをアドレスに) 場合、読み取り/書き込み</p></td>
</tr>
<tr class="odd">
<td align="left"><p>W</p></td>
<td align="left"><p>書き込み (する場合、CPU は、アドレスに書き込む)</p></td>
</tr>
</tbody>
</table>

 
特定の時点、4 つのデータ ブレークポイントを設定することができますのみで、データを正しく配置すること、または、ブレークポイントをトリガーしないかどうかを確認するかどうかは (単語が 2 で割り切れるアドレスで終了する必要があります、dword が 4 で割り切れる必要があります、および (クワドワード)。 0 または 8 で)。


**ベース ポインターのメモリ アクセスのブレークポイントで中断を設定します。**    

1.  この時点で、トレースでたい基本ポインター - ebp 00effe44 は、この例ではこれを書き込みメモリ アクセスにブレークポイントを設定します。 そのために、 **ba**コマンドを監視するアドレスを使用します。 W4 を指定しますので、4 バイトの書き込みを監視します。 

    ```dbgcmd
    0:000> ba w4 00effe44
    ```

2. 選択**ビュー**し**ブレークポイント**を意図したとおりに設定されていることを確認します。

    ![1 つのブレークポイントと WinDbg のプレビューが表示された [ブレークポイント] ウィンドウ](images/ttd-time-travel-walkthrough-view-breakpoints.png)


3.  ホーム メニューから選択**戻る**ブレークポイントがヒットするまでの時間に移動します。

    ```dbgcmd
    0:000> g-
    Breakpoint 0 hit
    Time Travel Position: 5B:92
    eax=0000000f ebx=003db000 ecx=00000000 edx=00cc1a6c esi=00d41046 edi=0053fde8
    eip=00d4174a esp=0053fcf8 ebp=0053fde8 iopl=0         nv up ei pl nz ac pe nc
    cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000216
    DisplayGreeting!DisplayGreeting+0x3a:
    00d4174a c745e000000000  mov     dword ptr [ebp-20h],0 ss:002b:0053fdc8=cccccccc
    ```

4. 選択**ビュー**し**ローカル**します。 [ローカル] ウィンドウで確認できます、*先*変数が、メッセージの一部のみ中に、*ソース*がすべてのテキストが含まれています。 この情報は、スタックが破損していることをサポートします。 

    ![[ローカル] ウィンドウのスクリーン ショットの WinDbg プレビュー](images/ttd-time-travel-walkthrough-locals-window.png)


5. この時点でどのようなコードがアクティブなプログラム スタックを確認できます。 **ビュー**リボン選択**スタック**します。 

    ![WinDbg プレビューのスクリーン ショットの履歴 ウィンドウ](images/ttd-time-travel-walkthrough-stack-window.png)


Wscpy_s() 関数は、このようなコードのバグを Microsoft が提供されることがよくありますがないため、スタックで詳しく説明します。 スタックことを示しています Greeting! メインあいさつ文を呼び出します。GetCppConGreeting します。 非常に小さなコード サンプルではこの時点で、コードを開くだけでしたおエラーをかなり簡単に見つかります。 大規模でより複雑なプログラムで使用できる手法を示すためは、さらに詳しく調査する新しいブレークポイントを設定します。 


**GetCppConGreeting 関数へのアクセスのブレークポイントで中断を設定します。**        

1. [ブレークポイント] ウィンドウを使用して、既存のブレークポイントを右クリックしを選択すると、既存のブレークポイントをクリアする**削除**します。

2. DisplayGreeting のアドレスを確認します。DetermineStringSize 関数を使用して、 **dx**コマンド。 

    ```dbgcmd
    0:000> dx &DisplayGreeting!GetCppConGreeting
    &DisplayGreeting!GetCppConGreeting                 : 0xb61720 [Type: void (__cdecl*)(wchar_t *,unsigned int)]
        [Type: void __cdecl(wchar_t *,unsigned int)]
    ```

3. 使用して、 **ba**メモリへのアクセスにブレークポイントを設定するコマンド。 関数は、実行用メモリから読み取りだけ、ためには、ブレークポイントを読み取る、-r を設定する必要があります。

    ```dbgcmd
    0:000> ba r4 b61720
    ```

4. [ブレークポイント] ウィンドウで、ハードウェアの読み取りのブレークポイントがアクティブであることを確認します。

    ![1 つのハードウェアと WinDbg のプレビューが表示された [ブレークポイント] ウィンドウでブレークポイントを読み取る](images/ttd-time-travel-walkthrough-hardware-write-breakpoint.png)


5. 案内文字列のサイズについて考えていますが、sizeof(greeting) の値を表示するウォッチ ウィンドウを設定します。 [表示] リボンから選択**ウォッチ**提供と*sizeof(greeting)* します。

    ![[ローカル]、ウォッチを示す WinDbg プレビュー ウィンドウ](images/ttd-time-travel-watch-locals.png)

6. [タイム トラベル] メニューを使用して、**開始への移動をタイム**トレースの開始に移行するコマンド。

    ```dbgcmd
    0:000> !tt 0
    Setting position to the beginning of the trace
    Setting position: 15:0
    (1e5c.710): Break instruction exception - code 80000003 (first/second chance not available)
    Time Travel Position: 15:0
    eax=68e28100 ebx=00000000 ecx=77a266ac edx=69e34afc esi=69e3137c edi=00fa2000
    eip=77a266ac esp=00ddf3b8 ebp=00ddf608 iopl=0         nv up ei pl nz na pe nc
    cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000206
    ntdll!LdrpInitializeProcess+0x1d1c:
    77a266ac 83bdbcfeffff00  cmp     dword ptr [ebp-144h],0 ss:002b:00ddf4c4=00000000
    ```

7.  [ホーム] メニューで、次のように選択します。**移動**ブレークポイントがヒットするまで、コードで前方に移動します。

    ```dbgcmd
    0:000> g
    Breakpoint 2 hit
    Time Travel Position: 4B:1AD
    eax=00ddf800 ebx=00fa2000 ecx=00ddf800 edx=00b61046 esi=00b61046 edi=00b61046
    eip=00b61721 esp=00ddf7a4 ebp=00ddf864 iopl=0         nv up ei pl nz na po nc
    cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000202
    DisplayGreeting!GetCppConGreeting+0x1:
    00b61721 8bec            mov     ebp,esp
    ```


8.  [ホーム] メニューで、次のように選択します。**ステップ バック**1 つの手順をバックアップします。

    ```dbgcmd
    0:000> g-u
    Time Travel Position: 4B:1AA
    eax=00ddf800 ebx=00fa2000 ecx=00ddf800 edx=00b61046 esi=00b61046 edi=00b61046
    eip=00b61917 esp=00ddf7ac ebp=00ddf864 iopl=0         nv up ei pl nz na po nc
    cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000202
    DisplayGreeting!main+0x27:
    00b61917 e8def7ffff      call    DisplayGreeting!ILT+245(?GetCppConGreetingYAXPA_WIZ) (00b610fa)
    ```


9. 根本原因を発見しましたように見えます。 *Greeting*宣言された配列は 50 文字で、GetCppConGreeting に渡している sizeof(greeting) は 0x64、100)。  

    ![WinDbg プレビューのあいさつ文ウォッチ [ローカル] ウィンドウに X64 でのコードの表示](images/ttd-time-travel-walkthrough-code-with-watch-locals.png)

    サイズに関する問題をさらに、見ていると、メッセージは 75 文字で、文字列の文字の終了など 76 もわかります。

    ```dbgcmd
    HELLO FROM THE WINDBG TEAM. GOOD LUCK IN ALL OF YOUR TIME TRAVEL DEBUGGING!
    ```


10. コードを修正する方法の 1 つは、文字配列のサイズを 100 に展開することです。

    ```cpp
    std::array <wchar_t, 100> greeting{};
    ```

    次のコード行で size(greeting) sizeof(greeting) に変更する必要もあります。

    ```cpp
     GetCppConGreeting(greeting.data(), size(greeting));
    ```

11. これらの修正プログラムを検証するには、コードを再コンパイルでしたおエラーなしで実行されることを確認します。


**ソース ウィンドウを使用してブレークポイントの設定**


1. この調査を実行する別の方法は、すべてのコード行をクリックしてブレークポイントを設定することです。 たとえば、ソース ウィンドウ std:array 定義の行の右側にあるをクリックするがあります、ブレークポイントが設定されます。

    ![Std:array に設定されたブレークポイントを示すソース ウィンドウのスクリーン ショット](images/ttd-time-travel-walkthrough-source-window-breakpoint.png)

2. [タイム トラベル] メニューを使用して、**開始への移動をタイム**トレースの開始に移行するコマンド。

    ```dbgcmd
    0:000> !tt 0
    Setting position to the beginning of the trace
    Setting position: 15:0
    (1e5c.710): Break instruction exception - code 80000003 (first/second chance not available)
    Time Travel Position: 15:0
    eax=68e28100 ebx=00000000 ecx=77a266ac edx=69e34afc esi=69e3137c edi=00fa2000
    eip=77a266ac esp=00ddf3b8 ebp=00ddf608 iopl=0         nv up ei pl nz na pe nc
    cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000206
    ntdll!LdrpInitializeProcess+0x1d1c:
    77a266ac 83bdbcfeffff00  cmp     dword ptr [ebp-144h],0 ss:002b:00ddf4c4=00000000
    ```

3. [ホーム] リボンをクリックします。**移動**ブレークポイントにヒットするまでバックアップを移動します。

    ```dbgcmd
    Breakpoint 0 hit
    Time Travel Position: 5B:AF
    eax=0000000f ebx=00c20000 ecx=00000000 edx=00000000 esi=013a1046 edi=00effa60
    eip=013a17c1 esp=00eff970 ebp=00effa60 iopl=0         nv up ei pl nz na po nc
    cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000202
    DisplayGreeting!DisplayGreeting+0x41:
    013a17c1 8bf4            mov     esi,esp
    ```


**アクセスのブレークポイントで中断を設定、 *greeting*変数**    

この調査の結果を実行する別の代替方法は、問題のある変数にブレークポイントを設定し、どのようなコードが変更することを確認することです。 たとえば、GetCppConGreeting メソッドであいさつの変数にブレークポイントを設定するには、この手順を使用します。

チュートリアルのこの部分では、前のセクションで、ブレークポイントが配置されているいることを前提としています。 

1. **ビュー**し**ローカル**します。 [ローカル] ウィンドウで*greeting*は、そのメモリ位置を決定することができるように、現在のコンテキストで使用できます。 

2.  使用して、 **dx**を確認するコマンド、 *greeting*配列。 

    ```dbgcmd
    0:000> dx &greeting
    &greeting                 : 0xddf800 [Type: std::array<wchar_t,50> *]
       [+0x000] _Elems           : "꽘棶檙瞝???" [Type: wchar_t [50]]
    ```

    このトレースに*greeting* ddf800 時のメモリ内にあります。 


2. [ブレークポイント] ウィンドウを使用して、既存のブレークポイントを右クリックしを選択すると、既存のすべてのブレークポイントをクリアする**削除**します。


3.  ブレークポイントを設定、 **ba**に対する書き込みアクセスを監視するメモリ アドレスを使用してコマンドします。 

    ```dbgcmd
    ba w4 ddf800
    ```

4. [タイム トラベル] メニューを使用して、**開始への移動をタイム**トレースの開始に移行するコマンド。

    ```dbgcmd
    0:000> !tt 0
    Setting position to the beginning of the trace
    Setting position: 15:0
    (1e5c.710): Break instruction exception - code 80000003 (first/second chance not available)
    Time Travel Position: 15:0
    eax=68e28100 ebx=00000000 ecx=77a266ac edx=69e34afc esi=69e3137c edi=00fa2000
    eip=77a266ac esp=00ddf3b8 ebp=00ddf608 iopl=0         nv up ei pl nz na pe nc
    cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000206
    ntdll!LdrpInitializeProcess+0x1d1c:
    77a266ac 83bdbcfeffff00  cmp     dword ptr [ebp-144h],0 ss:002b:00ddf4c4=00000000
    ```

5. [ホーム] メニューで、次のように選択します。**移動**メモリへのアクセスの案内配列の最初のポイントに前方に移動します。 

    ```dbgcmd
    0:000> g-
    Breakpoint 0 hit
    Time Travel Position: 5B:9C
    eax=cccccccc ebx=002b1000 ecx=00000000 edx=68d51a6c esi=013a1046 edi=001bf7d8
    eip=013a1735 esp=001bf6b8 ebp=001bf7d8 iopl=0         nv up ei pl nz na po nc
    cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000202
    DisplayGreeting!DetermineStringSize+0x25:
    013a1735 c745ec04000000  mov     dword ptr [ebp-14h],4 ss:002b:001bf7c4=cccccccc
    ```

   または、でしたがトレースの最後に出張し、配列のメモリ位置に書き込まれたトレース内でその最後のポイントを検索するコードを逆の順序で作業します。
      

**TTD を使用します。メモリ オブジェクトをメモリへのアクセスを表示するには**    

トレース内でどのメモリ アクセスを判断する別の方法、TTD を使用することです。メモリ オブジェクトと dx コマンドです。

1.  使用して、 **dx**を確認するコマンド、 *greeting*配列。 

    ```dbgcmd
    0:000> dx &greeting
    &greeting                 : 0xddf800 [Type: std::array<wchar_t,50> *]
       [+0x000] _Elems           : "꽘棶檙瞝???" [Type: wchar_t [50]]
    ```

    このトレースに*greeting* ddf800 時のメモリ内にあります。 

2. 使用して、 **dx**メモリ読み取り書き込みアクセスでは、そのアドレスで始まる 4 バイトで検索するコマンド。

    ```dbgcmd
    0:000> dx -r1 @$cursession.TTD.Memory(0xddf800,0xddf804, "rw")
    @$cursession.TTD.Memory(0x1bf7d0,0x1bf7d4, "rw")                
        [0x0]           
        [0x1]           
        [0x2]           
        [0x3]           
        [0x4]           
        [0x5]           
        [0x6]           
        [0x7]           
        [0x8]           
        [0x9]           
        [0xa]           
        ...         
    ```

3. メモリ アクセスの発生についての詳細情報を表示する項目のいずれかをクリックします。

    ```dbgcmd
    0:000> dx -r1 @$cursession.TTD.Memory(0xddf800,0xddf804, "rw")[5]
    @$cursession.TTD.Memory(0xddf800,0xddf804, "rw")[5]                
        EventType        : MemoryAccess
        ThreadId         : 0x710
        UniqueThreadId   : 0x2
        TimeStart        : 27:3C1 [Time Travel]
        TimeEnd          : 27:3C1 [Time Travel]
        AccessType       : Write
        IP               : 0x6900432f
        Address          : 0xddf800
        Size             : 0x4
        Value            : 0xddf818
    ```

4. トレースの位置を時間内にある [タイム トラベル] をクリックします。

    ```dbgcmd
    0:000> dx @$cursession.TTD.Memory(0xddf800,0xddf804, "rw")[5].TimeStart.SeekTo()
    @$cursession.TTD.Memory(0xddf800,0xddf804, "rw")[5].TimeStart.SeekTo()
    (1e5c.710): Break instruction exception - code 80000003 (first/second chance not available)
    Time Travel Position: 27:3C1
    eax=00ddf81c ebx=00fa2000 ecx=00ddf818 edx=ffffffff esi=00000000 edi=00b61046
    eip=6900432f esp=00ddf804 ebp=00ddf810 iopl=0         nv up ei pl nz ac po nc
    cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000212
    ucrtbased!_register_onexit_function+0xf:
    6900432f 51              push    ecx
   ```

5. 私たちは、最後に見つかったトレースの読み取り/書き込みメモリ アクセスの場合一覧の最後の項目をクリックしてまたは、追加します。Dx コマンドの末尾に Last() 関数。

    ```dbgcmd
    0:000> dx -r1 @$cursession.TTD.Memory(0xddf800,0xddf804, "rw").Last()
    @$cursession.TTD.Memory(0xddf800,0xddf804, "rw").Last()                
        EventType        : MemoryAccess
        ThreadId         : 0x710
        UniqueThreadId   : 0x2
        TimeStart        : 53:100E [Time Travel]
        TimeEnd          : 53:100E [Time Travel]
        AccessType       : Read
        IP               : 0x690338e4
        Address          : 0xddf802
        Size             : 0x2
        Value            : 0x45
    ```

6. 私たち、トレース内の位置に移動する [タイム トラベル] をクリックし、このラボで既に説明した手法を使用して、コードの実行時点で、さらに詳しく説明します。

詳細については、TTD です。メモリ オブジェクトを参照してください[TTD です。メモリ オブジェクト](time-travel-debugging-object-model.md)します。


**要約**      

この非常に小さいサンプルでは問題でしたが決定されて、わずか数行のコードを調べることで、大規模なプログラムでここで紹介する手法を使用して問題を検索するために必要な時間を短縮します。 

トレースが記録されると、トレースと再現手順を共有できるし、問題は、任意の PC ではオンデマンドで再現可能になります。  


---

## <a name="see-also"></a>参照

[旅行時間 - デバッグの概要](time-travel-debugging-overview.md)

[タイム トラベル デバッグ - 記録](time-travel-debugging-record.md)

[タイム トラベル デバッグ - トレースの再生](time-travel-debugging-replay.md)

[タイム トラベル デバッグ - トレース ファイルの使用](time-travel-debugging-trace-file-information.md)

---






