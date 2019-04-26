---
title: キーボードとマウスの HID クライアント ドライバー
description: キーボードとマウスの HID クライアント ドライバーをご覧ください。
ms.assetid: DAD50261-7619-4554-B864-9158A0FA1ACE
keywords:
- HID キーボード ドライバー
- キーボード ドライバー、HID
- Windows 用 HID キーボード ドライバー
- マウスの HID ドライバー
- マウスのドライバー、HID
- Windows 用 HID マウス ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4d83fcc34bcdc272e9e903ab1e9dfca6ca50893
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346242"
---
# <a name="keyboard-and-mouse-hid-client-drivers"></a>キーボードとマウスの HID クライアント ドライバー

> [!NOTE]
> このトピックでは、HID クライアント キーボードとマウス用のドライバーを作成している開発者です。 マウスまたはキーボードを修正する場合を参照してください。
>
> - [マウス、タッチパッド、およびキーボードの Windows での問題](https://support.microsoft.com/help/17417/windows-mouse-touchpad-keyboard-problems)
> - [正しく動作しないワイヤレス マウスをトラブルシューティングします。](https://support.microsoft.com/help/321122/troubleshoot-a-wireless-mouse-that-does-not-function-correctly)

このトピックでは、キーボードとマウスの HID クライアント ドライバーについて説明します。 キーボードとマウスは、HID Usage テーブルで標準化され、Windows オペレーティング システムで実装された HID クライアントの最初のセットを表します。

キーボードとマウスの HID クライアント ドライバーは、マッパーのドライバーを非表示の形式で実装されます。 HID ドライバーは、非-HID クラス ドライバーと HID クラス ドライバーの間の I/O 要求の双方向のインターフェイスを提供するカーネル モード WDM フィルター ドライバーです。 マッパーのドライバーでは、他の 1 つの I/O 要求とデータ プロトコルがマップされます。

Windows では、HID キーボード、および HID マウス デバイスをシステムから提供された HID マッパー ドライバーを提供します。

## <a name="architecture-and-overview"></a>アーキテクチャと概要

次の図は、キーボードとマウスまたはタッチパッドの USB デバイスのシステムによって提供されるドライバー スタックを示しています。

![キーボードとマウス ドライバー スタックの図、hid クラス マッパーのキーボードとマウス、キーボードとマウスのクラス ドライバーとドライバー。](images/keyboard-driver-stack.png)

上の図には、次のコンポーネントが含まれています。

- KBDHID.sys – キーボード用 HID クライアント マッパー ドライバー。 HID の使用を既存のキーボード クラス ドライバーとのインターフェイスのスキャン コードに変換します。
- MOUHID.sys – マウスまたはタッチパッド用 HID クライアント マッパー ドライバー。 HID の使用をマウス コマンドに変換します (X Y、ボタン、ホイール/)、既存のキーボード クラス ドライバーとのインターフェイス。
- KBDCLASS.sys – キーボード クラス ドライバーは、安全な方法でのキーボードとキーパッド、システム上のすべての機能を保持します。
- MOUCLASS.sys –、マウスのクラス ドライバーはすべてのマウスの機能/システム上のタッチパッドします。 ドライバーでは、絶対と相対の両方のポインティング デバイスをサポートします。 これは別の Windows でドライバーによって管理されるよう、タッチ スクリーン用のドライバーではありません。

システムでは、次のようにドライバー スタックを作成します。

- トランスポート スタックは、接続されている各 HID デバイスの物理デバイス オブジェクト (PDO) を作成し、順番 HID クラス ドライバーが読み込まれます、適切なトランスポートの HID ドライバーを読み込みます。
- HID クラス ドライバーは、キーボードまたはマウス TLC ごとの PDO を作成します。 複雑な HID デバイス (1 つ以上の TLC) HID クラス ドライバーによって作成された複数の Pdo として公開されます。 たとえば、統合のマウスとキーボードは、標準キーボード コントロールの 1 つのコレクションとマウスの別のコレクションがあります。
- キーボードまたはマウス FDO を適切なドライバーが読み込まれてクライアントのマッパーを非表示にします。
- HID のマッパー ドライバーでは、キーボードとマウスの Fdo を作成し、クラス ドライバーを読み込みます。

重要な注意事項:

- ドライバーのベンダーは、キーボードとマウス サポートされている HID の使用と最上位レベルのコレクションに対応している必要はありません。
- ベンダーは、これら特定 TLC の機能の alter/強化するために、HID スタック内のフィルター ドライバーを必要に応じて指定可能性があります。
- ベンダーは、ベンダー固有で、ベンダー、hid クライアントとデバイスの間の独自のデータを交換するには、個別の TLCs を作成する必要があります。 しない限り、フィルター ドライバーを使用しないように重要です。
- システムでは、すべてのキーボードとマウス コレクションを排他的に使用が開きます。
- システムでは、キーボードを無効にするか有効にできないようにします。
- システムでは、水平、垂直ホイールのスムーズ スクロール機能をサポートします。

## <a name="driver-guidance"></a>ドライバー ガイダンス

マイクロソフトでは、ドライバーを書く ihv 向けの次のガイダンスを提供します。

1. フィルター ドライバーや新しい HID クライアント ドライバーの形式で追加のドライバーを追加するドライバー開発者が許可されます。 条件を次に示します。
    1. ドライバーをフィルタ リングします。ドライバー開発者向けで、ことを確認します、付加価値ドライバーのフィルター ドライバーし、は置き換えられません (またはの代わりに使用)、入力のスタック内の既存の Windows HID ドライバー。
        - フィルター ドライバーは、次のシナリオで使用できます。
            - Kbdhid/mouhid を上部のフィルターとして
            - Kbdclass/mouclass を上部のフィルターとして
        - フィルター ドライバーが_いない_HIDCLASS およびトランスポートの HID ミニドライバー間のフィルターとしてお勧めします。

    2. 関数のドライバー:または仕入先を作成できます (フィルター ドライバーの場合) ではなく関数ドライバー仕入先については、(必要な場合は、ユーザー モード サービス) で特定の HID Pdo。

        関数のドライバーは、次のシナリオで使用できます。

        - 特定のベンダのハードウェア上でのみを読み込む

    3. トランスポート ドライバー:Windows チームでは、書き込み/維持するために複雑なドライバーは、追加のトランスポートの HID ミニドライバーを作成することはできません。 パートナーが SoC システムでは特に、新しいトランスポートの HID ミニドライバーを作成する場合、理由を理解し、ドライバーは正しく開発されていることを確認する詳細なアーキテクチャ レビューをお勧めします。

2. ドライバー開発者は、ドライバー フレームワーク (KMDF または UMDF) を利用し、フィルター ドライバーの WDM に依存しません。
3. ドライバー開発者向けには、そのサービスとドライバー スタック間ユーザー カーネルの遷移の数を削減する必要があります。
4. ドライバー開発者は、キーボード、およびタッチパッドの両方の機能 (エンドユーザー (デバイス マネージャー) または PC の製造元によって調整可能) を使用してシステムをスリープ解除する機能を確認してください。 さらに SoC システムでは、これらのデバイスは、システムは、S0 を動作状態では、そのコンピューター自体を低電源状態からウェイクできるある必要があります。
5. ドライバー開発者向けでは、自社のハードウェアが電力を効率的に管理を確認してください。
    - デバイスは、デバイスがアイドル状態のとき、その最下位の電力状態に移動できます。
    - システム (たとえば、スタンバイ (S3) またはコネクト スタンバイ) は、低電力状態にあるときにデバイスが省電力状態にします。

## <a name="keyboard-layout"></a>キーボード レイアウト

A*キーボード レイアウト*完全 Microsoft Windows 2000 およびそれ以降のバージョンのキーボードの入力の特性について説明します。 たとえば、キーボード レイアウトは、言語、キーボードの種類とバージョン、修飾子、スキャン コード、およびなどを指定します。

キーボード レイアウトについては、次を参照してください。

- キーボードのヘッダー ファイル、kdb.h で、Windows ドライバー開発キット (DDK)、キーボード レイアウトに関する一般的な情報を記述します。

- サンプルのキーボード[レイアウト](https://go.microsoft.com/fwlink/p/?linkid=256128)します。

特定のキーボードのレイアウトを表示するのを参照してください。 [Windows キーボードのレイアウト](https://docs.microsoft.com/globalization/windows-keyboard-layouts)します。

キーボード レイアウトの周りの詳細、コントロール パネル を参照してください。\\時計、言語および地域\\言語。

## <a name="supported-buttons-and-wheels-on-mice"></a>サポートされているボタンやマウスのホイール

次の表は、Windows オペレーティング システムのさまざまなクライアントのバージョン間でサポートされる機能を識別します。

| 機能                                               | Windows XP             | Windows Vista          | Windows 7              | Windows 8 以降    |
|-------------------------------------------------------|------------------------|------------------------|------------------------|------------------------|
| 1 ~ 5 をボタンします。                                           | (P/2 & HID) のサポート  | (Ps/2 & HID) のサポート | (Ps/2 & HID) のサポート | (Ps/2 & HID) のサポート |
| 垂直スクロール ホイール                                 | (Ps/2 & HID) のサポート | (Ps/2 & HID) のサポート | (Ps/2 & HID) のサポート | (Ps/2 & HID) のサポート |
| 水平スクロールのホイール                               | サポートされない          | サポートされている (HID のみ)    | サポートされている (HID のみ)    | サポートされている (HID のみ)    |
| スムーズ スクロール ホイールをサポート (水平方向および垂直方向) | サポートされない          | 部分的にサポートされています       | サポートされている (HID のみ)   | サポートされている (HID のみ)   |

### <a name="activating-buttons-4-5-and-wheel-on-ps2-mice"></a>Ps/2 マウスのホイール ボタン 4 ~ 5 のアクティブ化

新しい 4 と 5 つのボタンをアクティブ化 + ホイールのモードを Windows で使用されるメソッドは、3 番目のボタンと IntelliMouse と互換性のあるマウスのホイールをアクティブ化に使用する方法の拡張機能。

- これは実現し、レートを設定、レポート連続して 200 レポート/秒、100 をレポート/秒、3 ボタン ホイール モードにし、80 のレポートを最初に、マウスを設定/2 番目、およびマウスから ID を読み取るします。 このシーケンスが完了したときに、マウスは、ID が 3 を報告する必要があります。
- レポートのレート連続して 200 レポート/秒、しを 200 レポート/秒もう一度、5 つのボタンのホイール モードにし、80 のレポートを次に、マウスを設定/2 番目、およびマウスから ID を読み取るします。 このシーケンスが完了すると、5 つのボタンのホイール マウスは、(一方、IntelliMouse と互換性のある 3 ボタン ホイール マウスには、ID が 3 のレポートもは) ID 4 を報告する必要があります。

これは ps/2 マウスのみに適用し、(HID マウスは、レポート記述子の正確な使用状況をレポートする必要があります)、HID マウスには適用されませんに注意してください。

#### <a name="standard-ps2-compatible-mouse-data-packet-format-2-buttons"></a>標準的な PS/2 と互換性のあるマウス データ パケット形式 (2 つのボタン)

| バイト | D7    | D6    | D5    | D4    | D3  | D2  | D1  | D0  | Comment                          |
|------|-------|-------|-------|-------|-----|-----|-----|-----|----------------------------------|
| 1    | Yover | 付属のクロスオーバ | Ysign | Xsign | Tag | M   | R   | L   | X または Y overvlows、記号のボタン |
| 2    | X7    | X6    | X5    | X4    | X3  | X2  | X1  | X0  | データのバイト x                      |
| 3    | Y7 です。 ここ    | Y6    | Y5    | Y4    | Y3  | Y2  | Y1  | Y0  | Y のデータのバイト数                     |

> [!NOTE]
> Windows マウス ドライバーでは、オーバーフロー ビットはチェックされません。 オーバーフローが発生した場合、マウス最大符号付きの変位値が送信する必要があります。

#### <a name="standard-ps2-compatible-mouse-data-packet-format-3-buttons--verticalwheel"></a>標準 PS/2 と互換性のあるマウス データ パケット形式 (3 ボタン + VerticalWheel)

| バイト | D7  | D6  | D5    | D4    | D3  | D2  | D1  | D0  | Comment                     |
|------|-----|-----|-------|-------|-----|-----|-----|-----|-----------------------------|
| 1    | 0   | 0   | Ysign | Xsign | 1   | M   | R   | L   | X と Y の記号と M/R/L ボタン |
| 2    | X7  | X6  | X5    | X4    | X3  | X2  | X1  | X0  | データのバイト x                 |
| 3    | Y7 です。 ここ  | Y6  | Y5    | Y4    | Y3  | Y2  | Y1  | Y0  | Y のデータのバイト数                |
| 4    | Z7  | Z6  | Z5    | Z4    | Z3  | Z2  | Z1  | Z0  | Z ホイール/データのバイト           |

#### <a name="standard-ps2-compatible-mouse-data-packet-format-5-buttons--verticalwheel"></a>標準 PS/2 と互換性のあるマウス データ パケット形式 (5 ボタン + VerticalWheel)

| バイト | D7  | D6  | D5    | D4    | D3  | D2  | D1  | D0  | Comment                               |
|------|-----|-----|-------|-------|-----|-----|-----|-----|---------------------------------------|
| 1    | 0   | 0   | Ysign | Xsign | 1   | M   | R   | L   | X と Y の記号と M/R/L ボタン           |
| 2    | X7  | X6  | X5    | X4    | X3  | X2  | X1  | X0  | データのバイト x                           |
| 3    | Y7 です。 ここ  | Y6  | Y5    | Y4    | Y3  | Y2  | Y1  | Y0  | Y のデータのバイト数                          |
| 4    | 0   | 0   | B5    | B4    | Z3  | Z2  | Z1  | Z0  | Z/ホイール データと手順 4. と 5. ボタン |

重要な注意事項:

- IntelliMouse と互換性のある 3 ボタン ホイール モードで使用される 8 ビットではなく 4 つのビット ホイールの 5 ボタン マウスのホイール Z/データが削減されたことに注意してください。 この短縮はファクトのことは、ホイールを通常を生成できません、範囲 + 7/8 を超える値の間に特定の割り込みによって実現されます。 Windows マウスのドライバーは署名は、マウスが 3 ボタン ホイール モードで動作するときに、マウスが、5 つのボタンのホイール モードとフル Z/ホイール データ バイトがときに、4 つの Z/ホイール データ ビットを拡張します。
- 4 および 5 に、ボタンは、WM にマップされます\_APPCOMMAND のメッセージをアプリに対応して\_戻る ボタンとアプリ\_転送します。

### <a name="devices-not-requiring-vendor-drivers"></a>デバイス ドライバーのベンダーを必要としません。

ドライバーのベンダーは、次のデバイス必要ないです。

- HID 標準に準拠しているデバイス。
- キーボード、マウス、またはゲーム ポートのデバイスのシステムが指定した非-HIDClass ドライバーが運用します。

## <a name="kbfiltr-sample"></a>Kbfiltr サンプル

Kbfiltr は Kbdclass、キーボード デバイスと I8042prt、PS/2 スタイル キーボードの機能のドライバーのシステム クラスのドライバーで使用するように設計します。 Kbfiltr は、I/O 要求をフィルター処理する方法と Kbdclass と I8042prt の動作を変更するコールバック ルーチンを追加する方法について説明します。

Kbfiltr 操作の詳細については、次を参照してください。

- Ntddkbd.h WDK ヘッダー ファイルです。

- サンプル[Kbfiltr](https://go.microsoft.com/fwlink/p/?linkid=256125)ソース コード。

### <a name="kbfiltr-ioctls"></a>Kbfiltr Ioctl

<table>
<tr>
<th>制御コード</th>
<th>説明</th>
</tr>
<tr>
<td>
<p>
&lt;/Mshelp:link tabindex =「0」keywords="hid.ioctl_internal_i8042_hook_keyboard"&gt;<b>IOCTL_INTERNAL_I8042_HOOK_KEYBOARD</b>&lt;/MSHelp:link&gt;
</p>
</td>
<td>
<p>IOCTL_INTERNAL_I8042_HOOK_KEYBOARD 要求は、次を行います。</p>
<ul>
<li>
<p>I8042prt キーボードの初期化ルーチンに初期化のコールバック ルーチンを追加します。</p>
</li>
<li>
<p>I8042prt キーボード ISR に ISR のコールバック ルーチンを追加します。</p>
</li>
</ul>
<p>初期化と ISR コールバックは省略可能と PS/2 スタイル キーボード デバイスを上位レベルのフィルター ドライバーによって提供されます。</p>
<p>I8042prt を受信した後、 &lt;/mshelp:link tabindex =「0」keywords="hid.ioctl_internal_keyboard_connect2"&gt;<b>IOCTL_INTERNAL_KEYBOARD_CONNECT</b>&lt;/MSHelp:link&gt;要求、キーボード デバイス スタックの先頭には同期 IOCTL_INTERNAL_I8042_HOOK_KEYBOARD 要求を送信します。</p>
<p>Kbfiltr がフック キーボードの要求を受け取った後 Kbfiltr には、次のように、要求がフィルター処理されます。</p>
<ul>
<li>
<p>上位レベルのデバイス オブジェクト、初期化のコールバックをへのポインター、ISR コールバックへのポインターのコンテキストを含む、Kbfiltr に渡される上位レベルの情報を保存します。</p>
</li>
<li>
<p>独自の上位レベルの情報を置き換えられます。</p>
</li>
<li>
<p>Kbfiltr ISR コールバックを使用するコールバックを I8042prt およびポインターのコンテキストを保存します。</p>
</li>
</ul>
</p>
</dd>
</dl>
</td>
</tr>
<tr>
<td>
<p>
&lt;MSHelp:link tabindex="0" keywords="hid.ioctl_internal_keyboard_connect"&gt;<b>IOCTL_INTERNAL_KEYBOARD_CONNECT</b>&lt;/MSHelp:link&gt;
</p>
</td>
<td>
<p>IOCTL_INTERNAL_KEYBOARD_CONNECT 要求は、キーボード デバイスに Kbdclass サービスを接続します。 キーボード デバイスを開く前に、Kbdclass はキーボード デバイス スタックには、この要求を送信します。 </p>
<p>Kbfiltr がキーボードの接続要求を受け取った後 Kbfiltr には、次のように接続要求がフィルター処理されます。</p>
<ul>
<li>
<p>Kbdclass のコピーを保存&lt;/mshelp:link tabindex =「0」keywords="hid.connect_data__kbdclass_"&gt;<b>CONNECT_DATA (Kbdclass)</b>&lt;/MSHelp:link&gt;渡される構造体Kbdclass によってフィルター ドライバー</p>
</li>
<li>
<p>独自の置換クラス ドライバーの接続情報のために情報を接続</p>
</li>
<li>
<p>デバイス スタック IOCTL_INTERNAL_KEYBOARD_CONNECT 要求を送信します。</p>
</li>
</ul>
<p>要求が成功しなかった場合、Kbfiltr は、該当するエラー状態で要求を完了します。</p>
<p>Kbfiltr の操作を補足するフィルター サービス コールバック ルーチンのテンプレートを提供する&lt;/mshelp:link tabindex =「0」keywords="hid.keyboardclassservicecallback"&gt;<b>KeyboardClassServiceCallback</b> &lt;/MSHelp:link&gt;、Kbdclass クラス サービス コールバック ルーチン。 フィルター サービスのコールバックは、デバイスの入力バッファーからクラスのデータ キューに転送される入力データをフィルター処理できます。 </p>
<dl>
<dd>
</p>
</dd>
</dl>
</td>
</tr>
<tr>
<td>
<p>
&lt;MSHelp:link tabindex="0" keywords="hid.ioctl_internal_keyboard_disconnect"&gt;<b>IOCTL_INTERNAL_KEYBOARD_DISCONNECT</b>&lt;/MSHelp:link&gt;
</p>
</td>
<td>
<p>IOCTL_INTERNAL_KEYBOARD_DISCONNECT 要求が STATUS_NOT_IMPLEMENTED の状態で完了します。 プラグ アンド プレイ キーボードの追加またはプラグ アンド プレイ マネージャーによって削除されたことに注意してください。</p>
</td>
</tr>
</table>

<p>他のすべてのデバイス制御要求には、Kbfiltr は現在 IRP スタックをスキップし、さらに処理することがなく、デバイス スタック ダウン要求を送信します。</p>
<p><b>Kbfiltr によって実装されるコールバック ルーチン</b></p>
<p>
<ul>
<li><b>KbFilter_InitializationRoutine</b>

     (see &lt;MSHelp:link tabindex="0" keywords="hid.pi8042_keyboard_initialization_routine"&gt;<b>PI8042_KEYBOARD_INITIALIZATION_ROUTINE</b>&lt;/MSHelp:link&gt;)<p><b>
          KbFilter_InitializationRoutine</b> is not needed if I8042prt's default initialization of a keyboard is sufficient.</p>
<p>I8042prt 呼び出し<b>KbFilter_InitializationRoutine</b>とき、キーボードを初期化します。 既定のキーボードの初期化には、次の操作が含まれています: キーボードのリセット、キーボードの速度と遅延を設定し、発光ダイオード (LED) を設定します。
<pre><code>
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

<em>/

NTSTATUS KbFilter_InitializationRoutine(
  <em>In</em>  PDEVICE_OBJECT          DeviceObject,
  <em>In</em>  PVOID                   SynchFuncContext,
  <em>In</em>  PI8042_SYNCH_READ_PORT  ReadPort,
  <em>In</em>  PI8042_SYNCH_WRITE_PORT WritePort,
  <em>Out</em> PBOOLEAN                TurnTranslationOn
);
</code></pre>
</p>
</li>
<li><b>KbFilter_IsrHook</b>

     (see &lt;MSHelp:link tabindex="0" keywords="hid.pi8042_keyboard_isr"&gt;<i>PI8042_KEYBOARD_ISR</i>&lt;/MSHelp:link&gt;)<p>This callback is not needed if the default operation of I8042prt is sufficient.</p>
<p>I8042prt キーボード ISR 呼び出し<b>KbFilter_IsrHook</b>後、割り込みを検証し、スキャン コードを読むことです。 </p>
<p><b>KbFilter_IsrHook</b> I8042prt キーボード ISR. の IRQL でカーネル モードで実行</p>
<pre><code>
/</em>
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

<em>/

KbFilter_IsrHook KbFilter_IsrHook(
  <em>In</em>    PDEVICE_OBJECT       DeviceObject,
  <em>In</em>    PKEYBOARD_INPUT_DATA CurrentInput,
  <em>In</em>    POUTPUT_PACKET       CurrentOutput,
  <em>Inout</em> UCHAR                StatusByte,
  <em>In</em>    PUCHAR               DataByte,
  <em>Out</em>   PBOOLEAN             ContinueProcessing,
  <em>In</em>    PKEYBOARD_SCAN_STATE ScanState
);

);
</code></pre>
</li>
<li><b>KbFilter_ServiceCallback</b> (を参照してください&lt;/mshelp:link tabindex =「0」keywords="hid.kbdclass_class_service_callback_routine"&gt;<i>PSERVICE_CALLBACK_ROUTINE</i>&lt;/MSHelp:リンク&gt;)<p>ドライバーの関数呼び出しの ISR ディスパッチの完了ルーチン<b>KbFilter_ServiceCallback</b>、しのキーボード クラス ドライバーの実装を呼び出す&lt;/mshelp:link tabindex =「0」keywords="hid.kbdclass_class_service_callback_routine"&gt;<i>PSERVICE_CALLBACK_ROUTINE</i>&lt;/MSHelp:link&gt;します。 仕入先には、デバイスの入力バッファーからクラスのデータ キューに転送される入力データを変更するフィルター サービスのコールバックを実装できます。 たとえば、コールバックできます削除、変換、またはデータを挿入します。
<pre><code>
/</em>
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

);
</code></pre>
</p>

## <a name="moufiltr-sample"></a>Moufiltr サンプル

Moufiltr は Mouclass、Windows 2000 以降のバージョンと I8042prt、関数のドライバーを Windows 2000 以降を使用するスタイル 2 PS/マウスを使用するマウス デバイスのシステム クラスのドライバーで使用するように設計します。 Moufiltr では、I/O 要求をフィルター処理し、Mouclass と I8042prt の動作を変更するコールバック ルーチンを追加する方法を示します。

<table>
<tr>
<th>制御コード</th>
<th>説明</th>
</tr>
<tr>
<td>
<p>
&lt;/Mshelp:link tabindex =「0」keywords="hid.ioctl_internal_i8042_hook_mouse"&gt;<b>IOCTL_INTERNAL_I8042_HOOK_MOUSE</b>&lt;/MSHelp:link&gt;
</p>
</td>
<td>
<p>IOCTL_INTERNAL_I8042_HOOK_MOUSE 要求 I8042prt マウス ISR. ISR のコールバック ルーチンを追加します ISR コールバックは省略可能で、マウスの上位レベルのフィルター ドライバーによって提供されます。</p>
<p>I8042prt が受信した後、この要求を送信する&lt;/mshelp:link tabindex =「0」keywords="hid.ioctl_internal_mouse_connect2"&gt;<b>IOCTL_INTERNAL_MOUSE_CONNECT</b>&lt;/MSHelp:link&gt;要求。 I8042prt は、マウス デバイス スタックの一番上に同期 IOCTL_INTERNAL_I8042_HOOK_MOUSE 要求を送信します。</p>
<p>Moufiltr がフック マウスの要求を受信した後は、次のように、要求がフィルター処理されます。</p>
<ul>
<li>
<p>上位レベルのデバイス オブジェクトと、ISR コールバックへのポインターのコンテキストを含む、Moufiltr に渡される上位レベルの情報を保存します。</p>
</li>
<li>
<p>独自の上位レベルの情報を置き換えられます。</p>
</li>
<li>
<p>Moufiltr ISR コールバックを使用するコールバックを I8042prt およびポインターのコンテキストを保存します。</p>
</li>
</ul>
<p>この要求とコールバックの詳細については、次のトピックを参照してください。</p>
<dl>
<dd>
<p>
&lt;/Mshelp:link tabindex =「0」keywords="hid.i8042prt_callback_routines"&gt;I8042prt コールバック ルーチン&lt;/MSHelp:link&gt;
</p>
</dd>
<dd>
<p>
&lt;/Mshelp:link tabindex =「0」keywords="hid.moufiltr_callback_routines"&gt;Moufiltr コールバック ルーチン&lt;/MSHelp:link&gt;
</p>
</dd>
</dl>
</td>
</tr>
<tr>
<td>
<p>
&lt;/Mshelp:link tabindex =「0」keywords="hid.ioctl_internal_mouse_connect"&gt;<b>IOCTL_INTERNAL_MOUSE_CONNECT</b>&lt;/MSHelp:link&gt;
</p>
</td>
<td>
<p>IOCTL_INTERNAL_MOUSE_CONNECT 要求は、マウス デバイスに Mouclass サービスを接続します。</p>
</td>
</tr>
<tr>
<td>
<p>
&lt;/Mshelp:link tabindex =「0」keywords="hid.ioctl_internal_mouse_disconnect"&gt;<b>IOCTL_INTERNAL_MOUSE_DISCONNECT</b>&lt;/MSHelp:link&gt;
</p>
</td>
<td>
<p>IOCTL_INTERNAL_MOUSE_DISCONNECT 要求は、Moufiltr STATUS_NOT_IMPLEMENTED のエラー状態で終了されます。</p>
</td>
</tr>
</table>
<p> </p>
</p>
<p>その他のすべての要求は、Moufiltr は現在 IRP スタックをスキップし、さらに処理することがなく、デバイス スタック ダウン要求を送信します。</p>
<p><b>Kbfiltr によって実装されるコールバック ルーチン</b></p>
<dl>
<dd><b>MouFilter_IsrHook</b> (を参照してください&lt;/mshelp:link tabindex =「0」keywords="hid.pi8042_mouse_isr"&gt;<i>PI8042_MOUSE_ISR</i>&lt;/MSHelp:link&gt;)<p>
<pre><code>
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
</code></pre>
</p>
<p>A <b>MouFilter_IsrHook</b> I8042prt の既定の操作のための十分な場合、コールバックは必要ありません。

I8042prt マウス ISR 呼び出し<b>MouFilter_IsrHook</b>割り込みを検証後します。

マウスをリセットするには、I8042prt は運用の下位の MOUSE_RESET_SUBSTATE 列挙値によって識別されますがそれぞれ 1 つのシーケンスについて説明します。 I8042prt がマウスおよび対応するマウスをリセットする方法の詳細については、下位状態をリセットし、ntdd8042.h MOUSE_RESET_SUBSTATE のドキュメントを参照してください。

<b>MouFilter_IsrHook</b> I8042prt マウス ISR. の IRQL でカーネル モードで実行

</p>
</dd>
<dd><b>MouFilter_ServiceCallback</b> (を参照してください&lt;/mshelp:link tabindex =「0」keywords="hid.kbdclass_class_service_callback_routine"&gt;<i>PSERVICE_CALLBACK_ROUTINE</i>&lt;/MSHelp: リンク&gt;)<p>
<pre><code>
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
</code></pre>
</p>
<p>I8042prt の ISR DPC MouseClassServiceCallback を呼び出して、MouFilter_ServiceCallback を呼び出します。 デバイスの入力バッファーからクラスのデータ キューに転送される入力データを変更するのには、フィルター サービスのコールバックを構成できます。 たとえば、コールバックできます削除、変換、またはデータを挿入します。

</p>
