---
title: サメ Cove ボード上のサンプル デバイスとドライバーをインストールします。
description: サンプル ドライバーをインストールして ADXL345 加速度計をサメ Cove ボードに J1C1 ヘッダーにアタッチします。 これらの手順に従います。
ms.assetid: A67EBD9C-9C5A-49D3-9205-37FC4396DF56
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4933140d66f1aa5a7d8f9b0ce89d384aa87e808c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529671"
---
# <a name="install-the-sample-device-and-driver-on-your-sharks-cove-board"></a>サメ Cove ボード上のサンプル デバイスとドライバーをインストールします。


サンプル ドライバーをインストールして ADXL345 加速度計をサメ Cove ボードに J1C1 ヘッダーにアタッチします。 これらの手順に従います。

## <a name="install-windows-on-the-sharks-cove-board"></a>サメ Cove ボード上の Windows をインストールします。


サメ Cove ボードを取得する方法と、ボード上で Windows をインストールする方法については、次を参照してください。[サメ Cove ハードウェア開発ボード](https://msdn.microsoft.com/library/windows/hardware/dn745910)と[SharksCove.org](https://go.microsoft.com/fwlink/p/?linkid=403167)します。

## <a name="modify-the-adxl345-to-work-with-the-sharks-cove"></a>サメ Cove を使用する ADXL345 を変更します。


ADXL345 I2C モードを設定するには、次のように、CS 信号を出力 VDD を接続します。

![adxl345 ブレイク アウト ボード](images/adxl-breakout-board.png)

## <a name="attach-the-modified-adxl345-to-the-sharks-cove"></a>サメ Cove に変更された ADXL345 をアタッチします。


ADXL345 I2C モードで動作しているが、ときに、サメ Cove ボード J1C1 ヘッダーにアタッチします。 電源コネクタは、左上隅に表示されたら、右上隅にあるこのヘッダーが表示されます。

![j1c1 ヘッダー](images/j1c1-header.png)

J1C1 ヘッダー ピン次に示すように ADXL345 ピンを接続します。

![j1c1 ピン](images/pin-outs.png)

## <a name="install-kits-and-tools"></a>キットとツールをインストールします。


ドライバー開発環境には、*ホスト コンピューター*と*ターゲット コンピューター*という、2 台のコンピューターがあります。 ターゲット コンピューターは*テスト コンピューター*とも呼ばれます。 ドライバーの開発とビルドは、ホスト コンピューター上の Microsoft Visual Studio で行います。 デバッガーはホスト コンピューター上で実行され、Visual Studio のユーザー インターフェイスで利用できます。 ドライバーのテストとデバッグを行うときは、ドライバーをターゲット コンピューター上で実行します。 この場合、Sharks Cove ボードがターゲット コンピューターになります。

ホスト コンピューターにインストール キットとツール」の説明に従って[サメ Cove ハードウェア開発ボード](https://msdn.microsoft.com/library/windows/hardware/dn745910)します。

## <a name="download-and-extract-the-spbaccelerometer-sample"></a>ダウンロードし、抽出 SpbAccelerometer サンプル


ホスト コンピューター上に移動[このページ](https://go.microsoft.com/fwlink/p?linkid=506965)[ダウンロード] ボタンをクリックします。 をクリックして**保存**、 をクリックし、**フォルダーを開く**します。 SpbAccelerometer サンプル ドライバー (UMDF バージョン 1) .zip を右クリックし、選択**すべて展開**します。 指定するか、抽出したファイルのフォルダーを参照します。 たとえば、c: 情報を抽出することが\\SpbAccelerometer します。

## <a name="open-the-driver-solution-in-visual-studio"></a>Visual Studio でのドライバー ソリューションを開く


ホスト コンピューターには、解凍したサンプルのあるフォルダーに移動します。 SpbAccelerometer.sln、ソリューション ファイルをダブルクリックします。 Visual Studio で、ソリューション エクスプ ローラーを見つけます。 (これがまだ開いていない場合は、選択**ソリューション エクスプ ローラー**から、**ビュー**メニュー)。ソリューション エクスプ ローラーでは、2 つのプロジェクトを含む 1 つのソリューションを確認できます。 という名前のドライバーのプロジェクトがある**SpbAccelerometer**とという名前のパッケージ プロジェクト**パッケージ**(小文字)。

## <a name="set-the-configuration-and-platform-in-visual-studio"></a>Visual Studio での構成とプラットフォームを設定します。


ソリューション エクスプ ローラーで、Visual Studio で右クリックして**ソリューション 'SpbAccelerometer' (2 プロジェクト)**、選択**Configuration Manager**します。 構成とプラットフォームを設定します。 確認します構成**Win8.1 デバッグ**、プラットフォームを設定して**Win32**します。 このドライバーのプロジェクトとパッケージのプロジェクトの両方に対して行います。 オンにしないでください、**デプロイ**ボックス。

## <a name="build-the-sample-using-visual-studio"></a>Visual Studio を使用してサンプルをビルドします。


Visual Studio での**ビルド**] メニューの [選択**ソリューションのビルド**します。

## <a name="locate-the-built-driver-package"></a>組み込みのドライバー パッケージを見つける


ファイル エクスプ ローラーで、組み込みのドライバー パッケージが含まれているフォルダーに移動します。 たとえば、c:\\SpbAccelerometer\\Win8.1Debug\\パッケージ。

パッケージには、これらのファイルが含まれています。

| ファイル                  | 説明                                                                       |
|-----------------------|-----------------------------------------------------------------------------------|
| SpbSamples.cat        | 署名済みカタログ ファイル全体のパッケージの署名として機能します。      |
| SpbAccelerometer.inf  | ドライバーをインストールするために必要な情報が含まれる情報 (INF) ファイル。 |
| WudfUpdate\_01011.dll | WDF の共同インストーラー。                                                          |
| SpbAccelerometer.dll  | ドライバー ファイルです。                                                                  |



## <a name="alter-the-secondary-system-description-table-ssdt"></a>セカンダリ システムの説明テーブル (SSDT) の変更


1.  x86 バージョンの ASL.exe を Sharks Cove ボードにコピーします。 ASL.exe は、Windows Driver Kit (WDK) で含まれています。

    以下に例を示します。C:\\プログラム ファイル (x86)\\Windows キット\\8.1\\ツール\\x86\\ACPIVerify\\ASL.exe

2.  サメ Cove ボードには、管理者としてコマンド プロンプト ウィンドウを開きます。 次のコマンドを入力して、SSDT を逆コンパイルします。

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

4.  スコープを挿入 (\_SB\_) エントリ。 スコープ エントリ内に、ユーザー独自の Device エントリを挿入します。 スコープを次に示します (\_SB\_) エントリおよび ADXL345 加速度計のデバイス エントリ。

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

    **bcdedit/set TESTSIGNING ON**

2.  Sharks Cove ボードを再起動します。 ボードを再起動するとき、音量を上げるボタンを押したままにします。 **[Device Manager (デバイス マネージャー)] &gt; [System Setup (システム セットアップ)] &gt; [Boot (ブート)]** の順に移動します。 **[UEFI Security Boot (UEFI セキュリティ ブート)]** を **[Disabled (無効)]** に設定します。
3.  変更を保存し、Windows の起動を続けます。


7.  更新された SSDT を読み込むには、管理者としてコマンド プロンプト ウィンドウを開き、次のコマンドを入力します。

    **asl /loadtable ssdt.aml**

    Sharks Cove ボードを再起動します。

## <a name="install-and-run-the-sample-driver"></a>インストールして、ドライバーのサンプルの実行


1.  ホスト コンピューターには、Visual Studio で SpbAccelerometer ソリューションを開きます。
2.  ソリューション エクスプ ローラーでダブルクリック**パッケージ**(小文字) を選択し、**プロパティ**します。 **[Driver Install (ドライバーのインストール)] &gt; [配置]** の順に移動します。 確認**展開を有効にする**します。 **[展開前にドライバーの以前のバージョンを削除する]** チェック ボックスをオンにします。 **ターゲット コンピューター名**、以前にプロビジョニングしたサメ Cove ボードの名前を入力します。 **[Install and Verify (インストールと確認)]** を選びます。 **[OK]** をクリックします。
3.  **デバッグ** メニューの 選択**デバッグの開始**します。 ドライバー パッケージはサメ Cove ボードに自動的にコピーされます。 ドライバーは自動的にインストールされ、読み込まれます。 Windows ユーザー モード デバッガー (Visual Studio でのホスト コンピューターで実行されている) に自動的には、ドライバーをホストしている (サメ Cove ボード上で実行されている) Wudfhost.exe のインスタンスにアタッチします。








