---
title: Multi Interface Test Tool (MITT) によるテスト
description: ミットは、ハードウェアとソフトウェア UART、I2C、SPI、GPIO などの単純な周辺機器バスを検証するためのテスト ツールです。
ms.assetid: B847568F-4872-4FF7-BB73-E45A6FFF8249
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfd1727293c2758635e07a741327164ca76c2c5d
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391451"
---
# <a name="test-with-multi-interface-test-tool-mitt"></a>Multi Interface Test Tool (MITT) によるテスト


Multi Interface Test Tool (MITT) は、UART、I2C、SPI、GPIO などの SPB (simple peripheral bus) についてハードウェアとソフトウェアを検証するためのテスト ツールです。 MITT には、FPGA 開発ボードが使用されており、ファームウェア、テスト バイナリ、ドライバーを含む、安価なテスト ソリューションを提供するソフトウェア パッケージが組み込まれています。

## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>トピック</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/multi-interface-test-tool--mitt--" data-raw-source="[Buy hardware for using MITT](https://docs.microsoft.com/windows-hardware/drivers/spb/multi-interface-test-tool--mitt--)">ミットを使用するためのハードウェアを購入します。</a></p></td>
<td><p>複数インタ フェース テスト ツール (ミット) を使用して、ミット ボードを作成する必要があるし、バス固有のアダプターでは、そのプラグインをボード ミット ボード上のポートに注文します。 アダプターの掲示板の種類は、テストするバスによって異なります。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/get-started-with-mitt---" data-raw-source="[Get started with MITT](https://docs.microsoft.com/windows-hardware/drivers/spb/get-started-with-mitt---)">ミットを概要します。</a></p></td>
<td><p>ミット テストを実行するには、新しいミット掲示板にミット ファームウェアをインストールする必要があります。 次の手順では、ミット ファームウェアを更新およびミット テストの実行用のホスト コンピューターを準備する方法について説明します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/audio-playback-fidelity-tests-in-mitt" data-raw-source="[Audio playback fidelity tests in MITT](https://docs.microsoft.com/windows-hardware/drivers/spb/audio-playback-fidelity-tests-in-mitt)">ミットでオーディオの再生 fidelity テスト</a></p></td>
<td><p>ミット ボード上のオーディオのモジュールは、(0 個の間) にある正弦波頻度の正確性を検出し、場所、頻度またはオフセットが正しくないインスタンスをカウントして、オーディオ デバイスのトランスポート レベルで発生したエラーを検出するために使用されます。 可聴、このメカニズムを使用して自動的に検出可能なシフト波形のシグナルまたは失敗したパケットがないことになります。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/capacitive-touch-tests-in-mitt" data-raw-source="[Capacitive touch tests in MITT](https://docs.microsoft.com/windows-hardware/drivers/spb/capacitive-touch-tests-in-mitt)">ミットで静電容量方式タッチ テスト</a></p></td>
<td><p>ミット ソフトウェア パッケージの静電容量方式タッチ テストには、MCATT (Microsoft 静電容量方式のアプリケーション テスト ツール) が必要です。 容量ベースのタッチ ハードウェア (タッチパッドやタッチ スクリーンなど) を検証するための自動化ツールになります。 MCATT には MCATT デバイスおよび自動テストのプログラミングの単純なインターフェイスが含まれます。 テストを使用すると、ゴースト ポイントを検出するか、最初のタッチ入力システムのスリープ解除後に反映されるまでに時間テーブルを決定することができます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/gpio-tests-in-mitt" data-raw-source="[GPIO tests in MITT](https://docs.microsoft.com/windows-hardware/drivers/spb/gpio-tests-in-mitt)">ミットで GPIO テスト</a></p></td>
<td><p>ミット ソフトウェア パッケージに含まれている GPIO テスト モジュールを使用して、ダウン、電源、および回転ロックのボリュームを次のボタンのボリュームをテストできます。 これらのテストは、GPIO ドライバーやマイクロ コント ローラーの問題を検出し、短期または長期プッシュするシステムの応答が目的の応答であるかどうかを使用できます。 ボタンにアタッチされている行は、ミット委員会によって低、物理的にプルされます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/run-mitt-tests-for-an-i2c-controller-" data-raw-source="[I2C controller tests in MITT](https://docs.microsoft.com/windows-hardware/drivers/spb/run-mitt-tests-for-an-i2c-controller-)">ミットで I2C コント ローラーのテスト</a></p></td>
<td><p>ミット ソフトウェア パッケージに含まれている I²C テスト モジュールを使用して、I²C のコント ローラーとそのドライバーのデータ転送をテストできます。 ミット ボードは、I²C バスに接続されているクライアント デバイスとして機能します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/spi-tests-in-mitt" data-raw-source="[SPI tests in MITT](https://docs.microsoft.com/windows-hardware/drivers/spb/spi-tests-in-mitt)">ミットで SPI テスト</a></p></td>
<td><p>ミット ソフトウェア パッケージに含まれている SPI テスト モジュールを使用して、SPI コント ローラーとそのドライバーのテスト対象のシステム上のデータ転送をテストできます。 ミット ボードは、SPI バスに接続されているクライアント デバイスとして機能します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/uart-tests-in-mitt" data-raw-source="[UART tests in MITT](https://docs.microsoft.com/windows-hardware/drivers/spb/uart-tests-in-mitt)">ミットで UART テスト</a></p></td>
<td><p>ミット ソフトウェア パッケージには、UART コント ローラーとそのドライバーへのデータ転送を検証するためのテストが含まれています。 ミット board's UART インターフェイスは、UART ループバック デバイスとして機能します。</p></td>
</tr>
</tbody>
</table>

 

 

 




