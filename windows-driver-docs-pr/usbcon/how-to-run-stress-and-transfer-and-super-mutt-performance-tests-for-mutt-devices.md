---
Description: ストレスおよび転送とスーパー MUTT パフォーマンスを実行する方法をテストします。
title: MUTT デバイスのストレスおよび転送パフォーマンステストの実行方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d254c6e79297fa8ede9d4d7718afda88e3f03296
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366041"
---
# <a name="how-to-run-stress-and-transfer-performance-tests-for-mutt-devices"></a>MUTT デバイスのストレスおよび転送パフォーマンステストの実行方法


ストレスおよび転送とスーパー MUTT パフォーマンスを実行する方法を参照してテストします。

ストレスおよび転送テストは、bus プロトコルとホスト コント ローラーのソフトウェアの飽和に特化しました。 これらのテストでは、いくつかの同時転送の I/O と MUTT デバイスに取り消しを実行します。 MUTT ファームウェアは、これらのテストの転送が失敗するプログラミングされます。 このようなエラーがエラーをエミュレートする条件をコント ローラーまたは USB ドライバー スタックに USB のストレス条件下で公開されます。

## <a name="how-to-run-stress-and-transfer-tests"></a>テストをストレスおよび転送を実行する方法


1.  使用可能なポートに接続された MUTT デバイスをされているテスト システムの管理者特権のコマンド ウィンドウを開きます。
2.  など、テスト フォルダーに移動します**c:\\モジュールとしても**します。
3.  転送やストレス テストは、同じスクリプトを使用して実行します。 を実行するには、スクリプト runtest.bat を実行します。

    **C:\\usbTest\\runtest.bat**

書き込まれると、.bat ファイルでは、テストを無期限に実行されます。 このテストは、少なくとも 30 分間実行する必要があります。 もっと徹底したテストでは、8 時間のこれらのテストの実行を検討してください。 バッチ ファイルには、実行できる追加の調整のコメントが含まれています。

すべてのテストを終了するキーを押して**Ctrl + C**コマンド ウィンドウにします。 システムが実行し、コマンド ウィンドウから正常に終了時にバグチェックを生成しない場合、テストの実行が成功したと見なされます (または正の実行)。 ツールが正常に終了しない場合が示されます転送が完了していないと、調査する必要があります。

## <a href="" id="supermutt-perf"></a>SuperMUTT パフォーマンス テストを実行する方法


1.  XHCI コント ローラーに接続されている SuperMUTT をされているテスト システムの管理者特権のコマンド ウィンドウを開きます。
2.  など、テスト フォルダーに移動します**c:\\モジュールとしても**します。
3.  という名前のスクリプトを実行**FX3Perf.bat**テストの実行を開始します。

## <a name="related-topics"></a>関連トピック
[USB](https://msdn.microsoft.com/library/windows/hardware/ff538930)  
[Microsoft USB Test Tool (MUTT) デバイス](microsoft-usb-test-tool--mutt--devices.md)  



