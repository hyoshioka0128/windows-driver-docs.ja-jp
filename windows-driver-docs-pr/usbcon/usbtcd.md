---
Description: USBTCD は、ユーザー モード アプリケーションとカーネル モード ドライバーの組み合わせです。
title: USBTCD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d8e248fed9356c98e46843caed4f538cfaf3faa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333946"
---
# <a name="usbtcd"></a>USBTCD


USBTCD は、ユーザー モード アプリケーションとカーネル モード ドライバーの組み合わせです。 ツールを実行します。 読み取りおよび書き込み操作です。 さまざまな転送の長さにし、テスト デバイスからの一括、アイソクロナス、データ転送、コントロールを開始します。 SuperMUTT デバイスの場合は、USBTCD は、一括エンドポイントでサポートされているストリームにデータを転送します。 転送バッファー連鎖 MDLs としても送信できます。 その場合は、転送バッファー内のセグメントの数を指定できます。

含まれる USBTCD ファイル、 [MUTT ソフトウェア パッケージ](https://msdn.microsoft.com/windows/hardware/jj590752)します。

## <a name="usbtcd"></a>USBTCD


これらのコマンドを使用するには、デバイスの機能のドライバーとして USBTCD ドライバー (USBTCD.sys) を読み込む必要があります。 デバイスのドライバーを読み込むには、MUTTUtil を実行し、指定**USBTCD.inf**します。 このツールで読み込む**USBTCD.sys**接続されているすべての USB デバイス用です。

``` syntax
c:\Program Files (x86)\USBTest\x64>MuttUtil.exe -UpdateDriver usbtcd.inf
Return value: 0


c:\Program Files (x86)\USBTest\x64>MuttUtil.exe -list
       :    : HARDWARE ID                    :  PROBLEM CODE  : DRIVER
DEVICE :  0 : USB\VID_045E&PID_078E&REV_8011 :             0  : USBTCD
Return value: 1
```

SuperMUTT デバイスの一括エンドポイントと転送のパフォーマンスを測定するのに、次のコマンドを使用することができます。

**Usbtcd – パフォーマンス – 1 を読み取る 100 2 10240000 0**

**Usbtcd – パフォーマンス – 1 を書き込む 100 0 10240000 0**

上記のコマンドでは、USBTCD はパイプ 2 から 10240000 を読み取ります。 2 番目のコマンドでは、USBTCD は、書き込み操作に対し、10240000 が 0 のパイプに送信される場所を開始します。 どちらのコマンドについては、このツールは、100 回の操作を実行し、タイムアウト値を指定しません。

これらのコマンドは、MUTT デバイスの一括エンドポイントのパフォーマンスを測定に使用されます。 転送サイズはここで減少することに注意してください。

**Usbtcd – パフォーマンス – 1 を読み取る 100 2 512000 0**

**Usbtcd – パフォーマンス – 1 を書き込む 100 0 512000 0**

これらのコマンドは、SuperMUTT デバイスの一括エンドポイントのストリームへのデータ転送のパフォーマンスを測定します。 現時点では、デバイスのファームウェアがストリームを切り替えようとホストに新しいストリーム数と共に、ERDY を送信するミリ秒単位。 デバイス内で、タイマーと共に実装されています。

**Usbtcd – sread 1 100 7 1 1024 0**

**1 の Usbtcd – 校閲スペルチェッカー 100 6 1 1024 0**

上記のコマンド、USBTCD 読み取りと SuperMUTT デバイスの一括エンドポイントで特定のストリームに書き込みます。 最初のコマンドでは、ツールは、パイプ 7 に関連付けられている 1 のストリームから 1024 バイトを読み取り、ワーカー スレッドを開始します。 同様に、2 番目のコマンドは、パイプ 6 に関連付けられている 1 をストリーミングする 1024 バイトを書き込みます。 どちらのコマンドについては、このツールは、100 回の操作を実行し、タイムアウト値を指定しません。

USBTCD でヘルプを表示するには、次のコマンドを実行します。

**usbtcd -?**

コマンドは、コマンド ライン オプションに関する情報を表示します。 転送サイズ、冗長性、転送タイムアウト、およびコマンドラインで指定できます。

## <a name="related-topics"></a>関連トピック
[USB テスト ツール](usb-test-tools.md)  
[MUTT ソフトウェア パッケージのツール](mutt-software-package.md)  
[Microsoft USB Test Tool (MUTT) デバイス](microsoft-usb-test-tool--mutt--devices.md)  



