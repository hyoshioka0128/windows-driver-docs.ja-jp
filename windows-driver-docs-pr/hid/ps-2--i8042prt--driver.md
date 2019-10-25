---
title: PS/2 (i8042prt) ドライバー
description: このトピックでは、PS/2 スタイルのキーボードおよびマウスデバイス用の Microsoft Windows 2000 以降のシステム関数ドライバー I8042prt の機能について説明します。
ms.assetid: BB1046EE-8780-46ED-8CEB-63110643D325
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c9bc12c8e95aa9e5328f0f8bbf421df1acfc6cb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841560"
---
# <a name="ps2-i8042prt-driver"></a>PS/2 (i8042prt) ドライバー


このトピックでは、PS/2 スタイルのキーボードおよびマウスデバイス用の Microsoft Windows 2000 以降のシステム関数ドライバー *I8042prt*の機能について説明します。

I8042prt は I8042prt サービスを実装し、その実行可能イメージは I8042prt です。

I8042prt の機能は次のとおりです。

-   ハードウェアに依存し、PS/2 スタイルのキーボードとマウスデバイスの同時操作。

    キーボードとマウスは i/o ポートを共有しますが、さまざまな割り込み、割り込みサービスルーチン (ISR)、および ISR ディスパッチ完了ルーチンを使用します。

-   プラグアンドプレイ、電源管理、WMI

-   レガシデバイスの操作。

-   [キーボードクラスサービスコールバックルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/kbdmou/nc-kbdmou-pservice_callback_routine)と[マウスクラスサービスコールバックルーチン](https://docs.microsoft.com/previous-versions/ff542363(v=vs.85))の接続。

    I8042prt は、クラスのサービスコールバックを使用して、I8042prt の入力データバッファーからクラスドライバーのデータバッファーにデータを転送します。

-   ベンダーが提供する[**PI8042\_キーボード\_初期化\_ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/nc-ntdd8042-pi8042_keyboard_initialization_routine)コールバックルーチンをキーボードデバイスに追加します。

    オプションの上位レベルのデバイスフィルタードライバーは、コールバックルーチンを提供します。

-   ベンダーから提供された[**PI8042\_キーボード\_isr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/nc-ntdd8042-pi8042_keyboard_isr)コールバックルーチンとカスタム[**PI8042\_マウス\_isr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/nc-ntdd8042-pi8042_mouse_isr)コールバックルーチンの追加。

    オプションの上位レベルのデバイスフィルタードライバーは、これらのコールバックルーチンを提供します。

-   [キーボード書き込みバッファー要求](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/ni-ntdd8042-ioctl_internal_i8042_keyboard_write_buffer)と[マウス書き込みバッファー要求](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/ni-ntdd8042-ioctl_internal_i8042_mouse_write_buffer)。

    上位レベルのデバイスフィルタードライバーでは、書き込みバッファー要求を使用して、デバイスへの書き込みをデバイスに同期させることができます。また、デバイスでのその他の読み取りと書き込みを同期させることもできます。

-   [キーボードの開始情報要求](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/ni-ntdd8042-ioctl_internal_i8042_keyboard_start_information)と[マウスの開始情報の要求](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/ni-ntdd8042-ioctl_internal_i8042_mouse_start_information)。

    情報の開始要求では、デバイスの割り込みオブジェクトへのポインターが上位レベルのフィルタードライバーに渡されます。 フィルタードライバーは、interrupt オブジェクトを使用して、その操作をデバイスの ISR と同期させることができます。

-   [I8042prt コールバックルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。

    上位レベルのデバイスフィルタードライバーでは、デバイスの ISR のコンテキストでコールバックルーチンを使用して、デバイスに書き込むことができます。また、デバイスからのデータパケットをキューに置いてもかまいません。

### <a name="registry-settings-associated-with-the-ps2-driver"></a>PS/2 ドライバーに関連付けられているレジストリ設定

PS/2 ポートドライバーに関連付けられているレジストリキーの一覧を次に示します。

``` syntax
[Key: HKLM\SYSTEM\CurrentControlSet\Services\i8042prt\Parameters]
```

-   EnableWheelDetection \[REG\_DWORD\] –ドライバーがマウスデバイスのホイールを検出して有効にするかどうかを決定します。 一部のデバイスには、アプリケーションでサポートされている場合に、迅速なスクロールやその他のコントロール機能を提供するために、マウスホイールが搭載されています。
-   ResendIterations \[REG\_DWORD\] –ハードウェア操作が試行される最大回数を指定します。 試行回数がこのエントリの値を超えると、Windows は操作が失敗したと見なします。
-   NumberOfButtons \[REG\_DWORD\] –起動時にマウスポートマウスのボタンの数を指定します。 起動時に検出されたボタンの数が正しくない場合は、このエントリの値を変更することで上書きできます。
-   \[REG\_DWORD\] を指定する場合は、キーボードドライバーがバッファーするキーボードイベントの数を指定します。 このエントリは、非ページメモリプール内のキーボードドライバーの内部バッファーのサイズを計算するときにも使用されます。 バッファーに割り当てるバイト数を決定するために、システムはキーボード\_入力\_データ構造体のサイズを、Keyboard Dataの値で乗算します。
-   PollStatusIterations \[REG\_DWORD\] –システムが i8042 コントローラーステータスレジスタの割り込みを検証する最大回数を指定します。 このエントリの値に指定されている試行回数で割り込みが検証できない場合、割り込みは無視されます。
-   PollingIterations \[REG\_DWORD\]-Windows 2000 がハードウェアをポーリングする最大回数を指定します。 このエントリに指定されている試行回数を超えた場合、Windows 2000 はポーリングを停止します。
-   SampleRate \[REG\_DWORD\] – PS/2 ドライバーが PS/2 マウスの特性と動作を測定する頻度を指定します。 ドライバーは、サンプリングによって収集された情報を使用して、マウスデバイスの操作を最適化します。
-   PollingIterationsMaximum \[REG\_DWORD\] – Windows 2000 は、キーボードで古い形式のハードウェアをポーリングする最大回数を指定します。 このエントリに指定されている試行回数を超えた場合、Windows はポーリングを停止します。
-   OPEN Seresendstalltime \[REG\_DWORD\] – ACK を指定せずに再送信メッセージが返された場合に、マウスドライバーがリセットの受信確認 (ACK) を待機する時間を指定します。 このエントリは、マウスドライバーの割り込みサービスルーチンにリセットが含まれている場合に使用されます。
-   Overridekeyboard Type \[REG\_DWORD\] –キーボードの種類を指定します。 このエントリをレジストリに追加すると、起動時に検出されたキーボードの種類のエラーを修正できます。
-   Overridekeyboard Subtype \[REG\_DWORD\] – OEM に依存するキーボードサブタイプを指定します。 このエントリをレジストリに追加すると、起動時に検出されたキーボードサブタイプのエラーを修正できます。

詳細については、次のサイトを参照してください。

* https://docs.microsoft.com/windows/desktop/sysinfo/about-the-registry
* https://docs.microsoft.com/windows/desktop/sysinfo/registry-reference 
