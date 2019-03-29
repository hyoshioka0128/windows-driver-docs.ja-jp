---
title: Bluetooth Inquiry Record Verifier
description: Bluetooth の照会のレコードの検証ツールでは、Microsoft Windows で解釈されるように、Bluetooth デバイスの照会のレコードが表示されます。
ms.assetid: 3C48EEBA-3407-4A4A-91C2-EF001EFCDA6E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e1e90598ef52716cc164e6dedf01469366242cf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582353"
---
# <a name="bluetooth-inquiry-record-verifier"></a>Bluetooth Inquiry Record Verifier


Bluetooth の照会のレコードの検証ツールでは、Microsoft Windows で解釈されるように、Bluetooth デバイスの照会のレコードが表示されます。 このレコードは、サービスの探索プロトコルのレコードと取得した照会応答の拡張データの両方を示す、ツリー形式で表示されます。

このツールは、Microsoft Windows 認定プログラムまたは Bluetooth SIG の認定プロセスの任意の部分の置換ではありません。 デバイスと Microsoft Windows の間の相互作用のトラブルシューティングに役立つ Windows Driver Kit で提供されます。

Bluetooth の照会のレコードの検証ツールでは、3 つのメニューがあります。ファイル、ラジオ、および表示します。

使用して、**ファイル**を保存し、レコードを照会し、Bluetooth のプロファイルを開く メニュー。

-   現在の照会レコードを保存する をクリックして**ファイル&gt;エクスポート**します。

-   保存した照会レコードを開くには、次のようにクリックします。**ファイル&gt;インポート**します。

-   プロファイルの説明を読み込むには、次のようにクリックします。**ファイル&gt;プロファイルの説明を読み込む**します。 既定では、Microsoft が提供し、12 の一般的なプロファイルのプロファイルの説明を読み込みます。

-   読み込むには、どのプロファイル説明を選択する をクリックして**管理プロファイルの説明**します。

使用して、**ラジオ**] メニューの [すべての検出とペアになっているデバイスを表示します。

-   すべての検出とペアになっているデバイスを表示するには、次のようにクリックします。**ラジオ&gt;Inquire と選択**します。 その照会レコードを表示するデバイスを選択します。

-   指定したアドレスに Bluetooth 無線を照会するには、次のようにクリックします。**ラジオ&gt;アドレスを入力します**、し、[Bluetooth デバイスの選択] ダイアログ ボックスで Bluetooth の MAC アドレスを入力します。
-   現在表示されている、SDP のレコードを更新する をクリックして**ラジオ&gt;Requery 現在無線**します。

使用して、**ビュー** ] メニューの [結果を表示して、エラーを表示します。

-   16 進数で結果を表示するクリックして**ビュー&gt;生の結果**します。

-   その属性の Id に合わせて属性値を表示するには、次のようにクリックします。**ビュー&gt;属性の値に兄弟として**します。

-   エラーからエラーをジャンプするには、次のようにクリックします**ビュー&gt;前のエラー**または**ビュー&gt;次のエラー。**

## <a name="span-idknownissueswindows7spanspan-idknownissueswindows7spanspan-idknownissueswindows7spanknown-issues-windows-7"></a><span id="Known_Issues__Windows_7_"></span><span id="known_issues__windows_7_"></span><span id="KNOWN_ISSUES__WINDOWS_7_"></span>既知の問題 (Windows 7)


-   リモート デバイスを検索するには、初期の照会中に見つかったすべて表示されます。 照会が完了すると、対象のフレンドリ名があるデバイスのみが保持されます。
-   レコードの解析は機能しません、照会応答を拡張します。
-   **LanguageBaseAttributeIDList**間違って無効としてマークすることがあります。

 

 





