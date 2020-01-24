---
title: Time Travel Debugging - サンプル アプリのチュートリアル
description: このセクションでは、小規模C++なアプリのチュートリアルを紹介します。
ms.date: 01/23/2020
ms.localizationpriority: medium
ms.openlocfilehash: 4945f708ed5e8389af683d638b61e8b239c7e5de
ms.sourcegitcommit: ee70846334ab6710ec0f9143e9f3a3754bc69f98
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2020
ms.locfileid: "76706976"
---
# <a name="time-travel-debugging---sample-app-walkthrough"></a>Time Travel Debugging - サンプル アプリのチュートリアル

![時計を示す短いタイムトラベルロゴ](images/ttd-time-travel-debugging-logo.png)

このラボでは、コードの欠陥がある小さなサンプルプログラムを使用して、タイムトラベルデバッグ (TTD) を導入します。 TTD を使って問題をデバッグし、その根本原因を特定します。 この小さなプログラムの問題は簡単に見つけることができますが、一般的な手順はより複雑なコードでも使用できます。 この一般的な手順は、次のようにまとめることができます。

1. 失敗したプログラムのタイムトラベルトレースをキャプチャします。
2. 録音に格納されている例外イベントを確認するには、 [dx (Display Debugger Object Model Expression)](dx--display-visualizer-variables-.md)コマンドを使用します。 
3. [! Tt (タイムトラベル)](time-travel-debugging-extension-tt.md)コマンドを使用して、トレース内の例外イベントの位置に移動します。
4. その時点から、問題のあるコードがスコープ内になるまで、1つ前のステップが逆になります。
5. スコープ内のエラーコードを使用して、ローカル値を調べ、間違った値を含む可能性のある変数の仮説を作成します。
6. 間違った値を持つ変数のメモリアドレスを特定します。
7. Ba [(アクセス時に中断)](ba--break-on-access-.md)コマンドを使用して、問題のある変数のアドレスにメモリアクセス (ba) ブレークポイントを設定します。
8. "G-" を使用して、問題のある変数の最後のメモリへのアクセスを実行します。
9. その場所を確認するか、前にいくつかの手順を実行して、コードの欠陥点を確認してください。 そうすれば、完了です。
間違った値が他の変数から取得された場合は、2番目の変数のアクセスブレークポイントで別のブレークポイントを設定します。 
10. 2番目の問題のある変数で、g-を使用して最後のメモリアクセスポイントまで実行し直します。 その場所またはいくつかの手順にコードの欠陥が含まれているかどうかを確認します。 そうすれば、完了です。
11. エラーの原因となった間違った値が設定されているコードが見つかるまで、このプロセスを繰り返します。
 
この手順で説明する一般的な手法は、さまざまなコードの問題に適用されますが、一意の方法を必要とする一意のコードの問題があります。 このチュートリアルで示す手法は、デバッグツールセットを拡張するために使用する必要があります。また、TTD トレースでできることをいくつか示します。


## <a name="span-idlab_objectivesspanspan-idlab_objectivesspanspan-idlab_objectivesspanlab-objectives"></a><span id="Lab_objectives"></span><span id="lab_objectives"></span><span id="LAB_OBJECTIVES"></span>ラボの目標

このラボを完了すると、タイムトラベルトレースで一般的な手順を使用して、コード内の問題を見つけることができます。 

## <a name="span-idlab_setupspanspan-idlab_setupspanspan-idlab_setupspanlab-setup"></a><span id="Lab_setup"></span><span id="lab_setup"></span><span id="LAB_SETUP"></span>ラボのセットアップ

ラボを完了するには、次のハードウェアが必要です。

- Windows 10 を実行するラップトップまたはデスクトップコンピューター (ホスト) 

ラボを完成させるには、次のソフトウェアが必要です。

