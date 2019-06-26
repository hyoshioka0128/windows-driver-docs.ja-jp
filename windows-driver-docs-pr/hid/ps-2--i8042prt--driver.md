---
title: PS/2 (i8042prt) ドライバー
description: このトピックでは、I8042prt、Microsoft Windows 2000 以降のバージョンのシステム関数ドライバー PS/2 形式のキーボードとマウス デバイスの機能について説明します。
ms.assetid: BB1046EE-8780-46ED-8CEB-63110643D325
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de2287a99dfb610f85bd8cdf5053e1a0280d8a17
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385811"
---
# <a name="ps2-i8042prt-driver"></a>PS/2 (i8042prt) ドライバー


このトピックでは、の機能を示します*I8042prt*、Microsoft Windows 2000 と PS/2 形式のキーボードとマウス デバイスの場合、以降のバージョンのシステム関数ドライバー。

I8042prt I8042prt サービスを実装して、その実行可能イメージは i8042prt.sys します。

I8042prt の機能は次のとおりです。

-   PS/2 スタイル キーボードとマウス デバイスの操作をハードウェアに依存して同時に実行します。

    キーボードとマウス、I/O ポートを共有が、異なる割り込み、割り込みサービス ルーチン (ISR) および ISR ディスパッチの完了ルーチンを使用します。

-   プラグ アンド プレイ、電源管理、および WMI

-   レガシ デバイスの操作です。

-   接続、[クラス サービス コールバック ルーチンをキーボード](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/kbdmou/nc-kbdmou-pservice_callback_routine)と[クラス サービス コールバック ルーチンをマウス](https://docs.microsoft.com/previous-versions/ff542363(v=vs.85))します。

    I8042prt では、クラスのサービスのコールバックを使用して、クラス ドライバーのデータ バッファーに I8042prt の入力データのバッファーからデータを転送します。

-   ベンダーから提供された追加[ **PI8042\_キーボード\_初期化\_ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntdd8042/nc-ntdd8042-pi8042_keyboard_initialization_routine)キーボード デバイス用のコールバック ルーチン。

    省略可能な上位レベルのデバイスのフィルター ドライバーは、コールバック ルーチンを提供します。

-   ベンダーから提供された追加[ **PI8042\_キーボード\_ISR** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntdd8042/nc-ntdd8042-pi8042_keyboard_isr)コールバック ルーチンと、カスタム[ **PI8042\_マウス\_ISR** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntdd8042/nc-ntdd8042-pi8042_mouse_isr)コールバック ルーチン。

    省略可能な上位レベルのデバイスのフィルター ドライバーは、これらのコールバック ルーチンを提供します。

-   [キーボードの書き込みバッファー要求](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntdd8042/ni-ntdd8042-ioctl_internal_i8042_keyboard_write_buffer)と[マウス書き込みバッファー要求](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntdd8042/ni-ntdd8042-ioctl_internal_i8042_mouse_write_buffer)します。

    その他の読み取りし、デバイスで書き込みし、上位レベルのデバイスのフィルター ドライバーとデバイスの ISR デバイスへの書き込みを同期するバッファーの書き込み要求を使用できます。

-   [キーボードの開始情報要求](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntdd8042/ni-ntdd8042-ioctl_internal_i8042_keyboard_start_information)と[マウス開始情報要求](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntdd8042/ni-ntdd8042-ioctl_internal_i8042_mouse_start_information)します。

    開始情報の要求は、上位レベルのフィルター ドライバーへのデバイスの割り込みオブジェクトへのポインターを渡します。 フィルター ドライバーは、デバイスの ISR とその操作を同期するのに割り込みオブジェクトを使用することができます。

-   [I8042prt コールバック ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

    上位レベルのデバイスのフィルター ドライバーは、デバイス、およびデバイスからのデータ パケットをキューに書き込む、デバイスの ISR のコンテキストでコールバック ルーチンを使用できます。

### <a name="registry-settings-associated-with-the-ps2-driver"></a>Ps/2 ドライバーに関連するレジストリ設定

次には、ps/2 ポート ドライバーに関連付けられているレジストリ キーの一覧を示します。

``` syntax
[Key: HKLM\SYSTEM\CurrentControlSet\Services\i8042prt\Parameters]
```

-   EnableWheelDetection \[REG\_DWORD\] –、ドライバーを検出し、マウスのホイールを有効にするかどうかを決定します。 一部のデバイスは、マウスのホイールが高速スクロールを提供して、アプリケーションがサポートされている場合は、その他のコントロール機能を備えています。
-   ResendIterations \[REG\_DWORD\] – ハードウェア操作の試行回数の最大数を指定します。 試用版の数は、このエントリの値を超えている場合、Windows は、失敗した操作を考慮します。
-   NumberOfButtons \[REG\_DWORD\] – 起動時にマウス ポート マウスのボタンの数を指定します。 スタートアップ時に検出されたボタンの数が正しくない場合は、このエントリの値を変更することによってオーバーライドできます。
-   説明する\[REG\_DWORD\] – キーボード イベントの数を指定するキーボードのドライバー バッファー。 このエントリは、非ページ メモリ プール内のキーボード ドライバーの内部バッファーのサイズの計算にも使用されます。 システムをバッファーに割り当てるバイト数を確認するには、キーボードのサイズを乗算します\_入力\_で説明するの値によってデータ構造体。
-   PollStatusIterations \[REG\_DWORD\] – システム検証 i8042 コント ローラーの状態のレジスタの割り込み時間の最大数を指定します。 このエントリの値で指定された試行回数では、割り込みを確認することはできません、割り込みは無視されます。
-   タイムアウト\[REG\_DWORD\] -Windows 2000、ハードウェアをポーリングする最大回数を指定します。 このエントリで指定された試行回数を超えた場合、Windows 2000 には、ポーリングが停止します。
-   SampleRate \[REG\_DWORD\] – ps/2 ドライバーがの特性と ps/2 マウスのアクティビティを測定するどのくらいの頻度を指定します。 ドライバーは、マウス デバイスの操作を最適化するために、サンプリングで収集した情報を使用します。
-   PollingIterationsMaximum \[REG\_DWORD\] – Windows 2000 がキーボードで古いスタイルのハードウェアをポーリングする最大回数を指定します。 このエントリで指定された試行回数を超えた場合、Windows には、ポーリングが停止します。
-   MouseResendStallTime \[REG\_DWORD\] – マウス ドライバーが ACK メッセージを再送信が返されなかった場合に、リセットの受信確認 (ACK) を待機する時間を決定します。 このエントリは、マウス ドライバー割り込みサービス ルーチンには、リセットが含まれている場合に使用されます。
-   OverrideKeyboardType \[REG\_DWORD\] – キーボードの種類を指定します。 レジストリ スタートアップ時に検出されたキーボードの種類のエラーを修正するには、このエントリを追加できます。
-   OverrideKeyboardSubtype \[REG\_DWORD\] – OEM に依存するキーボードのサブタイプを指定します。 レジストリ スタートアップ時に検出されたキーボードのサブタイプでエラーを修正するには、このエントリを追加できます。

詳細については、次のサイトを参照してください。

* https://docs.microsoft.com/windows/desktop/sysinfo/about-the-registry
* https://docs.microsoft.com/windows/desktop/sysinfo/registry-reference 
