---
title: Sharks Cove ハードウェア開発ボード
description: Sharks Cove は、Windows 向けのハードウェアやドライバーの開発に使うことができるハードウェア開発ボードです
ms.assetid: D86546BB-B613-4CEE-9A76-3FD269137EE9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 459802c7686ac0fd9cfdd06f107c89724c6af86d
ms.sourcegitcommit: 1d531bf9d02653fdf9ad728126d68b8acb86182e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87402269"
---
# <a name="sharks-cove-hardware-development-board"></a>Sharks Cove ハードウェア開発ボード

> [!WARNING]
> Sharks Cove ハードウェア開発ボードは、Windows IoT Core ではサポートされなくなっています。  現在サポートされているボードの一覧については、「[SoCs and custom boards (SoC とカスタム ボード)](https://docs.microsoft.com/windows/iot-core/learn-about-hardware/socsandcustomboards)」をご覧ください。

Sharks Cove は、Windows 向けのハードウェアやドライバーの開発に使うことができる[ハードウェア開発ボード](https://go.microsoft.com/fwlink/p?linkid=506967)です

Intel Sharks Cove ボードは、さまざまなインターフェイス (GPIO、I2C、I2S、UART、SDIO、USB など) を使うデバイス用のドライバーの開発をサポートします。 Sharks Cove ボードを使って、カメラやタッチ スクリーン用のドライバーを開発することもできます。

Sharks Cove ボードに関連するダウンロードについては、[Sharks Cove の UEFI ファームウェアに関するページ](https://go.microsoft.com/fwlink/p?linkid=403167)をご覧ください。

詳細な仕様については、[Sharks Cove の技術仕様に関するページ](https://go.microsoft.com/fwlink/p?linkid=403169)をご覧ください。

## <a name="before-you-start"></a>開始する前に

ここで説明する手順を実行するには、Windows 10、Windows 8.1、または Windows 7 を実行している必要があります。 これらの手順は、Windows 8 を実行している場合は使用できません。

Windows 7 を実行している場合は、[PowerShell 4.0](https://go.microsoft.com/fwlink/p?linkid=507377) と [Windows 8.1 Update 用 Windows アセスメント & デプロイメント キット (ADK)](https://go.microsoft.com/fwlink/p/?linkid=239721) をインストールする必要があります。 その後で、 **[スタート]** メニューから、 **[すべてのプログラム] &gt; [Windows キット] &gt; [Windows ADK] &gt; [展開およびイメージング ツール環境]** の順にクリックします。 このコマンド プロンプト ウィンドウを管理者として開きます。 以下の各手順で説明するコマンドを入力するときは、このコマンド プロンプト ウィンドウを使います。

## <a name="step-1-get-the-board-and-related-hardware"></a>手順 1:ボードおよび関連するハードウェアを入手する

次のハードウェアが必要です。

- 電源コードとアダプターが付属する Sharks Cove ボード
- USB ハブ
- USB キーボード
- USB マウス
- USB ネットワーク アダプター
- モニターおよび HDMI ケーブル (場合によってはアダプターも必要)

Sharks Cove ボードは、[Mouser Electronics](https://go.microsoft.com/fwlink/p?linkid=403172) で入手できます。

## <a name="step-2-download-kits-and-tools"></a>手順 2:キットとツールのダウンロード

ドライバー開発環境には、*ホスト コンピューター*と*ターゲット コンピューター*という、2 台のコンピューターがあります。 ターゲット コンピューターは*テスト コンピューター*とも呼ばれます。 ドライバーの開発とビルドは、ホスト コンピューター上の Microsoft Visual Studio で行います。 デバッガーはホスト コンピューター上で実行され、Visual Studio のユーザー インターフェイスで利用できます。 ドライバーのテストとデバッグを行うときは、ドライバーをターゲット コンピューター上で実行します。 この場合、Sharks Cove ボードがターゲット コンピューターになります。

Sharks Cove ボードでハードウェアとドライバーを開発するには、次のキットとツールをホスト コンピューターにインストールする必要があります。

- [Visual Studio](https://go.microsoft.com/fwlink/p/?LinkId=533470)
- [Windows Driver Kit (WDK)、WDK Test Pack、Debugging Tools for Windows](https://go.microsoft.com/fwlink/p/?LinkId=733614)

ホスト コンピューターで、最初に Visual Studio をダウンロードし、次に WDK をダウンロードしてから、WDK Test Pack をダウンロードします。 Debugging Tools for Windows は WDK に含まれているため、別個にダウンロードする必要はありません。

### <a name="documentation"></a>ドキュメント

- [WDK のオンライン ドキュメント](https://go.microsoft.com/fwlink/p?linkid=317001)。

- [Debugging Tools for Windows のオンライン ドキュメント](https://go.microsoft.com/fwlink/p?linkid=223405)。

- Debugging Tools for Windows のドキュメントは、インストール ディレクトリに CHM ファイルとしても保存されています 例:C:\\Program Files (x86)\\Windows Kits\\10\\Debuggers\\x64\\debugger.chm

## <a name="step-3-install-windows-on-the-sharks-cove-board"></a>手順 3:Sharks Cove ボードに Windows をインストールする

次のいずれかのバージョンの Windows を Sharks Cove ボードにインストールできます。

|用語|説明|
|----|----|
|Windows Embedded 8.1 Industry Pro Evaluation|これは、180 日間無料の試用版です。 これは、評価版として扱われます。|
|Windows Embedded 8.1 Industry Pro with Update (x86) - DVD|これには、サブスクリプションが必要です。 これは、通常版として扱われます。|

評価版をインストールする場合は、使用許諾契約に対する次の修正をお読みください。

### <a name="evaluation-software-license-terms-amendment-for-the-hardware-developer-program"></a>評価版ソフトウェア ライセンス条項に関する修正 (ハードウェア開発者プログラム向け)

このソフトウェアの使用がハードウェア開発者プログラムをサポートする場合は、次の条項が適用されます。

- Windows Embedded 8.1 Industry Pro に関する Microsoft 評価版ソフトウェアのライセンス条項 (評価版ソフトウェア ライセンス条項) の、以下を除くすべての条項に同意するものとします。
  - 評価版ソフトウェア ライセンス条項の 1.b 項 (デモンストレーションの権利) の一部が次のように修正されました。
        -   ソフトウェアを使って開発された Windows Embedded 8.1 Industry Pro デバイス ("デモンストレーション デバイス") を、デモンストレーションの目的で合理的に必要となる数だけ使い、潜在的なユーザーに対してデモンストレーションを行ったり、デモンストレーションで使うために潜在的なユーザーに提供したりすることができます。 守秘義務の対象ではないユーザーに対して、デモンストレーション デバイスのデモンストレーションを行ったり、提供したりすることができます。
  - 上記の修正条項に直接抵触しない、1.b 項の条項は すべて適用されます。
- **本ソフトウェアを使用することにより、お客様は本ライセンス条項に同意されたものとします。** これらの条項に同意せず従わない場合は、ソフトウェアおよびその機能を使うことができないものとします。

[Windows Embedded 8.1 Industry (x86) Pro Evaluation](https://go.microsoft.com/fwlink/p?linkid=403173) または Windows Embedded 8.1 Industry Pro Update (x86) - DVD をダウンロードします。
ダウンロードしたファイルを探します。 たとえば、

9600.17050.WINBLUE\_REFRESH...X86FRE\_EN-US\_DV9.ISO

Sharks Cove セットアップ ファイルのルートとなるフォルダーを作成します (例: C:\\SharksCoveWindows)。 このフォルダーを *Root* と呼びます。 *Root* 内に、次のサブフォルダーを作ります。

- セットアップ
- SharksCoveBsp

ISO ファイルをダブルクリックして、次のファイルを *Root*\\Setup にコピーします。

- Boot
- Efi
- ソース
- サポート
- Autorun.inf
- Bootmgr
- Bootmgr.efi
- Setup.exe

>[!NOTE]
>Windows 7 を実行している場合は、ISO ファイルを右クリックして、 **[ディスク イメージの書き込み]** をクリックします。 イメージを書き込み可能 DVD に書き込みます。 次に、ファイルを DVD から *Root*\\Setup にコピーします。

[Sharks Cove ボードのサポート パッケージ (BSP)](https://go.microsoft.com/fwlink/p?linkid=506954) を入手します。 パッケージに含まれるすべてのファイルを *Root*\\SharksCoveBsp にコピーします。

[WDK Development Boards Add-on Kit](https://go.microsoft.com/fwlink/p/?linkid=403174) を入手します。 **[SourceCode (ソースコード)]** タブを開きます。[Downloads (ダウンロード)] タブではなく、 **[Download (ダウンロード)]** をクリックして、キット スクリプトを入手します。 Scripts フォルダーを開き、次の 2 つの項目を *Root* にコピーします。

- Create-DevboardImage.ps1
- DevBoard フォルダー

>[!NOTE]
>DevBoard フォルダーには、複数のスクリプトとモジュールが含まれます (DevboardImage.ps1、Devboard.psm1、enable-telnet.ps1 など)。

管理者としてコマンド プロンプト ウィンドウを開き、「**Powershell**」と入力します。 *Root* に移動します。 BSP を Windows イメージに追加するには、次のいずれかのコマンドを入力します。

Windows の評価版を使っている場合は、次のコマンドを入力します。

``` syntax
.\Create-DevboardImage -SourcePath Setup\sources\install.wim -Index 2 -BspManifest SharksCoveBsp\SharksCoveBsp.xml
```

Windows の通常版を使っている場合は、次のコマンドを入力します。

``` syntax
.\Create-DevboardImage -SourcePath Setup\sources\install.wim -Index 1 -BspManifest SharksCoveBsp\SharksCoveBsp.xml
```

**注** **Create-DevboardImage** スクリプトを実行する前に、実行ポリシーの設定が必要になる場合があります。 たとえば、次のように入力します。

``` syntax
Set-ExecutionPolicy -ExecutionPolicy Unrestricted
```

BSP が Windows イメージに追加されたので、次のフォルダーとファイルを、*Root*\\Setup から USB フラッシュ ドライブ (FAT32) にコピーします。

- Boot
- Efi
- ソース
- サポート
- Autorun.inf
- Bootmgr
- Bootmgr.efi
- Setup.exe

次に示すように Sharks Cove ハードウェアをセットアップします。

![ボードと接続の画像](images/sharkscoveconnections03.png)

フラッシュ ドライブを、Sharks Cove ボードに接続されているハブに接続します。 Sharks Cove ボードの起動時または再起動時には、音量を上げるボタンを押したままにしておきます。 音量を上げるボタンは、ボードの左側にある 3 つのボタンのセットの一番上にあります。上の図をご覧ください (ボードが既に起動されている場合は、電源ボタンを数秒間押し続けることで、ボードを停止できます)。ボードが起動すると、画面に EFI シェルが表示されます。

>[!NOTE]
>場合によっては、EFI シェルに移動する必要があります。 その場合は、 **[Boot Manager (ブート マネージャー)] &gt; [EFI Internal Shell (EFI 内部シェル)]** に移動します

USB フラッシュ ドライブの名前 (**fs1**: など) を覚えておきます。

(ここでは、USB フラッシュ ドライブの名前に **fs1**: を使います。)**Shell&gt;** プロンプトで、次のコマンドを入力します。

**fs1:** 
**cd efi\\boot**
**dir** bootia32.efi がディレクトリにあることを確認します。 次のコマンドを入力します。

**bootia32.efi** 画面に示される Windows セットアップの指示に従います。

## <a name="step-4-provision-the-sharks-cove-board-for-driver-deployment-and-testing"></a>手順 4:ドライバーの展開とテストのために Sharks Cove ボードをプロビジョニングする

"*プロビジョニング*" は、自動ドライバー展開、テスト、デバッグ用にコンピューターを構成するプロセスです。

次に示すようにハードウェアをセットアップします。

![プロビジョニング用の接続を行ったボードの画像](images/sharkscoveconnections02.png)

Sharks Cove ボードのプロビジョニングは、他のコンピューターのプロビジョニングと似ています。 Sharks Cove ボードをプロビジョニングするには、次トピックの手順に従ってください。

- [ドライバーの展開およびテストのためのコンピューターのプロビジョニング (WDK 8.1)](provision-a-target-computer-wdk-8-1.md)

また、次のトピックの手順にも従ってください。このトピックはオンライン ドキュメントまたは debugger.chm で確認できます。

- [Visual Studio での USB 経由のシリアル接続を使ったカーネル モード デバッグの設定](https://go.microsoft.com/fwlink/p?linkid=400460)

>[!NOTE]
>Sharks Cove ボードをプロビジョニングする前に、セキュア ブートを無効にする必要があります。 Sharks Cove ボードを再起動します。 ボードを再起動するとき、音量を上げるボタンを押したままにします。 **[Device Manager (デバイス マネージャー)] &gt; [System Setup (システム セットアップ)] &gt; [Boot (ブート)]** の順に移動します。 **[UEFI Security Boot (UEFI セキュリティ ブート)]** を **[Disabled (無効)]** に設定します。

## <a name="step-5-write-a-software-driver-for-the-sharks-cove-board"></a>手順 5:Sharks Cove ボードでソフトウェア ドライバーを作成する

Sharks Cove ボードでデバイス ドライバーを作る前に、ソフトウェア ドライバーを作って、ドライバー開発ツールについて理解しておくことをお勧めします。 その手順は、他のターゲット コンピューターでのソフトウェア ドライバーの作成に似ています。 最初に、次の実践的な演習を行ってください。

- [初めてのドライバーの作成](writing-your-first-driver.md)

## <a name="step-6-alter-the-secondary-system-description-table-ssdt"></a>手順 6:Secondary System Description Table (SSDT) を変更する

Sharks Cove ボード上の Simple Peripheral Bus (SPB) に接続されるデバイスのドライバーを作る場合は、Sharks Cove ファームウェアの Secondary System Description Table (SSDT) を更新する必要があります。 このようなドライバーの作成の例として、I2C バス経由でデータを転送し、汎用 I/O (GPIO) ピンを介して割り込みを生成する加速度計のドライバーの作成が挙げられます。 詳しくは、[Simple Peripheral Bus に関するページ](https://go.microsoft.com/fwlink/p?linkid=399232)をご覧ください。

SSDT の変更例を次に示します。 ここでは、[ADXL345](https://go.microsoft.com/fwlink/p?linkid=401463) 加速度計のテーブル エントリを追加します。

>[!NOTE]
>[SpbAccelerometer サンプル ドライバー](https://go.microsoft.com/fwlink/p?linkid=506965)と ADXL345 加速度計の手順ガイドについては、「[SpbAccelerometer ドライバー クックブック](https://docs.microsoft.com/windows-hardware/drivers/sensors/spbaccelerometer-driver-cookbook)」をご覧ください。

1. x86 バージョンの ASL.exe を Sharks Cove ボードにコピーします。 ASL.exe は WDK に付属しています。

    例:C:\\Program Files (x86)\\Windows Kits\\8.1\\Tools\\x86\\ACPIVerify\\ASL.exe

2. 管理者としてコマンド プロンプト ウィンドウを開きます。 次のコマンドを入力して、SSDT を逆コンパイルします。

    **asl /tab=ssdt**

    このコマンドによって Ssdt.asl が作成されます。

3. Ssdt.asl をメモ帳などで開きます。

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

4. Scope(\_SB\_) エントリを挿入します。 スコープ エントリ内に、ユーザー独自の Device エントリを挿入します。 ADXL345 加速度計の Scope(\_SB\_) エントリと Device エントリの例を次に示します。

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

1. 管理者としてコマンド プロンプト ウィンドウを開き、次のコマンドを入力します。

    **bcdedit /set TESTSIGNING ON**

2. Sharks Cove ボードを再起動します。 ボードを再起動するとき、音量を上げるボタンを押したままにします。 **[Device Manager (デバイス マネージャー)] &gt; [System Setup (システム セットアップ)] &gt; [Boot (ブート)]** の順に移動します。 **[UEFI Security Boot (UEFI セキュリティ ブート)]** を **[Disabled (無効)]** に設定します。
3. 変更を保存し、Windows の起動を続けます。

4. 更新された SSDT を読み込むには、管理者としてコマンド プロンプト ウィンドウを開き、次のコマンドを入力します。

    **asl /loadtable ssdt.aml**

    Sharks Cove ボードを再起動します。

## <a name="step-7-connect-your-device-to-the-sharks-cove-board"></a>手順 7:デバイスを Sharks Cove ボードに接続する

[Sharks Cove ヘッダーとピンの仕様](https://go.microsoft.com/fwlink/p?linkid=506966)を入手します。

その仕様を参照して、デバイスで使うピンを特定します。 たとえば、ADXL345 加速度計を I2C バスに接続するとします。 仕様では、J1C1 ヘッダーが必要なピンを保持していることを確認できます。 次に、J1C1 ヘッダーで使うピンの一部を示しますが、これがすべてではありません。

| Pin | ピンの名前        | 備考                            | ACPI オブジェクト      |
|-----|-----------------|-------------------------------------|------------------|
| 7   | GPIO\_S5\[23\]  | 加速度計割り込みのシグナル      | \_SB.GPO2 {0x17} |
| 13  | SIO\_I2C2\_DATA | I2C コント ローラー 2 の I2C データ ライン  | \_SB.I2C3        |
| 15  | SIO\_I2C2\_CLK  | I2C コント ローラー 2 の I2C クロック ライン | \_SB.I2C3        |

SSDT での Device エントリとの関係に注目してください。

``` syntax
I2CSerialBus(... "\\_SB.I2C3", , )
GpioInt(... "\\_SB.GPO2") {0x17}
```

## <a name="step-8-write-build-and-deploy-a-driver-for-your-device"></a>手順 8:デバイス ドライバーの作成、ビルド、展開を行う

Sharks Cove ボードでのデバイス ドライバーの作成は、他のコンピューターでのデバイス ドライバーの作成に似ています。 Visual Studio で、ドライバー テンプレートを使って作業を始めるか、ドライバー サンプルを使って作業を始めます。

Sharks Cove ボードでドライバーをテストする準備ができたら、次の手順を実行します。

1. ホスト コンピューターの Visual Studio で、パッケージ プロジェクトを右クリックし、 **[プロパティ]** をクリックします。 **[Driver Install (ドライバーのインストール)] &gt; [配置]** の順に移動します。 **[配置を有効にする]** および **[Remove previous driver versions before deployment (配置前にドライバーの以前のバージョンを削除する)]** をオンにします。 **[ターゲット コンピューター名]** で、Sharks Cove ボードの名前を選びます。 **[Install and Verify (インストールと確認)]** を選びます。
2. プロパティ ページで、 **[Driver Signing (ドライバーの署名)] &gt; [全般]** の順に移動します。 **[Sign Mode (署名モード)]** で、 **[Test Sign (テスト署名)]** を選びます。 **[OK]** をクリックします。
3. ドライバー プロジェクトで、INF ファイルを開きます。 SSDT で作成したハードウェア ID (\_HID) に一致するように、ハードウェア ID を編集します。 たとえば、次の Device エントリを SSDT に指定したとします。

    ``` syntax
    Device(SPBA)
    {
       Name(_HID, "SpbAccelerometer")
       ...
    ```

    この場合、INF ファイルのハードウェア ID は ACPI\\SpbAccelerometer になります。

    ``` syntax
    [Standard.NT$ARCH$]
    %KMDFDriver1.DeviceDesc%=KMDFDriver1_Device, ACPI\SpbAccelerometer
    ```

4. Visual Studio で、 **[デバッグ]** メニューの **[デバッグの開始]** を選びます。
5. Microsoft Visual Studio ではまず、 **[出力]** ウィンドウに進行状況が表示されます。 次に、**デバッガーのイミディエイト ウィンドウ**が開き、引き続き進行状況が表示されます。

    ドライバーが Sharks Cove ボードに展開、インストールされ、読み込まれるまで待機します。 この処理は、1 ～ 2 分かかる場合があります。

6. デバッガーが自動的に中断しない場合は、 **[デバッグ]** メニューの **[すべて中断]** をクリックします。 ホスト コンピューター上のデバッガーが、ターゲット コンピューターへの割り込みを行うか (カーネル モード)、Wudfhost.exe の適切なインスタンスへの割り込みを行います (UMDF)。 **デバッガーのイミディエイト ウィンドウ**に、デバッガーのコマンド プロンプトが表示されます。

7. 読み込まれたモジュールを表示するには、「**lm**」と入力します。 ドライバーが、読み込まれたモジュールの一覧に表示されることを確認します。

## <a name="using-windbg-to-debug-the-sharks-cove-board"></a>WinDbg を使った Sharks Cove ボードのデバッグ

Visual Studio を使ってカーネル モード デバッグをセットアップするのではなく、手動でセットアップすることができます。 次のトピックはオンライン ドキュメントまたは debugger.chm で確認できます。

- [USB 経由のシリアル接続を使用してカーネル モード デバッグを手動でセットアップする](https://go.microsoft.com/fwlink/p?linkid=400461)

デバッグで Visual Studio を使う代わりに、WinDbg を使うことができます。

Visual Studio を使う場合でも、WinDbg を使う場合でも、デバッガー コマンドについて学習する際は、次の実践的なガイドが役立ちます。

- [WinDbg ドライバーの概要 (ユーザー モード)](https://docs.microsoft.com/windows-hardware/drivers/debugger/getting-started-with-windbg)
- [WinDbg ドライバーの概要 (カーネル モード)](https://docs.microsoft.com/windows-hardware/drivers/debugger/getting-started-with-windbg--kernel-mode-)

## <a name="sample-driver-code"></a>サンプルのドライバー コード

- [SpbAccelerometer サンプル ドライバー (UMDF バージョン 1)](https://go.microsoft.com/fwlink/p?linkid=506965)

## <a name="understanding-simple-peripheral-buses"></a>Simple Peripheral Bus について

Windows ドライバーでの Simple Peripheral Bus の操作方法については、「[Simple Peripheral Bus](https://go.microsoft.com/fwlink/p?linkid=399232)」をご覧ください。

## <a name="related-topics"></a>関連トピック

[すべてのドライバー開発者のための概念](https://go.microsoft.com/fwlink/p/?linkid=399233)

[ドライバーの開発、テスト、および展開](https://go.microsoft.com/fwlink/p/?linkid=399234)

[Windows Driver Framework](https://go.microsoft.com/fwlink/p/?linkid=399235)

[Windows ハードウェア デベロッパー センター](https://go.microsoft.com/fwlink/p/?linkid=8703)

[Windows 向けの WDK サンプル](https://go.microsoft.com/fwlink/p?linkid=394031)

[Windows ハードウェアとドライバー開発者のコミュニティ](https://go.microsoft.com/fwlink/p?linkid=393983)

[テクニカル サポート](https://go.microsoft.com/fwlink/p/?linkid=8713)