- WinDbg のプレビュー。 WinDbg Preview のインストールの詳細については、「 [Windbg プレビュー-インストール](https://docs.microsoft.com/windows-hardware/drivers/debugger/windbg-install-preview)」を参照してください。
- サンプルC++コードをビルドするための Visual Studio。

このラボには、次の3つのセクションがあります。

- [セクション 1: サンプルコードをビルドする](#build)
- [セクション 2: "DisplayGreeting" サンプルのトレースを記録する](#record)
- [セクション 3: トレースファイルの記録を分析してコードの問題を特定する](#analyze)

## <a name="span-idbuildspansection-1-build-the-sample-code"></a><span id="build"></span>セクション 1: サンプルコードをビルドする

*セクション1では、Visual Studio を使用してサンプルコードをビルドします。*

**Visual Studio でサンプルアプリを作成する**

1. Microsoft Visual Studio で、[**ファイル**&gt;**新しい**&gt;**プロジェクト/ソリューション...** ] をクリックし、 **C++** ビジュアルテンプレートをクリックします。

    Win32 コンソールアプリケーションを選択します。

    *Displaygreeting*のプロジェクト名を指定し、[ **OK]** をクリックします。

2. セキュリティ開発ライフサイクル (SDL) のチェックをオフにします。

    ![win32 アプリケーションウィザードのアプリケーション設定](images/ttd-time-travel-walkthrough-application-wizard-application-settings.png) 

3. **[完了]** をクリックします。

4. 次のテキストを Visual Studio の DisplayGreeting ウィンドウに貼り付けます。

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

6. Visual Studio で、[**プロジェクト**&gt; **displaygreeting のプロパティ**] をクリックします。 次に、[ **CC++ /** および**コード生成**] をクリックします。

    次のプロパティを設定します。

    | 設定              |  Value                        |
    |----------------------|-------------------------------|
    | セキュリティ チェック       | セキュリティチェックを無効にする (/GS-) |
    | 基本ランタイムチェック |  既定                      |

 
   > [!NOTE]
   > これらの設定は推奨されていませんが、コーディングを迅速化したり、特定のテスト環境を容易にしたりするために、これらの設定を使用することをユーザーがアドバイスするシナリオを想像することができます。
   >  

7. Visual Studio で、 **[ビルド]** 、[**ソリューションのビルド**&gt;] の順にクリックします。

    すべてうまくいくと、ビルドウィンドウには、ビルドが成功したことを示すメッセージが表示されます。

8. **ビルドされたサンプルアプリファイルの検索**

    ソリューションエクスプローラーで、 *Displaygreeting*プロジェクトを右クリックし、 **[エクスプローラーでフォルダーを開く]** を選択します。

    このサンプルのコンパイルされた exe ファイルとシンボル pdb ファイルを含むデバッグフォルダーに移動します。 たとえば、プロジェクトが格納されているフォルダーの場合は、 *C:\Projects\DisplayGreeting\Debug*に移動します。 

9. **コードの欠陥を含むサンプルアプリを実行する**

    .Exe ファイルをダブルクリックして、サンプルアプリを実行します。

    ![[エラーのあるアプリケーション] ダイアログボックス](images/ttd-time-travel-walkthrough-faulting-app-dialog-box.png)

    このダイアログボックスが表示されたら、 **[プログラムを閉じる]** を選択します。

    ![[エラーのあるアプリケーション] ダイアログボックス](images/ttd-time-travel-walkthrough-program-not-working-dialog-box.png)

    このチュートリアルの次のセクションでは、サンプルアプリの実行を記録して、この例外が発生した理由を確認できるかどうかを確認します。

## <a name="span-idrecordspansection-2-record-a-trace-of-the-displaygreeting-sample"></a><span id="record"></span>セクション 2: "DisplayGreeting" サンプルのトレースを記録する

*セクション2では、不適切なサンプルの "DisplayGreeting" アプリのトレースを記録します。*

サンプルアプリを起動して TTD トレースを記録するには、次の手順に従います。 TTD トレースの記録に関する一般的な情報については、「[タイムトラベルデバッグ-トレースの記録](time-travel-debugging-record.md)」を参照してください。

1. タイムトラベルトレースを記録できるように、WinDbg Preview を管理者として実行します。

2. WinDbg Preview で、**ファイル** > **デバッグ開始** > **実行可能ファイルの起動 (詳細)** を選択します。

3. 記録するユーザーモードの実行可能ファイルへのパスを入力するか、 **[参照]** を選択して実行可能ファイルに移動します。 WinDbg Preview で [起動実行可能ファイル] メニューを操作する方法の詳細については、「 [Windbg preview-user mode session を開始する](windbg-user-mode-preview.md)」を参照してください。

    ![[起動実行可能ファイル (詳細)] 画面に [記録の開始] チェックボックスが表示されている WinDbg プレビューのスクリーンショット](images/ttd-time-travel-walkthrough-recording-app.png)

4. [**タイムトラベルを含むレコード] デバッグ**ボックスをオンにして、実行可能ファイルが起動されたときにトレースを記録します。

5. **[構成]** をクリックして記録を開始します。

6. 記録の構成 ダイアログボックスが表示されたら、**記録** をクリックして実行可能ファイルを起動し、記録を開始します。

    ![Apath が temp に設定された、"記録の構成" ダイアログを示す WinDbg プレビューのスクリーンショット](images/ttd-time-travel-walkthrough-recording-configure.png)

7. トレースが記録されていることを示す [記録] ダイアログが表示されます。 その後すぐに、アプリケーションがクラッシュします。

8. **プログラムを閉じる** をクリックして、displaygreeting が動作を停止しました ダイアログボックスを閉じます。

   ![[エラーのあるアプリケーション] ダイアログボックス](images/ttd-time-travel-walkthrough-program-not-working-dialog-box.png)

9. プログラムがクラッシュすると、トレースファイルが閉じられ、ディスクに書き込まれます。

    ![1/1 キーフレームがインデックス付きの出力を表示する WinDbg Preview のスクリーンショット](images/ttd-time-travel-walkthrough-windbg-indexed-frames.png)

10. デバッガーは自動的にトレースファイルを開き、インデックスを作成します。 インデックス作成は、トレースファイルの効率的なデバッグを可能にするプロセスです。 このインデックス作成処理にかかる時間は、トレースファイルのサイズが大きいほど長くなります。

    ```dbgcmd
    (5120.2540): Break instruction exception - code 80000003 (first/second chance not available)
    Time Travel Position: D:0 [Unindexed] Index
    !index
    Indexed 10/22 keyframes
    Indexed 20/22 keyframes
    Indexed 22/22 keyframes
    Successfully created the index in 755ms.
    ```

   > [!NOTE]
   > キーフレームは、インデックス作成に使用されるトレース内の場所です。 キーフレームは自動的に生成されます。 大きいトレースには、より多くのキーフレームが含まれます。
   >

11. この時点で、トレースファイルの先頭に移動して、時間をさかのぼる準備ができています。

    TTD トレースの記録が完了したので、トレースを再生するか、トレースファイルを使用できます。たとえば、同僚と共有できます。 トレースファイルを操作する方法の詳細については、「[タイムトラベルデバッグ-トレースファイルの操作](time-travel-debugging-trace-file-information.md)」を参照してください。

このラボの次のセクションでは、トレースファイルを分析して、コードに関する問題を見つけます。

## <a name="span-idanalyzespansection-3-analyze-the-trace-file-recording-to-identify-the-code-issue"></a><span id="analyze"></span>セクション 3: トレースファイルの記録を分析してコードの問題を特定する

*セクション3では、トレースファイルの記録を分析して、コードの問題を特定します。*

**WinDbg 環境を構成する**

1.  シンボルパスにローカルシンボルの場所を追加し、次のコマンドを入力してシンボルを再度読み込みます。

    ```dbgcmd
    .sympath+ C:\MyProjects\DisplayGreeting\Debug
    .reload
    ```

2.  次のコマンドを入力して、ソースパスにローカルコードの場所を追加します。

    ```dbgcmd
    .srcpath+ C:\MyProjects\DisplayGreeting\DisplayGreeting
    ```

3. スタックおよびローカル変数の状態を表示できるようにするには、WinDbg Preview リボンで、**表示**、 **ローカル** 、および **ビュー**と**スタック** を選択します。 ウィンドウを整理して、それらのウィンドウ、ソースコード、およびコマンドウィンドウを同時に表示できるようにします。

4.  WinDbg Preview リボンで、**ソース** を選択し、**ソースファイル** を開きます。 DisplayGreeting .cpp ファイルを見つけて開きます。

**例外を確認する**

1. トレースファイルが読み込まれると、例外が発生したことを示す情報が表示されます。

    ```dbgcmd
    2fa8.1fdc): Break instruction exception - code 80000003 (first/second chance not available)
    Time Travel Position: 15:0
    eax=68ef8100 ebx=00000000 ecx=77a266ac edx=69614afc esi=6961137c edi=004da000
    eip=77a266ac esp=0023f9b4 ebp=0023fc04 iopl=0         nv up ei pl nz na pe nc
    cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000206
    ntdll!LdrpInitializeProcess+0x1d1c:
    77a266ac 83bdbcfeffff00  cmp     dword ptr [ebp-144h],0 ss:002b:0023fac0=00000000
    ```
2. Dx コマンドを使用して、記録内のすべてのイベントを一覧表示します。 例外イベントは、イベントに一覧表示されます。

    ```dbgcmd
    0:000> dx -r1 @$curprocess.TTD.Events
    ...
    [0x2c]           : Module Loaded at position: 9967:0
    [0x2d]           : Exception at 9BDC:0
    [0x2e]           : Thread terminated at 9C43:0
    ...

    ```

   > [!NOTE]
   > このチュートリアルでは、余分な出力が削除されたことを示すために、3つの期間を使用します。
   >

3. 例外イベントをクリックすると、その TTD イベントに関する情報が表示されます。 

    ```dbgcmd
    0:000> dx -r1 @$curprocess.TTD.Events[17]
    @$curprocess.TTD.Events[17]                 : Exception at 68:0
        Type             : Exception
        Position         : 68:0 [Time Travel]
        Exception        : Exception of type Hardware at PC: 0X540020
    ```

4. 例外フィールドをクリックして、例外データをさらにドリルダウンします。 

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

   例外データは、これが CPU によってスローされたハードウェア障害であることを示します。 また、これがアクセス違反であることを示す、0xc0000005 の例外コードも提供します。 これは通常、アクセス権のないメモリへの書き込みを試行していることを示しています。

5. 例外イベントの [Time トラベル] リンクをクリックして、トレース内のその位置に移動します。

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

    この出力では、スタックと基本ポインターが2つの非常に異なるアドレスを指していることに注意してください。

    ```dbgcmd
    esp=00effe4c ebp=00520055
    ```

    これは、スタックが破損していることを示している可能性があります。関数が返され、スタックが破損している可能性があります。 これを検証するには、CPU 状態が破損する前にに戻り、スタックの破損が発生したことを確認できるかどうかを確認する必要があります。

**ローカル変数を調べ、コードのブレークポイントを設定します。**

トレースで障害が発生した時点では、エラー処理コードの実際の原因の後にいくつかの手順を終了するのが一般的です。 タイムトラベルを使用すると、実際の根本原因を特定するために、一度に命令を戻すことができます。

1. **[ホーム]** リボンで、 **[ステップイン戻る]** コマンドを使用して、3つの手順を実行します。 このようにして、引き続きスタックウィンドウとメモリウィンドウを確認します。

    コマンドウィンドウには、時間の移動位置とレジスタが表示されます。手順に従って3つの手順を実行します。

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
   > このチュートリアルでは、コマンドの出力に、コマンドラインの使用法を使用するユーザーがコマンドラインコマンドを使用できるようにする UI メニューオプションの代わりに使用できるコマンドを示します。
   >

2. トレースのこの時点で、スタックと基本ポインターにはより意味のある値が含まれているため、破損が発生したコードのポイントに近づいているように見えます。

    ```dbgcmd
    esp=00effd94 ebp=00effe44
    ```

    また、[ローカル] ウィンドウには対象アプリからの値が含まれており、[ソースコード] ウィンドウにはトレースのこの時点で実行する準備ができているコード行が強調表示されていることに注目してください。

    ![メモリ ASCII 出力とソースコードウィンドウを使用したローカルウィンドウを示す WinDbg Preview のスクリーンショット](images/ttd-time-travel-walkthrough-locals-window.png)

3. さらに詳しく調査するために、[メモリ] ウィンドウを開いて、 *0x00effe44*の基本ポインターのメモリアドレスの近くにコンテンツを表示することができます。

4. 関連する ASCII 文字を表示するには、メモリ リボンで、**テキスト**、**ascii** の順に選択します。

    ![メモリ ascii 出力とソースコードウィンドウを示す winbbg preview のスクリーンショット](images/ttd-time-travel-walkthrough-memory-ascii.png)

5. 基本ポインターが命令を指しているのではなく、メッセージテキストを指しています。 ここでは、スタックが破損している時点に近い状態になる可能性があります。 さらに詳しく調査するには、ブレークポイントを設定します。

> [!NOTE]
> この非常に小さなサンプルでは、コードを簡単に調べることができますが、数百行のコードがあり、サブルーチンが多数ある場合は、ここで説明する手法を使用して、問題の特定に必要な時間を短縮できます。
>

**TTD とブレークポイント**

ブレークポイントの使用は、特定のイベントでコードの実行を一時停止するための一般的な方法です。  TTD を使用すると、トレースが記録された後にブレークポイントがヒットするまで、ブレークポイントを設定し、時間をさかのぼって戻すことができます。 問題が発生した後にプロセスの状態を確認する機能は、ブレークポイントの最適な場所を特定するために、TTD に固有の追加のデバッグワークフローを有効にします。 

**メモリアクセスのブレークポイント**

メモリ位置にアクセスしたときに起動するブレークポイントを設定できます。 次の構文を使用して、 **ba** (アクセス時の中断) コマンドを使用します。

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
<th align="left">オプション</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>e</p></td>
<td align="left"><p>実行 (CPU がアドレスから命令をフェッチする場合)</p></td>
</tr>
<tr class="even">
<td align="left"><p>r</p></td>
<td align="left"><p>読み取り/書き込み (CPU がそのアドレスに対して読み取りまたは書き込みを行う場合)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>週</p></td>
<td align="left"><p>書き込み (CPU がそのアドレスに書き込む場合)</p></td>
</tr>
</tbody>
</table>


常に4つのデータブレークポイントを設定できます。また、データを適切に配置していることを確認してください。または、ブレークポイントをトリガーしないことに注意してください (単語は2で割り切れるアドレスで終わる必要があります。、、および0または8によって quadwords)。

**基本ポインターの メモリアクセスのブレークポイントを設定する。**    

1.  トレースのこの時点で、基本ポインター-ebp への書き込みメモリアクセスにブレークポイントを設定します。この例では、00effe44 です。 これを行うには、監視するアドレスを使用して**ba**コマンドを使用します。 4バイトの書き込みを監視するため、w4 を指定します。 

    ```dbgcmd
    0:000> ba w4 00effe44
    ```

2. **[表示]** 、 **[ブレークポイント]** の順に選択して、意図したとおりに設定されていることを確認

    ![1つのブレークポイントがある、WinDbg のプレビューウィンドウ](images/ttd-time-travel-walkthrough-view-breakpoints.png)


3.  [ホーム] メニューの [戻る]**を選択し**て、ブレークポイントにヒットするまで戻ります。

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

4. **[表示]** 、 **[ローカル]** の順に選択します。 [ローカル] ウィンドウでは、*コピー先*の変数にメッセージの一部だけが含まれ、*ソース*にすべてのテキストが含まれていることがわかります。 この情報は、スタックが破損しているという概念をサポートしています。 

    ![WinDbg プレビューの [ローカル] ウィンドウのスクリーンショット](images/ttd-time-travel-walkthrough-locals-window.png)


5. この時点で、プログラムスタックを調べて、アクティブなコードを確認できます。 **ビュー**のリボンで、 **[スタック]** を選択します。 

    ![WinDbg プレビュースタックウィンドウのスクリーンショット](images/ttd-time-travel-walkthrough-stack-window.png)


Microsoft が提供する wscpy_s () 関数には、このようなコードのバグがあることはほとんどないため、スタックを詳しく見ていきます。 スタックには、そのことが案内されます。 main はあいさつを呼び出します。GetCppConGreeting。 非常に小さなコードサンプルでは、この時点でコードを開くだけで、エラーが非常に簡単に見つかる可能性があります。 しかし、より大規模で複雑なプログラムで使用できる手法を示すために、新しいブレークポイントを設定してさらに調査します。 


**GetCppConGreeting 関数のアクセスブレークポイントを設定する**        

1. 既存のブレークポイントを右クリックし、**削除** を選択して、既存のブレークポイントをクリアするには、ブレークポイント ウィンドウを使用します。

2. DisplayGreeting のアドレスを確認します。**Dx**コマンドを使用して GetCppConGreeting 関数を実行します。

    ```dbgcmd
    0:000> dx &DisplayGreeting!GetCppConGreeting
    &DisplayGreeting!GetCppConGreeting                 : 0xb61720 [Type: void (__cdecl*)(wchar_t *,unsigned int)]
        [Type: void __cdecl(wchar_t *,unsigned int)]
    ```

3. メモリアクセスにブレークポイントを設定するには、 **ba**コマンドを使用します。 関数は実行のためにメモリから読み取られるだけなので、r 読み取りのブレークポイントを設定する必要があります。

    ```dbgcmd
    0:000> ba r4 b61720
    ```

4. [ブレークポイント] ウィンドウで、ハードウェア読み取りブレークポイントがアクティブであることを確認します。

    ![1つのハードウェア読み取りブレークポイントを持つ、ブレークポイントウィンドウを表示している WinDbg プレビュー](images/ttd-time-travel-walkthrough-hardware-write-breakpoint.png)

5. あいさつ文のサイズについては、sizeof (挨拶) の値を表示するようにウォッチウィンドウを設定します。 ビューのリボンで、 **[ウォッチ]** を選択し、 *sizeof (あいさつ)* を入力します。

    ![[ウォッチローカル] ウィンドウを表示している WinDbg プレビュー](images/ttd-time-travel-watch-locals.png)

6. タイムトラベルメニューで、 **[タイムトラベル]** を使用して開始するか、`!tt 0`コマンドを使用してトレースの開始位置に移動します。

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

7. ホーム メニューの **移動** を選択するか、`g` コマンドを使用して、ブレークポイントにヒットするまでコード内を前方に移動します。

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

8. ホーム メニューの **ステップアウト** を選択するか、`g-u` コマンドを使用して1つの手順を実行します。

    ```dbgcmd
    0:000> g-u
    Time Travel Position: 4B:1AA
    eax=00ddf800 ebx=00fa2000 ecx=00ddf800 edx=00b61046 esi=00b61046 edi=00b61046
    eip=00b61917 esp=00ddf7ac ebp=00ddf864 iopl=0         nv up ei pl nz na po nc
    cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000202
    DisplayGreeting!main+0x27:
    00b61917 e8def7ffff      call    DisplayGreeting!ILT+245(?GetCppConGreetingYAXPA_WIZ) (00b610fa)
    ```

9. 根本原因が見つかったようです。 宣言した*あいさつ*配列は長さが50文字で、GetCppConGreeting に渡す sizeof (挨拶) は 0x64, 100) です。  

    ![[ウォッチのローカル] ウィンドウを使用して、X64 を表示した挨拶コードを表示する WinDbg プレビュー](images/ttd-time-travel-walkthrough-code-with-watch-locals.png)

    さらに、サイズの問題についても説明しますが、メッセージの長さは75文字で、文字列の末尾を含む76であることがわかります。

    ```dbgcmd
    HELLO FROM THE WINDBG TEAM. GOOD LUCK IN ALL OF YOUR TIME TRAVEL DEBUGGING!
    ```

10. コードを修正する1つの方法は、文字配列のサイズを100に拡張することです。

    ```cpp
    std::array <wchar_t, 100> greeting{};
    ```

    また、このコード行で、sizeof (挨拶) を size (挨拶) に変更する必要もあります。

    ```cpp
     GetCppConGreeting(greeting.data(), size(greeting));
    ```

11. これらの修正を検証するには、コードを再コンパイルし、エラーなしで実行されていることを確認します。

**ソースウィンドウを使用したブレークポイントの設定**

1. この調査を行う別の方法として、コード行をクリックしてブレークポイントを設定する方法もあります。 たとえば、ソースウィンドウで [std: array definition] 行の右側をクリックすると、そこにブレークポイントが設定されます。

    ![Std: array に設定されているブレークポイントを示すソースウィンドウのスクリーンショット](images/ttd-time-travel-walkthrough-source-window-breakpoint.png)

2. タイムトラベルメニューで、[**タイムトラベル] を**使用して、トレースの開始位置に移動します。

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

3. ホーム リボンで、**移動** をクリックして、ブレークポイントにヒットするまで戻ります。

    ```dbgcmd
    Breakpoint 0 hit
    Time Travel Position: 5B:AF
    eax=0000000f ebx=00c20000 ecx=00000000 edx=00000000 esi=013a1046 edi=00effa60
    eip=013a17c1 esp=00eff970 ebp=00effa60 iopl=0         nv up ei pl nz na po nc
    cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000202
    DisplayGreeting!DisplayGreeting+0x41:
    013a17c1 8bf4            mov     esi,esp
    ```

***あいさつ*変数のアクセスのブレークポイントを設定する**

この調査を実行するもう1つの方法は、問題のある変数にブレークポイントを設定し、変更されているコードを調べることです。 たとえば、GetCppConGreeting メソッドで案内変数にブレークポイントを設定するには、次の手順を使用します。

このチュートリアルの部分では、前のセクションのブレークポイントに配置されていることを前提としています。 

1. **[表示]** 、 **[ローカル]** の順に選択します。 [ローカル] ウィンドウでは、現在のコンテキストで*案内*を表示できるため、メモリの場所を決定できます。

2. **Dx**コマンドを使用して、*グリーティング*の配列を調べます。

    ```dbgcmd
    0:000> dx &greeting
    &greeting                 : 0xddf800 [Type: std::array<wchar_t,50> *]
       [+0x000] _Elems           : "꽘棶檙瞝???" [Type: wchar_t [50]]
    ```

    このトレースでは、ddf800 のメモリに*グリーティング*が配置されています。

3. 既存のブレークポイントを右クリックし、**削除** を選択して、既存のブレークポイントをクリアするには、ブレークポイント ウィンドウを使用します。

4. 書き込みアクセスを監視するメモリアドレスを使用して、 **ba**コマンドでブレークポイントを設定します。

    ```dbgcmd
    ba w4 ddf800
    ```

5. タイムトラベルメニューで、[**タイムトラベル] を**使用して、トレースの開始位置に移動します。

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

6. ホーム メニューの **移動** を選択して、グリーティング配列の最初のメモリアクセスポイントに移動します。 

    ```dbgcmd
    0:000> g-
    Breakpoint 0 hit
    Time Travel Position: 5B:9C
    eax=cccccccc ebx=002b1000 ecx=00000000 edx=68d51a6c esi=013a1046 edi=001bf7d8
    eip=013a1735 esp=001bf6b8 ebp=001bf7d8 iopl=0         nv up ei pl nz na po nc
    cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000202
    DisplayGreeting!GetCppConGreeting+0x25:
    013a1735 c745ec04000000  mov     dword ptr [ebp-14h],4 ss:002b:001bf7c4=cccccccc
    ```

   もう1つの方法として、トレースの最後まで旅行し、コードを逆に使用して、配列のメモリ位置に書き込んだトレースの最後のポイントを見つけることもできます。

**TTD を使用します。メモリアクセスを表示するためのメモリオブジェクト**

トレースメモリ内のどのポイントがアクセスされたかを判断するもう1つの方法は、TTD を使用することです。メモリオブジェクトと dx コマンド。

1. **Dx**コマンドを使用して、*グリーティング*の配列を調べます。

    ```dbgcmd
    0:000> dx &greeting
    &greeting                 : 0xddf800 [Type: std::array<wchar_t,50> *]
       [+0x000] _Elems           : "꽘棶檙瞝???" [Type: wchar_t [50]]
    ```

    このトレースでは、ddf800 のメモリに*グリーティング*が配置されています。 

2. **Dx**コマンドを使用して、そのアドレスから始まるメモリの4バイトを読み取り書き込みアクセスで確認します。

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

3. いずれかの項目をクリックすると、その発生したメモリアクセスの詳細情報が表示されます。

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

4. [タイムトラベル] をクリックして、特定の時点でトレースを配置します。

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

5. トレースでの読み取り/書き込みメモリアクセスが最後に発生したい場合は、一覧の最後の項目をクリックするか、を追加します。Last () 関数を dx コマンドの最後まで実行します。

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

6. その後、[タイムトラベル] をクリックしてトレース内のその位置に移動し、このラボで前述した手法を使用して、その時点でのコードの実行をさらに詳しく調べることができます。

TTD の詳細については、「」を参照してください。メモリオブジェクト、「TTD」を参照してください[。メモリオブジェクト](time-travel-debugging-object-model.md)。

## <a name="summary"></a>概要

この非常に小さなサンプルでは、数行のコードを見て問題を特定できましたが、大規模なプログラムでは、ここで説明する手法を使用して、問題の特定に必要な時間を短縮できます。

トレースが記録されると、トレースと再現の手順を共有できます。また、問題はどの PC でも必要に応じて再現できます。  

## <a name="see-also"></a>関連項目

[タイムトラベルのデバッグ-概要](time-travel-debugging-overview.md)

[タイムトラベルデバッグ-記録](time-travel-debugging-record.md)

[タイムトラベルデバッグ-トレースを再生する](time-travel-debugging-replay.md)

[タイムトラベルデバッグ-トレースファイルの操作](time-travel-debugging-trace-file-information.md)
