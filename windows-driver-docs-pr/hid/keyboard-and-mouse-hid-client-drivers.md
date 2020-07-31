---
title: キーボードとマウスの HID クライアント ドライバー
description: キーボードとマウスの HID クライアント ドライバーをご覧ください。
ms.assetid: DAD50261-7619-4554-B864-9158A0FA1ACE
keywords:
- HID キーボードドライバー
- キーボードドライバー、HID
- Windows 用 HID キーボードドライバー
- HID マウスドライバー
- マウスドライバー、HID
- Windows 用 HID マウスドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a7a76af565ccaf5058e3d19eeb335ddd348c2e1
ms.sourcegitcommit: f63852446e614c985a65f599cdfe788bdb0c6089
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/30/2020
ms.locfileid: "87425738"
---
# <a name="keyboard-and-mouse-hid-client-drivers"></a>キーボードとマウスの HID クライアント ドライバー

> [!NOTE]
> このトピックは、キーボードおよびマウス HID クライアント用のドライバーを作成する開発者を対象としています。 マウスまたはキーボードを修正する場合は、次を参照してください。
>
> - [Windows でのマウス、タッチパッド、キーボードの問題](https://support.microsoft.com/help/17417/windows-mouse-touchpad-keyboard-problems)
> - [正常に機能しないワイヤレスマウスのトラブルシューティング](https://support.microsoft.com/help/321122/troubleshoot-a-wireless-mouse-that-does-not-function-correctly)

このトピックでは、キーボードとマウスの HID クライアントドライバーについて説明します。 キーボードとマウスは、HID の使用表で標準化され、Windows オペレーティングシステムに実装されている最初の HID クライアントのセットを表します。

キーボードとマウスの HID クライアントドライバーは、HID マッパードライバーの形式で実装されています。 HID マッパードライバーは、非 HID クラスドライバーと HID クラスドライバーの間の i/o 要求に対して双方向インターフェイスを提供するカーネルモードの WDM フィルタードライバーです。 マッパードライバーは、1つの i/o 要求とデータプロトコルを相互にマップします。

Windows には、HID キーボードおよび HID マウスデバイス用のシステム提供の HID マッパードライバーが用意されています。

## <a name="architecture-and-overview"></a>アーキテクチャと概要

次の図は、USB キーボードおよびマウス/タッチパッドデバイスのシステム提供のドライバースタックを示しています。

![キーボードおよびマウスドライバーのスタック図。キーボードおよびマウス用の hid クラスマッパードライバーと共に、キーボードおよびマウスクラスドライバーが表示されます。](images/keyboard-driver-stack.png)

上の図には、次のコンポーネントが含まれています。

- KBDHID.sys –キーボード用の HID クライアントマッパードライバー。 HID 使用法を scancodes に変換し、既存のキーボードクラスドライバーとのインターフェイスを使用します。
- MOUHID.sys – HID クライアントマッパー driver for ネズミ/タッチパッド向け。 HID 使用法を、既存のキーボードクラスドライバーとのインターフェイスにマウスコマンド (X/Y、ボタン、ホイール) に変換します。
- KBDCLASS.sys-キーボードクラスドライバーは、システム上のすべてのキーボードとキーパッドの機能を安全な方法で保持します。
- MOUCLASS.sys –マウスクラスドライバーは、システム上のすべてのマウス/タッチパッド向けの機能を維持します。 このドライバーは、絶対ポイントデバイスと相対ポイントデバイスの両方をサポートしています。 これは、Windows の別のドライバーによって管理されている touchscreens のドライバーではありません。

システムは、次のようにドライバースタックを構築します。

- トランスポートスタックは、接続されている各 HID デバイスに対して物理デバイスオブジェクト (PDO) を作成し、適切な HID トランスポートドライバーを読み込みます。これにより、HID クラスドライバーが読み込まれます。
- HID クラスドライバーは、キーボードまたはマウス TLC ごとに PDO を作成します。 複雑な HID デバイス (1 つ以上の TLC) は、HID クラスドライバーによって作成された複数の PDOs として公開されます。 たとえば、マウスが統合されたキーボードには、標準のキーボードコントロール用に1つのコレクションがあり、マウスに別のコレクションが存在する場合があります。
- キーボードまたはマウス hid クライアントマッパードライバーは、適切な FDO に読み込まれます。
- HID マッパードライバーは、キーボードおよびマウス用の FDOs を作成し、クラスドライバーを読み込みます。

重要なメモ:

- サポートされている HID 使用と最上位のコレクションに準拠しているキーボードおよびマウスでは、ベンダードライバーは必要ありません。
- 必要に応じて、ベンダーは HID スタックにフィルタードライバーを提供して、これらの特定の TLC の機能を変更/拡張できます。
- ベンダーは、独自の TLCs を作成する必要があります。これはベンダー固有のもので、hid クライアントとデバイスの間でベンダー独自のデータを交換します。 重大でない限り、フィルタードライバーは使用しないでください。
- システムによって、すべてのキーボードおよびマウスのコレクションが排他的に使用されます。
- キーボードを無効または有効にできないようにします。
- システムは、スムーズスクロール機能を備えた水平または垂直のホイールをサポートしています。

## <a name="driver-guidance"></a>ドライバーのガイダンス

Microsoft では、Ihv によるドライバーの書き込みに関する次のガイダンスを提供しています。

1. ドライバー開発者は、フィルタードライバーまたは新しい HID クライアントドライバーの形式で追加のドライバーを追加できます。 条件は次のとおりです。
    1. フィルタードライバー: ドライバー開発者は、その値追加ドライバーがフィルタードライバーであり、入力スタック内の既存の Windows HID ドライバーを置き換える (またはその代わりに使用されない) ことを確認する必要があります。
        - フィルタードライバーは、次のシナリオで許可されます。
            - Kbdhid/の場合は、上位フィルターとして
            - Kbdclass/クラスへの上位フィルターとして
        - フィルタードライバーは、HIDCLASS と HID Transport ミニドライバー間のフィルターとして推奨されて_いません_。

    2. 関数ドライバー: または、ベンダー固有の HID PDOs (必要に応じてユーザーモードサービス) に対してのみ、(フィルタードライバーではなく) 関数ドライバーを作成できます。

        関数ドライバーは、次のシナリオで使用できます。

        - 特定のベンダーのハードウェアにのみ負荷をかける

    3. トランスポートドライバー: Windows チームは、書き込み/保守のための複雑なドライバーであるため、追加の HID Transport ミニドライバーを作成することは推奨されません。 パートナーが新しい HID トランスポートミニドライバーを作成している場合 (特に SoC システムの場合) は、その理由を理解し、ドライバーが正しく開発されていることを確認するために、詳細なアーキテクチャレビューを行うことをお勧めします。

2. ドライバーの開発者は、ドライバーフレームワーク (KMDF または UMDF) を活用する必要があり、そのフィルタードライバーでは WDM に依存しません。
3. ドライバーの開発者は、サービスとドライバースタック間のカーネルユーザーの移行回数を減らす必要があります。
4. ドライバー開発者は、キーボードとタッチパッドの両方の機能 (エンドユーザー (デバイスマネージャー) または PC の製造元によって調整可能) を使用してシステムをスリープ解除できることを確認する必要があります。 SoC システムに加えて、これらのデバイスは、システムが動作している S0 の状態である間、電力が低い状態からスリープ解除できる必要があります。
5. ドライバーの開発者は、ハードウェアが効率的に電源管理されるようにする必要があります。
    - デバイスがアイドル状態になると、デバイスの電源が最も低くなります。
    - システムの電源が低状態である場合 (たとえば、スタンバイ (S3) またはコネクトスタンバイ)、デバイスの電源の状態は最も低くなります。

## <a name="keyboard-layout"></a>キーボードレイアウト

*キーボードレイアウト*では、Microsoft Windows 2000 以降のバージョンのキーボード入力特性が完全に記述されています。 たとえば、キーボードレイアウトでは、言語、キーボードの種類、バージョン、修飾子、スキャンコードなどを指定します。

キーボードレイアウトの詳細については、次を参照してください。

- キーボードのレイアウトに関する全般的な情報をドキュメントに記載した Windows Driver Development Kit (DDK) のキーボードヘッダーファイル (kdb .h)。

- サンプルのキーボード[レイアウト](https://go.microsoft.com/fwlink/p/?linkid=256128)。

特定のキーボードのレイアウトを視覚化するには、「 [Windows キーボードレイアウト](https://docs.microsoft.com/globalization/windows-keyboard-layouts)」を参照してください。

キーボードレイアウトの詳細については、コントロールパネルの \\ 時計、言語、および地域の言語に関するページを参照してください \\ 。

## <a name="supported-buttons-and-wheels-on-mice"></a>マウスでサポートされているボタンとホイール

次の表は、さまざまなクライアントバージョンの Windows オペレーティングシステムでサポートされている機能を示しています。

|特徴量|Windows XP|Windows Vista|Windows 7|Windows 8 以降|
|----|----|----|----|----|
|ボタン1-5|サポート (P/2 & HID)|サポートされている (PS/2 & HID)|サポートされている (PS/2 & HID)|サポートされている (PS/2 & HID)|
|垂直スクロールホイール|サポートされている (PS/2 & HID)|サポートされている (PS/2 & HID)|サポートされている (PS/2 & HID)|サポートされている (PS/2 & HID)|
|水平スクロールホイール|サポートされていません|サポート (HID のみ)|サポート (HID のみ)|サポート (HID のみ)|
|スムーズスクロールホイールのサポート (水平および垂直)|サポートされていません|部分的にサポート|サポート (HID のみ)|サポート (HID のみ)|

### <a name="activating-buttons-4-5-and-wheel-on-ps2-mice"></a>PS/2 マウスでのボタン4-5 とホイールのアクティブ化

新しい 4&5 ボタン + ホイールモードをアクティブにするために Windows によって使用されるメソッドは、3番目のボタンと IntelliMouse 互換のマウスのホイールをアクティブ化するために使用されるメソッドの拡張機能です。

- 1つ目は、マウスを3ボタンホイールモードに設定することです。これは、レポートレートを200レポート/秒に連続して設定し、次に 100 80 reports/second に設定し、次にマウスから ID を読み取ることで実現されます。 このシーケンスが完了すると、マウスは ID 3 を報告する必要があります。
- 次に、マウスは5つのボタンのホイールモードに設定されます。これは、レポートレートを連続して200レポート/秒に設定し、次に 200 reports/second に再び設定し、次に 80 reports/second に対してマウスで ID を読み取ることで実現されます。 このシーケンスが完了すると、5ボタンのホイールマウスは ID 4 を報告する必要があります (一方、IntelliMouse と互換性のある3ボタンホイールマウスでは、ID が3であると報告されます)。

これは PS/2 マウスにのみ適用されることに注意してください。 HID マウスには適用されません (HID マウスはレポート記述子で正確な使用状況を報告する必要があります)。

#### <a name="standard-ps2-compatible-mouse-data-packet-format-2-buttons"></a>標準 PS/2 互換マウスデータパケット形式 (2 ボタン)

|Byte|D7|D6|D5|D4|D3|D2|D1|D0|コメント|
|------|-------|-------|-------|-------|-----|-----|-----|-----|-----|
| 1    | Yover | Xover | Ysign | Xsign | タグ | M   | R   | L   | X/Y overvlows と記号、ボタン |
| 2    | X 7    | X6    | X5    | X4    | X3  | X2  | X1  | X0  | X データバイト                      |
| 3    | Y7    | Y6    | Y5    | Y4    | Y3  | Y2  | Y1  | Y0  | Y データバイト数                     |

> [!NOTE]
> Windows マウスドライバーでは、オーバーフロービットはチェックされません。 オーバーフローが発生した場合、マウスは単に最大符号付きの変位値を送信する必要があります。

#### <a name="standard-ps2-compatible-mouse-data-packet-format-3-buttons--verticalwheel"></a>標準 PS/2 互換マウスデータパケット形式 (3 つのボタン + 垂直ホイール)

| Byte | D7  | D6  | D5    | D4    | D3  | D2  | D1  | D0  | コメント                     |
|------|-----|-----|-------|-------|-----|-----|-----|-----|-----------------------------|
| 1    | 0   | 0   | Ysign | Xsign | 1   | M   | R   | L   | X/Y 記号と R/L/M ボタン |
| 2    | X 7  | X6  | X5    | X4    | X3  | X2  | X1  | X0  | X データバイト                 |
| 3    | Y7  | Y6  | Y5    | Y4    | Y3  | Y2  | Y1  | Y0  | Y データバイト数                |
| 4    | Z7  | Z6  | Z5    | Z4    | Z3  | Z2  | Z1  | A-za-z0  | Z/ホイールデータバイト           |

#### <a name="standard-ps2-compatible-mouse-data-packet-format-5-buttons--verticalwheel"></a>標準 PS/2 互換マウスデータパケット形式 (5 つのボタン + 垂直ホイール)

| Byte | D7  | D6  | D5    | D4    | D3  | D2  | D1  | D0  | コメント                               |
|------|-----|-----|-------|-------|-----|-----|-----|-----|---------------------------------------|
| 1    | 0   | 0   | Ysign | Xsign | 1   | M   | R   | L   | X/Y 記号と R/L/M ボタン           |
| 2    | X 7  | X6  | X5    | X4    | X3  | X2  | X1  | X0  | X データバイト                           |
| 3    | Y7  | Y6  | Y5    | Y4    | Y3  | Y2  | Y1  | Y0  | Y データバイト数                          |
| 4    | 0   | 0   | B5    | B4    | Z3  | Z2  | Z1  | A-za-z0  | Z/ホイールデータとボタン4および5 |

>[!IMPORTANT]
>IntelliMouse と互換性のある3ボタンホイールモードで使用される8ビットではなく、5つのボタンのホイールマウスの Z/ホイールデータが4ビットに縮小されていることに注意してください。 この削減は、特定の割り込み期間中に、通常、ホイールが範囲 + 7/-8 を超える値を生成できないという事実によって可能になります。 マウスが5ボタンのホイールモードになっている場合は、Windows のマウスドライバーによって4つの Z/wheel データビットが拡張され、3ボタンのホイールモードでマウスが動作する場合は、Z/ホイールのデータバイトが表示されます。
>
>のボタン 4 & 5 は、WM appcommand メッセージにマップされ \_ 、アプリの \_ バックとアプリの転送に対応し \_ ます。

### <a name="devices-not-requiring-vendor-drivers"></a>ベンダドライバを必要としないデバイス

製造元のドライバーは、次のデバイスには必要ありません。

- HID 標準に準拠しているデバイス。
- システムによって提供される非 HIDClass ドライバーによって操作されるキーボード、マウス、またはゲームポートデバイス。

## <a name="kbfiltr-sample"></a>Kbfiltr サンプル

Kbfiltr は、Kbdclass で使用するように設計されています。これは、キーボードデバイスと I8042prt のシステムクラスドライバーであり、PS/2 スタイルのキーボード用の関数ドライバーです。 Kbfiltr は、i/o 要求をフィルター処理する方法と、Kbdclass および I8042prt の操作を変更するコールバックルーチンを追加する方法を示しています。

Kbfiltr 操作の詳細については、次を参照してください。

- Ntddkbd WDK ヘッダーファイル。

- サンプルの[Kbfiltr](https://go.microsoft.com/fwlink/p/?linkid=256125)ソースコード。

### <a name="kbfiltr-ioctls"></a>Kbfiltr Ioctl

#### <a name="ioctl_internal_i8042_hook_keyboard"></a>IOCTL_INTERNAL_I8042_HOOK_KEYBOARD

IOCTL_INTERNAL_I8042_HOOK_KEYBOARD 要求では、次のことが行われます。

- 初期化コールバックルーチンを I8042prt キーボード初期化ルーチンに追加します。
- ISR コールバックルーチンを I8042prt キーボード ISR に追加します。

初期化と ISR のコールバックは省略可能であり、PS/2 スタイルのキーボードデバイス用の上位レベルのフィルタードライバーによって提供されます。

I8042prt は、 **IOCTL_INTERNAL_KEYBOARD_CONNECT**要求を受信すると、同期**IOCTL_INTERNAL_I8042_HOOK_KEYBOARD**要求をキーボードデバイススタックの一番上に送信します。

Kbfiltr がフックキーボード要求を受け取ると、Kbfiltr は次の方法で要求をフィルター処理します。

- 上位レベルのデバイスオブジェクトのコンテキスト、初期化コールバックへのポインター、および ISR コールバックへのポインターを含む、Kbfiltr に渡される上位レベルの情報を保存します。
- 上位レベルの情報を独自のに置き換えます。
- I8042prt のコンテキストと、Kbfiltr ISR コールバックで使用できるコールバックへのポインターを保存します。

#### <a name="ioctl_internal_keyboard_connect"></a>IOCTL_INTERNAL_KEYBOARD_CONNECT

**IOCTL_INTERNAL_KEYBOARD_CONNECT**要求は、Kbdclass サービスをキーボードデバイスに接続します。 Kbdclass は、キーボードデバイスを開く前に、この要求をキーボードデバイススタックに送信します。

Kbfiltr がキーボード接続要求を受け取った後、Kbfiltr は次の方法で connect 要求をフィルター処理します。

- Kbdclass によってフィルタードライバーに渡される Kbdclass の**CONNECT_DATA (Kbdclass)** 構造体のコピーを保存します。
- クラスドライバー接続情報の独自の接続情報を置き換えます。
- **IOCTL_INTERNAL_KEYBOARD_CONNECT**要求をデバイススタックに送信します。

要求が成功しなかった場合、Kbfiltr は適切なエラー状態で要求を完了します。

Kbfiltr は、Kbdclass クラスのサービスコールバックルーチン**KeyboardClassServiceCallback**の操作を補完できるフィルターサービスコールバックルーチンのテンプレートを提供します。 フィルターサービスのコールバックでは、デバイスの入力バッファーからクラスデータキューに転送される入力データをフィルター処理できます。

#### <a name="ioctl_internal_keyboard_disconnect"></a>IOCTL_INTERNAL_KEYBOARD_DISCONNECT

**IOCTL_INTERNAL_KEYBOARD_DISCONNECT**要求は、STATUS_NOT_IMPLEMENTED の状態で完了します。 プラグアンドプレイマネージャーでプラグアンドプレイキーボードを追加または削除できることに注意してください。

その他のすべてのデバイス制御要求では、Kbfiltr は、現在の IRP スタックをスキップし、要求をデバイススタックに送信します。これを処理する必要はありません。

### <a name="callback-routines-implemented-by-kbfiltr"></a>Kbfiltr によって実装されるコールバックルーチン

#### <a name="kbfilter_initializationroutine"></a>KbFilter_InitializationRoutine

「」を参照してください**PI8042_KEYBOARD_INITIALIZATION_ROUTINE**

キーボードの I8042prt の既定の初期化に十分な場合、 **KbFilter_InitializationRoutine**は必要ありません。

I8042prt は、キーボードを初期化するときに**KbFilter_InitializationRoutine**を呼び出します。 既定のキーボード初期化には、次の操作が含まれます。

- キーボードをリセットする
- 速度のレートと遅延を設定する
- 発光ダイオード (LED) を設定する

```cpp
/*
Parameters
DeviceObject [in]
Pointer to the device object that is the context for this callback.

SynchFuncContext [in]
Pointer to the context for the routines pointed to by ReadPort and Writeport.

ReadPort [in]
Pointer to the system-supplied PI8042_SYNCH_READ_PORT callback that reads from the port.

WritePort [in]
Pointer to the system-supplied PI8042_SYNCH_WRITE_PORT callback that writes to the port.

TurnTranslationOn [out]
Specifies, if TRUE, to turn translation on. Otherwise, translation is turned off.

Return value
KbFilter_InitializationRoutine returns an appropriate NTSTATUS code.
*/

NTSTATUS KbFilter_InitializationRoutine(
  In  PDEVICE_OBJECT          DeviceObject,
  In  PVOID                   SynchFuncContext,
  In  PI8042_SYNCH_READ_PORT  ReadPort,
  In  PI8042_SYNCH_WRITE_PORT WritePort,
  Out PBOOLEAN                TurnTranslationOn
);
```

#### <a name="kbfilter_isrhook"></a>KbFilter_IsrHook

「 **PI8042_KEYBOARD_ISR**」を参照してください。 I8042prt の既定の操作で十分な場合、このコールバックは必要ありません。

I8042prt キーボード ISR は、割り込みを検証し、スキャンコードを読み取ると**KbFilter_IsrHook**を呼び出します。

**KbFilter_IsrHook**は、I8042prt キーボードの IRQL でカーネルモードで実行されます。

```cpp
/*
Parameters
DeviceObject [in]
Pointer to the filter device object of the driver that supplies this callback.

CurrentInput [in]
Pointer to the input KEYBOARD_INPUT_DATA structure that is being constructed by the ISR.

CurrentOutput [in]
Pointer to an OUTPUT_PACKET structure that specifies the bytes that are being written to the hardware device.

StatusByte [in, out]
Specifies the status byte that is read from I/O port 60 when an interrupt occurs.

DataByte [in]
Specifies the data byte that is read from I/O port 64 when an interrupt occurs.

ContinueProcessing [out]
Specifies, if TRUE, to continue processing in the I8042prt keyboard ISR after this callback returns; otherwise, processing is not continued.

ScanState [in]
Pointer to a KEYBOARD_SCAN_STATE structure that specifies the keyboard scan state.

Return value
KbFilter_IsrHook returns TRUE if the interrupt service routine should continue; otherwise it returns FALSE.
*/

KbFilter_IsrHook KbFilter_IsrHook(
  <em>In</em>    PDEVICE_OBJECT       DeviceObject,
  <em>In</em>    PKEYBOARD_INPUT_DATA CurrentInput,
  <em>In</em>    POUTPUT_PACKET       CurrentOutput,
  <em>Inout</em> UCHAR                StatusByte,
  <em>In</em>    PUCHAR               DataByte,
  <em>Out</em>   PBOOLEAN             ContinueProcessing,
  <em>In</em>    PKEYBOARD_SCAN_STATE ScanState
);
```

#### <a name="kbfilter_servicecallback"></a>KbFilter_ServiceCallback

「 **PSERVICE_CALLBACK_ROUTINE**」を参照してください。

関数ドライバーの ISR ディスパッチ完了ルーチンは**KbFilter_ServiceCallback**を呼び出し、その後、キーボードクラスドライバーの*PSERVICE_CALLBACK_ROUTINE*の実装を呼び出します。 ベンダーは、フィルターサービスコールバックを実装して、デバイスの入力バッファーからクラスデータキューに転送される入力データを変更できます。 たとえば、コールバックは、データの削除、変換、または挿入を行うことができます。

```cpp
/*
Parameters
DeviceObject [in]
Pointer to the class device object.

InputDataStart [in]
Pointer to the first keyboard input data packet in the input data buffer of the port device.

InputDataEnd [in]
Pointer to the keyboard input data packet that immediately follows the last data packet in the input data buffer of the port device.

InputDataConsumed [in, out]
Pointer to the number of keyboard input data packets that are transferred by the routine.

Return value
None
*/

VOID KbFilter_ServiceCallback(
  <em>In</em>    PDEVICE_OBJECT       DeviceObject,
  <em>In</em>    PKEYBOARD_INPUT_DATA InputDataStart,
  <em>In</em>    PKEYBOARD_INPUT_DATA InputDataEnd,
  <em>Inout</em> PULONG               InputDataConsumed
);
```

## <a name="moufiltr-sample"></a>お持ちのサンプル

I8042prt は、このクラスと共に使用するように設計されています。このクラスは、Windows 2000 以降のバージョンで使用されるマウスデバイス用のシステムクラスドライバーであり、Windows 2000 以降で使用される PS/2 スタイルのマウスの関数ドライバーです。 I8042prt filtr は、i/o 要求をフィルター処理し、の操作を変更するコールバックルーチンを追加する方法を示しています。

### <a name="moufiltr-control-codes"></a>コントロールコード

#### <a name="ioctl_internal_i8042_hook_mouse"></a>IOCTL_INTERNAL_I8042_HOOK_MOUSE

**IOCTL_INTERNAL_I8042_HOOK_MOUSE**要求は、isr コールバックルーチンを I8042PRT MOUSE isr に追加します。 ISR コールバックは省略可能であり、上位レベルのマウスフィルタードライバーによって提供されます。

I8042prt は、 **IOCTL_INTERNAL_MOUSE_CONNECT**要求を受信した後に、この要求を送信します。 I8042prt は、マウスデバイススタックの一番上に同期**IOCTL_INTERNAL_I8042_HOOK_MOUSE**要求を送信します。

ネズミ Filtr は、フックマウス要求を受信した後、次の方法で要求をフィルター処理します。

- 上位レベルのデバイスオブジェクトのコンテキストと ISR コールバックへのポインターを含む、テキストに渡された上位レベルの情報を保存します。
- 上位レベルの情報を独自のに置き換えます。
- I8042prt のコンテキストと、このコールバックが使用できるコールバックへのポインターを保存します。

### <a name="moufiltr-callback-routines"></a>///コールバックルーチン

#### <a name="ioctl_internal_mouse_connect"></a>IOCTL_INTERNAL_MOUSE_CONNECT

IOCTL_INTERNAL_MOUSE_CONNECT 要求は、マウスデバイスにマウスのサービスを接続します。

#### <a name="ioctl_internal_mouse_disconnect"></a>IOCTL_INTERNAL_MOUSE_DISCONNECT

IOCTL_INTERNAL_MOUSE_DISCONNECT 要求は、STATUS_NOT_IMPLEMENTED のエラー状態を持つ、の場合には、このように完了します。

他のすべての要求については、現在の IRP スタックがスキップされ、デバイススタックに要求が送信されます。これを処理する必要はありません。

### <a name="callback-routines"></a>コールバックルーチン

#### <a name="moufilter_isrhook"></a>MouFilter_IsrHook

「 **PI8042_MOUSE_ISR**」を参照してください。

```cpp
/*
Parameters
DeviceObject
Pointer to the filter device object of the driver that supplies this callback.

CurrentInput
Pointer to the input MOUSE_INPUT_DATA structure being constructed by the ISR.

CurrentOutput
Pointer to the OUTPUT_PACKET structure that specifies the bytes being written to the hardware device.

StatusByte
Specifies a status byte that is read from I/O port 60 when the interrupt occurs.

DataByte
Specifies a data byte that is read from I/O port 64 when the interrupt occurs.

ContinueProcessing
Specifies, if TRUE, that the I8042prt mouse ISR continues processing after this callback returns. Otherwise, processing is not continued.

MouseState
Pointer to a MOUSE_STATE enumeration value, which identifies the state of mouse input.

ResetSubState
Pointer to MOUSE_RESET_SUBSTATE enumeration value, which identifies the mouse reset substate. See the Remarks section.

Return value
MouFilter_IsrHook returns TRUE if the interrupt service routine should continue; otherwise it returns FALSE.
*/

BOOLEAN MouFilter_IsrHook(
   PDEVICE_OBJECT        DeviceObject,
   PMOUSE_INPUT_DATA     CurrentInput,
   POUTPUT_PACKET        CurrentOutput,
   UCHAR                 StatusByte,
   PUCHAR                DataByte,
   PBOOLEAN              ContinueProcessing,
   PMOUSE_STATE          MouseState,
   PMOUSE_RESET_SUBSTATE ResetSubState
);
```

I8042prt の既定の操作で十分であれば、 **MouFilter_IsrHook**コールバックは必要ありません。

I8042prt マウス ISR は、割り込みを検証した後に**MouFilter_IsrHook**を呼び出します。

マウスをリセットするために、I8042prt は一連の操作の下位の部分を通過し、それぞれが MOUSE_RESET_SUBSTATE 列挙値によって識別されます。 I8042prt がマウスとそれに対応するマウスリセットの下位部分をリセットする方法の詳細については、ntdd8042 の MOUSE_RESET_SUBSTATE のドキュメントを参照してください。

**MouFilter_IsrHook**は、I8042PRT マウス ISR の IRQL でカーネルモードで実行されます。

#### <a name="moufilter_servicecallback"></a>MouFilter_ServiceCallback

「」を参照してください*PSERVICE_CALLBACK_ROUTINE*

```cpp
/*
Parameters
DeviceObject [in]
Pointer to the class device object.

InputDataStart [in]
Pointer to the first mouse input data packet in the input data buffer of the port device.

InputDataEnd [in]
Pointer to the mouse input data packet immediately following the last data packet in the port device's input data buffer.

InputDataConsumed [in, out]
Pointer to the number of mouse input data packets that are transferred by the routine.

Return value
None
*/

VOID MouFilter_ServiceCallback(
  _In_    PDEVICE_OBJECT    DeviceObject,
  _In_    PMOUSE_INPUT_DATA InputDataStart,
  _In_    PMOUSE_INPUT_DATA InputDataEnd,
  _Inout_ PULONG            InputDataConsumed
);
```

I8042prt の ISR DPC は MouFilter_ServiceCallback を呼び出し、その後、MouseClassServiceCallback を呼び出します。 フィルターサービスコールバックは、デバイスの入力バッファーからクラスデータキューに転送される入力データを変更するように構成できます。 たとえば、コールバックは、データの削除、変換、または挿入を行うことができます。
