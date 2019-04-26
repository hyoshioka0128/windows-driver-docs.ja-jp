---
title: センサー ドライバーをインストールします。
description: このトピックでは、開発ボード、センサー ドライバーをインストールする方法を示します。
ms.assetid: 01CC1903-A36B-4ECC-856D-6196EC606973
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cda94f5dc8955bce05a900764d818c967f15779c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345260"
---
# <a name="install-the-sensor-driver"></a>センサー ドライバーをインストールします。


このトピックでは、セカンダリ システムの説明テーブル (SSDT) の開発ボードを更新した後に、開発ボード、センサー ドライバーをインストールする方法を示しています。

このトピックではサメ Cove 開発ボードと ADXL345 加速度計を開発ボード、センサー ドライバーをインストールするプロセスを説明するために、ケース スタディとして使用します。 このトピックで説明するタスクを実行する場合は、サメ Cove でオペレーティング システムをインストールする必要があります。 その方法の詳細については、次を参照してください。 [Windows 10 向けキットとツールをダウンロード](https://docs.microsoft.com/windows-hardware/get-started/adk-install)、Windows 10 をインストールする指示に従います。

サメ Cove を参照してくださいでのオペレーティング システムのインストールが完了したら[センサー ドライバー](build-the-sensor-driver.md)に Microsoft Visual Studio でのドライバーをビルドする方法について説明します。 ここに戻り続行します。

加速度計は、I2C バスを通じてサメ Cove にアタッチされます。 I2C バスに接続されている周辺機器は、Advanced Configuration and Power Interface (ACPI) を使用して列挙されます。 したがって、加速度計のサンプル ドライバーは、プラグ アンド プレイではなく ACPI をサポートするために開発されました。

I2C バス上に新しいデバイス (加速度計) を認識サメ Cove の ACPI ドライバーをさせる、サメ Cove で SSDT を加速度計に関する情報を追加する必要があります。 このテーブルは、ハードウェア リソースとハードウェア プラットフォームのデバイス、加速度計などの周辺の割り込みの要件について説明します。

## <a name="before-you-begin"></a>始める前に


以下に示すタスクの実行を開始する前に、次の図のように、サメ Cove が設定されていることを確認してください。

![サメ cove ボード用の推奨のセットアップ](images/sharkscove-setup.png)

## <a name="retrieve-and-review-the-default-ssdt"></a>取得し、SSDT の既定の確認


このセクションでは、ACPI ソース言語 (ASL) コンパイラを使用して、サメ Cove の SSDT 工場出荷時の既定値を取得し、それを確認する方法を示します。 SSDT の既定値を 1 つずつ更新に置き換える方法も学習します。

1. 開発用コンピューターで ASL コンパイラをコピーする次の場所に移動します: **c:\\Program Files (x86)\\Windows キット\\10\\ツール\\x86\\ACPIVerify**
2. コピー、 *Asl.exe*ファイルを開き、フラッシュ ドライブに保存します。

3. サメ Cove、作成、**ツール**のルート ディレクトリのフォルダー。 サメ Cove の USB ハブ、およびコピーする、フラッシュ ドライブをアタッチ、 *Asl.exe*ファイルを**ツール**フォルダー。

4. 管理者は、コマンド プロンプト ウィンドウを開き、次のコマンドを入力します: **cd\\ツール**
**dir**ことを確認、 *Asl.exe*ディレクトリにファイルが表示されます。

5. ASL コンパイラを起動し、次のコマンドを入力して ASL ファイルを作成します**asl/tab ssdt を =。**
6. 次のコマンドを入力して、ASL ファイルが正常に作成されたことを確認します**dir ssdt.asl。**
7. 次のコマンドを入力してメモ帳で ASL ファイルを開きます:**メモ帳 ssdt.asl** ASL ファイルを確認して、加速度計、または I2C バスへの参照がないことに注意してください。

8. メモ帳を閉じます。 名前を変更する、コマンド プロンプト ウィンドウで、次のコマンドを入力、 *ssdt.asl*ファイル。
**ren ssdt.asl ssdt-old.asl**を使用して、 **dir**コマンドとして、ファイルが現在表示されていることを確認する*ssdt old.asl*します。

## <a name="update-the-default-ssdt"></a>SSDT の既定を更新します。


SSDT を更新する次のタスクを実行し、読み込む工場出荷時の既定のバージョンを置換することです。 最新の SSDT は薬と呼ばれるメモリに格納されます*RAM バッテリ*します。 したがって、サメ Cove に付属するボタン セル (バッテリ使用時) が、ソケットに接続されていることを確認します。

1. 次の更新された SSDT をコピーしてメモ帳の新しいインスタンスに貼り付けます。

    ```cpp
    // CreatorID=INTL  CreatorRev=20.14.805
    // FileLength=177   FileChkSum=0x88
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
        Scope(_SB_)
        {
            Device(SPBA)
            {
                Name(_HID, "ADXL345Acc")
                Name(_UID, 1)
                Method(_CRS, 0x0, NotSerialized)
                {
                    Name(RBUF, ResourceTemplate()
                    {
                        I2CSerialBus(0x53, ControllerInitiated, 400000, 
                            AddressingMode7Bit, "\\_SB.I2C3", 0, ResourceConsumer)
                        GpioInt(Edge, ActiveHigh, Exclusive, PullDown, 0, "\\_SB.GPO2") 
                        {0x17}
                    })
                Return(RBUF)
                }
               Method(_DSM, 0x4, NotSerialized)
               {
                   If(LEqual(Arg0, Buffer(0x10)
                   {
                       0x1e, 0x54, 0x81, 0x76, 0x27, 0x88, 0x39, 0x42, 0x8d, 
                       0x9d, 0x36, 0xbe, 0x7f, 0xe1, 0x25, 0x42
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
    }
    ```

2. メモ帳で、**ファイル** &gt; **付けて**します。 順にクリックして、**型として保存**ドロップダウン ボックス、および選択**すべてのファイル**します。

3. **ファイル名**ボックスに「 *ssdt.asl*、 をクリックしてし、**保存**、メモ帳を閉じます。

4. コマンド プロンプト ウィンドウで実行して、 **dir**コマンドとして表示されます、既定のファイルを表示できることを確認する*ssdt old.asl*ととして一覧表示、新しいファイル*ssdt.asl*します。

5. コンパイル、 *ssdt.asl*サメ Cove は、次のコマンドを入力して理解できる形式にファイル: **asl ssdt.asl**
6. コンパイル済みのファイルがで正常に作成されたことを確認します**手順 3**次のコマンドを入力して: **dir ssdt.aml**表示にする必要があります、 *ssdt.aml*ファイル ツールに一覧表示ディレクトリ。

7. RAM のバッテリ バックアップに、次のコマンドを入力して、コンパイル済みファイルを読み込む: **asl/loadtable ssdt.aml**
## <a name="turn-on-testsigning"></a>Testsigning を有効にします。


サンプル センサー ドライバーをインストールする前に、testsigning をオンする必要があります。 Testsigning を有効にする、次のタスクを実行します。 次の手順を使用してセンサー ドライバーをインストールする実行**デバイス マネージャー**します。

1. コマンド プロンプト ウィンドウで、testsigning をまだオンにするかどうかを確認するには、次のコマンドを入力します。<br/>
**bcdedit/enum**
2. Testsigning、エントリを表示、次のような一覧を表示する場合は、その値を設定して`yes`にスキップ**手順 5**します。<br/>
![コマンド プロンプト ウィンドウが testsigning を [はい] に設定を表示します。](images/testsigning.png)

3. テスト署名を有効にする必要がある場合、次のコマンドを入力してください: **bcdedit に testsigning を設定/**

4. 繰り返します**手順 1** (この演習では) では、testsigning システム変数の値は、Windows ブート ローダーの一覧で [はい] に設定されたことを確認します。

5. サメ Cove を再起動します。 ボードの再起動時には、約 2 秒間ボリュームをボタンを押したまま、システムのセットアップ (UEFI) ウィンドウに入力します。

6. UEFI ウィンドウで、次のように選択します**デバイス マネージャー** &gt; **システム セットアップ** &gt; **ブート**、ことを確認および**UEFI セキュリティ ブート。** に設定されている**&lt;を無効にする&gt;** します。

7. 変更を保存し、UEFI ウィンドウを終了します。

## <a name="install-the-sensor-driver"></a>センサー ドライバーをインストールします。


サメ Cove ボード上のドライバーをインストールするための 4 つの主な方法はあります。

-   サメ Cove に直接ネットワーク ソースからドライバーをダウンロードします。
-   プロビジョニング済みのクライアントとして接続して、サメ Cove で、ホスト コンピューター上のセンサー ドライバーを開発します。 次にサメ Cove ホスト コンピューターからドライバーを展開します。
-   フラッシュ ドライブにドライバー パッケージをコピーし、サメ Cove にフラッシュ ドライブをアタッチします。 使用して、 **devcon**ドライバーを手動でインストールするコマンド プロンプト ウィンドウからコマンド。
-   フラッシュ ドライブにドライバー パッケージをコピーし、サメ Cove にフラッシュ ドライブをアタッチします。 使用して手動でドライバーをインストールし、**デバイス マネージャー**します。

わかりやすくするためは、上記の一覧で、最後のメソッドを使用します。 次の手順を使用してセンサー ドライバーを手動でインストールする実行**デバイス マネージャー**します。

センサー ドライバーをインストールする前に、サメ Cove にセンサーを接続する必要があります。 SparkFun から ADXL345 加速度計のブレイク アウト ボードを変更する方法については、サンプル センサー ドライバーと連動するようを参照してください[センサー テスト ボードの準備](prepare-your-sensor-test-board.md)します。 サメ Cove にセンサーのブレイク アウト ボードを接続する方法については、次を参照してください。 および[サメ Cove 掲示板にセンサーを接続](connect-your-sensor-to-the-sharks-cove-board.md)します。

1. サメ Cove J1C1 コネクタ、サメ Cove の電源をオンし ADXL345 加速度計が接続されていることを確認します。

2. センサー ドライバーをフラッシュ ドライブをサメ Cove に接続されている電源の USB ハブに接続します。 たとえば、次の手順で作成したドライバーの保存先となる、フラッシュ ドライブをられます[センサー ドライバー](build-the-sensor-driver.md)します。

3. 開いている**デバイス マネージャー**、「不明なデバイス」内で検索し、**他のデバイス**ノード黄色い感嘆符シンボルに対して (次のスクリーン ショットを参照してください)。<br/>![デバイス マネージャーのスクリーン ショットに黄色の感嘆符に不明なデバイスを示します。](images/dev-manager.png)

4. (不明なデバイスとして表示)、黄色の感嘆符でデバイスを右クリックして**ドライバー ソフトウェアの更新**、 をクリック**参照コンピューターでドライバー ソフトウェア**します。

5. ADXL345 ドライバー、フラッシュ ドライブ上に移動し、をクリックして**次**します。 センサー ドライバーをインストールする画面の指示に従います。

6. サンプル センサー ドライバーが正常にインストールされると、**デバイス マネージャー**の次のスクリーン ショットに示すように、センサーを表示します。<br/>![デバイス マネージャーのスクリーン ショット、正常にインストールされている adxl345 加速度計に対してデバイス ノードの表示](images/dev-mgr-sensors.png)

Visual Studio を使用して (サメ Cove) などのクライアント コンピューターにドライバーを展開する方法については、次を参照してください。[テスト コンピューターにドライバーを展開する](https://docs.microsoft.com/windows-hardware/drivers/develop/deploying-a-driver-to-a-test-computer)します。

センサー ドライバーのサンプルを正常にインストールした後、次を参照してください。[ユニバーサル センサー ドライバーをテストして](test-your-universal-sensor-driver.md)センサーをテストする方法についてはします。

 

 




