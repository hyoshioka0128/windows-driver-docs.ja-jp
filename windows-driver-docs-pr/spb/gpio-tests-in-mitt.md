---
title: MITT の GPIO テスト
description: ミット ソフトウェア パッケージに含まれている GPIO テスト モジュールを使用して、ダウン、電源、および回転ロックのボリュームを次のボタンのボリュームをテストできます。
ms.assetid: D50C371B-4A03-4BDD-8EC2-6E7A4A4DF3C5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 327d545f5a1704d0e90b245d5b263fff76fab6b6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356807"
---
# <a name="gpio-tests-in-mitt"></a>MITT の GPIO テスト


**最終更新日**

-   2015 年 1 月

**適用対象:**

-   Windows 8.1

ミット ソフトウェア パッケージに含まれている GPIO テスト モジュールを使用して、ダウン、電源、および回転ロックのボリュームを次のボタンのボリュームをテストできます。 これらのテストは、GPIO ドライバーやマイクロ コント ローラーの問題を検出し、短期または長期プッシュするシステムの応答が目的の応答であるかどうかを使用できます。 ボタンにアタッチされている行は、ミット委員会によって低、物理的にプルされます。

## <a name="before-you-begin"></a>開始する前にしています.


-   ミット ボードと GPIO アダプターのボードを取得します。 参照してください[ミットを使用するためのハードウェアを購入](https://msdn.microsoft.com/library/windows/hardware/dn919811)します。
-   [ミット ソフトウェア パッケージをダウンロード](https://msdn.microsoft.com/library/windows/hardware/dn919810)します。 テスト対象のシステムにインストールします。
-   ミット ボード ミット ファームウェアをインストールします。 参照してください[ミット概要](https://msdn.microsoft.com/library/windows/hardware/dn919779)します。

## <a name="hardware-setup"></a>ハードウェアのセットアップ


![ミット gpio ハードウェアの設定](images/mitttogpio.jpg)

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>バスのインターフェイス</th>
<th>暗証番号 (pin)-不足</th>
<th>ACPI と概略図</th>
<th>接続ソリューション</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>GPIO ボタン</td>
<td>ボタンをクリックし、インジケーター行:ボリューム アップ/スケール ダウン、電源、回転ロック、ラップトップ/スレートのインジケーター、ドック インジケーター</td>
<td>概略図</td>
<td>(デバッグ ボード) 単純な男性のブロック</td>
</tr>
<tr class="even">
<td>GPIO コント ローラー</td>
<td>GPIO コント ローラー pin アウトとインデックスの使用</td>
<td><ul>
<li>GPIO コント ローラーを使用ピン配列の ACPI 名前です。</li>
<li>割り込みコント ローラー (レベルまたはエッジに基づく) でトリガーを起動するタイプ</li>
<li>テスト パス中に無効にすることに GPIO ピン留めを使用してデバイス (指定されている場合) の説明 (その PNP ID を含む)</li>
</ul></td>
<td>(デバッグ ボード) 単純な男性のブロック</td>
</tr>
</tbody>
</table>

 

1.  ミット掲示板、GPIO コネクタを識別します。 左を使用して最も 12-pin ヘッダー、ラベル付け**JA1**、この図のようにします。

    ![ミット ボードの gpio ヘッダー](images/gpioheader.jpg)

2.  接続には、GPIO アダプター ボード、 **JA1**ヘッダー。
3.  3V3 ミット ボードに電源ジャンパーに接続します。
4.  ボードの電源を GPIO ヘッダーの横のスイッチ スライダーにプッシュします。

    ![gpio power 接続](images/gpiopower.png)

5.  テスト対象のシステムに対応するピン GPIO アダプター ボード (、ミットに接続) から (volu) 上のボリューム、ボリューム (vold) ダウン、ドッキングまたはドッキング解除 (ドック) およびスレート/ラップトップ (モード) の行を接続します。

    この図のように、12 pin ヘッダーは、GPIO を 1 行ずつにワイヤード (有線) します。

    ![gpio 配線 ja1 ヘッダー](images/gpiowiring.png)

    出力の概略図は、GPIO ボードにピン留めします。 Pin はスイッチがプッシュされた場合、FET をプルできます行低いようにスイッチを使用して並列に配置する必要があります。

    ![gpio output pin on mitt](images/gpiooutputpin.png)

6.  任意。 ボリュームまたはインジケーターが、両方でミット GPIO テストを実行する場合は、これらのレジストリ エントリを設定して GPIO オートメーションに関連するテストをスキップできます。 各エントリは、DWORD と 1 の値により、テストします。0 は、それを無効にします。
    -   [ボリューム]

        **HKEY\_CURRENT\_USER\\Software\\Microsoft\\MITT\\GPIO\\RunVolumeTest**

    -   インジケーター

        **HKEY\_現在\_ユーザー\\ソフトウェア\\Microsoft\\ミット\\GPIO\\RunIndicatorsTest**

## <a name="run-gpio-automation-tests"></a>GPIO オートメーション テストを実行します。


WDTF を使用して手動で GPIO テストを実行するには、これらのタスクを実行します。

1.  %Programfiles (x86) % ミット ソフトウェア パッケージから mittsimpleioaction.dll にコピー\\Windows キット\\8.1\\テスト\\ランタイム\\WDTF\\ランタイム\\アクション\\SimpleIO
2.  実行 **%programfiles (x86) %\\Windows キット\\8.1\\テスト\\ランタイム\\WDTF\\ランタイム\\UnRegisterWDTF.exe**します。
3.  実行 **%programfiles (x86) %\\Windows キット\\8.1\\テスト\\ランタイム\\WDTF\\ランタイム\\アクション.\\RegisterWDTF.exe/nogacinstall**
4.  SimpleIO を実行して GPIO オートメーション テストを開始\_ミット\_GPIO \_Sample.vbs ミットのソフトウェア パッケージに含まれています。

## <a name="example-custom-gpio-input-injection"></a>以下に例を示します。カスタム GPIO インジェクションの入力


この例では、Example.txt で、シーケンスを 2 秒間の電源ボタンを押すし、ボタンを離しますを含む、ファイルを使用します。 ファイルの内容を次に示します。

``` syntax
‘h001E8480
‘b0000000000011111
‘b0000000100011111
‘b0000000000011111
```

これらのコマンドを実行します。

**Muttutil.exe -SetChannel 00**

**Muttutil.exe -WriteData 0000**

**Muttutill.exe – SetChannel 01**

**Muttutil.exe – WriteDataFromFile Example.txt**

**Muttutil.exe –SetChannel 00**

**Muttutil.exe –Writedata 0001**

-   **SetChannel** 00 コントロール チャネルがデータを受信することを示します。
-   **WriteData**すべてテスト モジュールで 0000 一時停止します。
-   **SetChannel** 01 を指定することで、GPIO チャネルがデータを取得することを示すオプション。
-   **WriteDataFromFile** GPIO モジュールに入力ファイルの例の内容を送信するファイルの名前に置き換えます。
-   **SetChannel**チャネル コントロールに戻るには 00 で、データが表示されます。
-   **WriteData** 0001 GPIO sequencer をアクティブ化する、コントロール チャネルを使用します。 GPIO モジュールには、シーケンス処理が開始します。

## <a name="generate-input-sequences"></a>入力シーケンスを生成します。


シーケンスを生成するには、これらの値が必要です。

-   間隔の値

    間隔の値では、間隔中にどのボタンが押されたかを示すビット マスクです。 ビット マスクの 0 の値は、時間間隔中に、ボタンが押されていないことを示します。 ここで使用可能な値インデックス値はビットです。

    | 16 ビット値のビットのインデックス | テスト対象のシステムでの使用率                      |
    |---------------------------|-----------------------------------------------------|
    | 0                         | 電源ボタンの有効化 (「1」により、出力)        |
    | 1                         | ドッキングのインジケーターを有効にする (「1」により、出力)      |
    | 2                         | ボリュームを有効にする (「1」により、出力)           |
    | 3                         | 回転のロックを有効にする (「1」により、出力)       |
    | 4                         | ボリュームを有効にする (「1」により、出力)         |
    | 5                         | スレート/ラップトップの切り替えを有効にする (「1」により、出力) |
    | 6-7                       | 使用しない                                            |
    | 8                         | 電源ボタンの値 (「1」が押したスイッチ)         |
    | 9                         | インジケーターの値をドッキング (「1」が押したスイッチ)       |
    | 10                        | ボリューム値 (「1」が押したスイッチ)            |
    | 11                        | 回転ロック値 (「1」が押したスイッチ)        |
    | 12                        | 音量下げる値 (「1」が押したスイッチ)          |
    | 13                        | スレート/ラップトップ トグルの値 (「1」が押したスイッチ)  |
    | 14-15                     | 使用しない                                            |

     

-   クロックの乗数

    クロックの乗数は、パターンごとにデータのデータのパターンを次に進む前に (1 つのマイクロ秒単位) で、ボタンのホールド時間です。 GPIO test モジュールは、回線がリセットされるまで、データの最後のパターンを保持します。

    小規模と大規模なクロック乗数を使用するためにトレードオフが発生します。 乗数としてより小さい値には、timespan をカバーするデータのパターンで複数の行を作成する必要があります、複数の有効桁数が使用できます。 データのパターンのファイルを作成するときに必要なデータ パケットとクロックの乗数値の間の適切なバランスを決定する必要があります。

    前の例を使用して入力インジェクション ファイルを作成できます。 入力シーケンスを生成するには、通信プロトコルが必要です。 このパターンでは、テスト対象のシステムにミット ボードから送信されるデータが配置されています。

    ![gpio モジュールの通信プロトコル](images/gpioprotocol.png)

    プロトコル レベルのエラーの GPIO テストの回線でチェックすることはありません。 プロトコル エラーがある場合は、ミットに不明なエラーが表示されます。

## <a name="gpio-adapter-schematic"></a>GPIO アダプターの概略図


![gpio 概略図](images/gpioschematic.png)

## <a name="related-topics"></a>関連トピック
[複数のインターフェイスのテスト ツール (ミット) でのテスト](https://msdn.microsoft.com/library/windows/hardware/dn919874)  



