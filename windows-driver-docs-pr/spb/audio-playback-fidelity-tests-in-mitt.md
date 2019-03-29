---
title: MITT でのオーディオ再生の忠実さテスト
description: ミット ボード上のオーディオのモジュールは、(0 個の間) にある正弦波頻度の正確性を検出し、場所、頻度またはオフセットが正しくないインスタンスをカウントして、オーディオ デバイスのトランスポート レベルで発生したエラーを検出するために使用されます。
ms.assetid: 1EAAF6F7-17B6-452F-9273-D7CD1DC33154
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1abc1e6bfc59a5affed22e6104470253a31ce497
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573686"
---
# <a name="audio-playback-fidelity-tests-in-mitt"></a>MITT でのオーディオ再生の忠実さテスト


**最終更新日**

-   2015 年 1 月

**適用対象します。**

-   Windows 8.1

ミット ボード上のオーディオのモジュールは、(0 個の間) にある正弦波頻度の正確性を検出し、場所、頻度またはオフセットが正しくないインスタンスをカウントして、オーディオ デバイスのトランスポート レベルで発生したエラーを検出するために使用されます。 可聴、このメカニズムを使用して自動的に検出可能なシフト波形のシグナルまたは失敗したパケットがないことになります。

## <a name="before-you-begin"></a>開始する前にしています.


-   ミット ボードとオーディオのアダプターを取得します。 参照してください[ミットを使用するためのハードウェアを購入](https://msdn.microsoft.com/library/windows/hardware/dn919811)します。
-   [ミット ソフトウェア パッケージをダウンロード](https://msdn.microsoft.com/library/windows/hardware/dn919810)します。 テスト対象のシステムにインストールします。
-   ミット ボード ミット ファームウェアをインストールします。 参照してください[ミット概要](https://msdn.microsoft.com/library/windows/hardware/dn919779)します。

## <a name="hardware-setup"></a>ハードウェアのセットアップ


![ミット オーディオ テスト ハードウェアの設定](images/mitttoaudio.jpg)

1.  オーディオのアダプターを接続**JC1**ミット ボード。
2.  ライン入力を使用して、1/8"1/8 インチの男性に male ケーブルでテスト対象システムで、オーディオ デバイスからの行からの入力があります。 その他のオーディオ ソースは、適切なケーブルで接続できます。

## <a name="audio-playback-automation-tests"></a>オーディオ再生のオートメーションのテスト


1.  テスト対象システム上のフォルダーを作成します。
2.  ミット ソフトウェア パッケージから AudiounitsimpleIO.dll をフォルダーにコピーします。
3.  このコマンドを使用して、すべてのテストを実行します。

    te.exe audiounitSimpleIO.dll

4.  単純な IO プラグインとして実行し、SimpleIO 付属のスクリプトを使用して、\_ミット\_オーディオ\_Sample.vbs
5.  オーディオ SimpleIO テストの実行を無効にするには、次のレジストリ エントリを設定します。
    -   **HKEY\_CURRENT\_USER\\Software\\Microsoft\\MITT\\AudioUnit** \\**** = RunAudioTest

           データ型  
           REG\_DWORD

           説明  
           0 に設定します。

異常検出の数、一連の 500 hz 18 khz とレポートからのテスト トーンが再生されます。 多数の 10000 + などの問題が検出された場合、ケーブルが正しく接続されていることと、ボリュームがミュートになっていないことを確認します。 中断された信号は数が非常に高くなることができますので、予想される交差ごとの故障で検出されました。

すべてのテストが成功した場合、デバイスは、正しく接続されていると期待どおりに動作が。

 

 




