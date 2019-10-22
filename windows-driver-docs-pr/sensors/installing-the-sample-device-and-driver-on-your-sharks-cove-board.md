---
title: サメ Cove board にサンプルデバイスとドライバーをインストールする
description: 次の手順に従って、サンプルドライバーをインストールし、サメ Cove board の J1C1 ヘッダーに ADXL345 加速度計をアタッチします。
ms.assetid: A67EBD9C-9C5A-49D3-9205-37FC4396DF56
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a9012ca8c4543a94397e89da9a2eaec48205974
ms.sourcegitcommit: 19ba939a139e8ad62b0086c30b2fe772a2320663
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/21/2019
ms.locfileid: "72681936"
---
# <a name="install-the-sample-device-and-driver-on-your-sharks-cove-board"></a>サメ Cove board にサンプルデバイスとドライバーをインストールする


次の手順に従って、サンプルドライバーをインストールし、サメ Cove board の J1C1 ヘッダーに ADXL345 加速度計をアタッチします。

> [!WARNING]
> サメ Cove hardware development board はサポートされなくなりました。 現在サポートされているボードの一覧については、「[SoCs and custom boards (SoC とカスタム ボード)](https://docs.microsoft.com/windows/iot-core/learn-about-hardware/socsandcustomboards)」をご覧ください。

## <a name="install-windows-on-the-sharks-cove-board"></a>Sharks Cove ボードに Windows をインストールする

サメ Cove board を入手する方法と、ボードに Windows をインストールする方法の詳細については、「[サメ Cove hardware development board](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/sharks-cove-hardware-development-board) and SharksCove.org」を参照してください。
## <a name="modify-the-adxl345-to-work-with-the-sharks-cove"></a>サメ Cove を使用するように ADXL345 を変更する


ADXL345 を I2C モードで設定するには、次に示すように、VDD 出力を CS シグナルに接続します。

![adxl345 ブレイクボードボード](images/adxl-breakout-board.png)

## <a name="attach-the-modified-adxl345-to-the-sharks-cove"></a>変更した ADXL345 をサメ Cove にアタッチします。


ADXL345 が I2C モードで動作している場合は、サメ Cove ボードの J1C1 ヘッダーにアタッチします。 電源コネクタが左上隅に表示されている場合は、右下隅に次のヘッダーが表示されます。

![j1c1 ヘッダー](images/j1c1-header.png)

次に示すように、ADXL345 ピンを J1C1 ヘッダーピンに接続します。

![j1c1 ピン](images/pin-outs.png)

## <a name="install-kits-and-tools"></a>キットとツールをインストールする


ドライバー開発環境には、*ホスト コンピューター*と*ターゲット コンピューター*という、2 台のコンピューターがあります。 ターゲット コンピューターは*テスト コンピューター*とも呼ばれます。 ドライバーの開発とビルドは、ホスト コンピューター上の Microsoft Visual Studio で行います。 デバッガーはホスト コンピューター上で実行され、Visual Studio のユーザー インターフェイスで利用できます。 ドライバーのテストとデバッグを行うときは、ドライバーをターゲット コンピューター上で実行します。 この場合、Sharks Cove ボードがターゲット コンピューターになります。

ホストコンピューターで、「[サメ Cove hardware development board](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/sharks-cove-hardware-development-board)」に記載されているキットとツールをインストールします。

## <a name="download-and-extract-the-spbaccelerometer-sample"></a>SpbAccelerometer サンプルをダウンロードして抽出する


ホストコンピューターで[このページ](https://go.microsoft.com/fwlink/p?linkid=506965)にアクセスし、[ダウンロード] ボタンをクリックします。 **[保存]** をクリックし、 **[フォルダーを開く]** をクリックします。 SpbAccelerometer Sample Driver (UMDF Version 1) .zip を右クリックし、 **[すべて展開]** を選択します。 抽出されたファイルのフォルダーを指定または参照します。 たとえば、c: \\SpbAccelerometer に抽出できます。

## <a name="open-the-driver-solution-in-visual-studio"></a>Visual Studio でドライバーソリューションを開く


ホストコンピューターで、抽出されたサンプルが含まれているフォルダーにアクセスします。 ソリューションファイル SpbAccelerometer をダブルクリックします。 Visual Studio で、ソリューションエクスプローラーを見つけます。 (まだ開いていない場合は、 **[表示]** メニューの **[ソリューションエクスプローラー]** をクリックします)。ソリューションエクスプローラーには、2つのプロジェクトを持つソリューションが1つ表示されます。 **SpbAccelerometer**という名前のドライバープロジェクトと、package という名前のパッケージ**プロジェクト (小**文字) があります。

## <a name="set-the-configuration-and-platform-in-visual-studio"></a>Visual Studio での構成とプラットフォームの設定


Visual Studio のソリューションエクスプローラーで、 **[ソリューション ' SpbAccelerometer ' (プロジェクト2プロジェクト)]** を右クリックし、 **[Configuration Manager]** を選択します。 構成とプラットフォームを設定します。 構成に**win 8.1 のデバッグ**が実行されていることを確認し、プラットフォームを**Win32**に設定します。 これは、ドライバープロジェクトとパッケージプロジェクトの両方に対して実行します。 **[配置]** ボックスをオンにしないでください。

## <a name="build-the-sample-using-visual-studio"></a>Visual Studio を使用してサンプルをビルドする


Visual Studio の **[ビルド]** メニューで、 **[ソリューションのビルド]** を選択します。

## <a name="locate-the-built-driver-package"></a>ビルドされたドライバーパッケージを検索する


エクスプローラーで、ビルドしたドライバーパッケージが格納されているフォルダーに移動します。 たとえば、C: \\SpbAccelerometer \\Win8 デバッグ \\Packge ます。

パッケージには次のファイルが含まれています。

| ファイル                  | 説明                                                                       |
|-----------------------|-----------------------------------------------------------------------------------|
| SpbSamples.cat        | パッケージ全体の署名として機能する、署名されたカタログファイル。      |
| SpbAccelerometer  | ドライバーのインストールに必要な情報が含まれている情報 (INF) ファイル。 |
| WudfUpdate \_01011 .dll | WDF の共同インストーラー。                                                          |
| SpbAccelerometer  | ドライバーファイル。                                                                  |



## <a name="alter-the-secondary-system-description-table-ssdt"></a>Secondary System Description Table (SSDT) を変更する


1.  x86 バージョンの ASL.exe を Sharks Cove ボードにコピーします。 ASL は、Windows Driver Kit (WDK) に含まれています。

    例: C: \\Program Files (x86) \\Windows Kit \\8 .1 \\Tools \\x86 \\ACPIVerify \\ASL .exe

2.  サメ Cove ボードで、管理者としてコマンドプロンプトウィンドウを開きます。 次のコマンドを入力して、SSDT を逆コンパイルします。

    **asl /tab=ssdt**

    このコマンドによって Ssdt.asl が作成されます。

3.  Ssdt.asl をメモ帳などで開きます。

    ``` syntax
    DefinitionBlock("SSDT.AML", "SSDT", 0x01, "Intel_", "ADebTabl", 0x00001000)
    {
        Scope()
        {
            Name(DPTR, 0x3bf2d000)
            Name(EPTR, 0x3bf3d000)
            Name(CPTR, 0x3bf2d010)
            Mutex(MMUT, 0x0)
            Method(MDBG, 0x1, Serialized)
            {
                Store(Acquire(MMUT, 0x3e8), Local0)
                If(LEqual(Local0, Zero))
                {
                    OperationRegion(ABLK, SystemMemory, CPTR, 0x10)
                    Field(ABLK, ByteAcc, NoLock, Preserve)
                    {
                        AAAA, 128
                    }
                    Store(Arg0, AAAA)
                    Add(CPTR, 0x10, CPTR)
                    If(LNot(LLess(CPTR, EPTR)))
                    {
                        Add(DPTR, 0x10, CPTR)
                    }
                    Release(MMUT)
                }
                Return(Local0)
            }
        }

        // Insert a Scope(_SB_) and a Device entry here.

    }
    ```

4.  Scope(\_SB\_) エントリを挿入します。 スコープ エントリ内に、ユーザー独自の Device エントリを挿入します。 ADXL345 加速度計のスコープ (\_SB \_) エントリとデバイスエントリを次に示します。

    ``` syntax
    Scope(_SB_)
    {
        Device(SPBA)
        {
            Name(_HID, "SpbAccelerometer")
            Name(_UID, 1)



        Method(_CRS, 0x0, NotSerialized)
        {
            Name(RBUF, ResourceTemplate()
            {          
                I2CSerialBus(0x53, ControllerInitiated, 400000, AddressingMode7Bit, "\\_SB.I2C3", 0, ResourceConsumer) 
                GpioInt(Edge, ActiveHigh, Exclusive, PullDown, 0, "\\_SB.GPO2") {0x17}
            })

            Return(RBUF)
        }


        Method(_DSM, 0x4, NotSerialized)
        {
            If(LEqual(Arg0, Buffer(0x10)
            {
                0x1e, 0x54, 0x81, 0x76, 0x27, 0x88, 0x39, 0x42, 0x8d, 0x9d, 0x36, 0xbe, 0x7f, 0xe1, 0x25, 0x42
            }))
            {
                If(LEqual(Arg2, Zero))
                {
                    Return(Buffer(One)
                    {
                        0x03
                    })
                }

                If(LEqual(Arg2, One))
                {
                    Return(Buffer(0x4)
                    {
                        0x00, 0x01, 0x02, 0x03
                    })
                }
            }
            Else
            {
                Return(Buffer(One)
                {
                    0x00
                })
            }
        } // Method(_DSM ...)

    } // Device(SPBA)

} // Scope(_SB_)
```

この例では、`ResourceTemplate()` の下にあるエントリは、加速度計で 2 つのハードウェア リソース (特定の I2C バス コント ローラーへの接続 ID (I2C3) および GPIO 割り込み) が必要であることを示しています。 割り込みでは、GPO2 という名前の GPIO コント ローラーのピン 0x17 を使います。


5.  ユーザー独自の Device エントリを Ssdt.asl に追加した後で、次のコマンドを入力して Ssdt.asl をコンパイルします。

    **asl ssdt.asl**

    これにより、コンパイル済みの出力が Ssdt.aml という名前のファイルに配置されます。

6.  Sharks Cove ボードに対してテスト署名が有効になっていることを確認します。

    **注**  テスト署名は、プロビジョニング中に自動的に有効になります。




Sharks Cove ボードで、管理者としてコマンド プロンプト ウィンドウを開きます。 次のコマンドを入力します。

**bcdedit /enum {current}**

出力に `testsigning Yes` が表示されることを確認します。

``` syntax
Windows Boot Loader
-------------------
identifier              {current}
...
testsigning             Yes
...
```

テスト署名を手動で有効にする場合は、次の手順を実行します。

1.  管理者としてコマンド プロンプト ウィンドウを開き、次のコマンドを入力します。

    **bcdedit /set TESTSIGNING ON**

2.  Sharks Cove ボードを再起動します。 ボードを再起動するとき、音量を上げるボタンを押したままにします。 **[Device Manager (デバイス マネージャー)] &gt; [System Setup (システム セットアップ)] &gt; [Boot (ブート)]** の順に移動します。 **[UEFI Security Boot (UEFI セキュリティ ブート)]** を **[Disabled (無効)]** に設定します。
3.  変更を保存し、Windows の起動を続けます。


7.  更新された SSDT を読み込むには、管理者としてコマンド プロンプト ウィンドウを開き、次のコマンドを入力します。

    **asl /loadtable ssdt.aml**

    Sharks Cove ボードを再起動します。

## <a name="install-and-run-the-sample-driver"></a>サンプルドライバーをインストールして実行する


1.  ホストコンピューターで、Visual Studio で SpbAccelerometer ソリューションを開きます。
2.  ソリューションエクスプローラーで、 **[パッケージ]** (小文字) をダブルクリックし、 **[プロパティ]** を選択します。 **[Driver Install (ドライバーのインストール)] &gt; [配置]** の順に移動します。 [**デプロイの有効化] をオンに**します。 **[展開前にドライバーの以前のバージョンを削除する]** チェック ボックスをオンにします。 **[ターゲットコンピューター名]** に、前にプロビジョニングしたサメ Cove board の名前を入力します。 **[Install and Verify (インストールと確認)]** を選びます。 **[OK]** をクリックします。
3.  **[デバッグ]** メニューの **[デバッグ開始]** をクリックします。 ドライバーパッケージは、サメ Cove board に自動的にコピーされます。 ドライバーが自動的にインストールされ、読み込まれます。 (Visual Studio のホストコンピューターで実行されている) Windows ユーザーモードデバッガーは、ドライバーをホストしている Wudfhost .exe のインスタンス (サメ Cove board で実行されている) に自動的にアタッチされます。








