---
title: Bluetooth のホスト オプションのサポート
ms.assetid: 7AA53797-F8DC-4FA6-9A19-E20289AF50CA
description: Windows で Bluetooth ホスト オプションのサポートに関する質問と回答の一覧を示します
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e03f6b403d7dd73869326dc0d9fa2b69e3934c66
ms.sourcegitcommit: 1a5d7884cec9dd8d2b85242bee78b56a1cf8e4c9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/01/2019
ms.locfileid: "58761857"
---
# <a name="bluetooth-host-radio-support"></a>Bluetooth ホストの無線のサポート

次の一覧は、Bluetooth 無線サポート Q & a:

- [Bluetooth のホスト コント ローラーの Windows でサポートされています](#bluetooth-host-controllers-supported-in-windows)
- [Windows がデバイス ID (Windows Vista) に一致しない場合は読み込みに Bluetooth スタックの強制](#forcing-the-bluetooth-stack-to-load-if-windows-cannot-match-the-device-id-(windows-vista))
- [Windows Vista での Bluetooth ラジオのインボックス サポートを確認する方法](#how-to-ensure-in-box-support-for-bluetooth-radios-in-windows-vista)
- [サード パーティ製の INF ファイルがマイクロソフトによって定義されたクラス GUID を使用するかどうか](#whether-third-party-inf-files-should-use-the-microsoft-defined-class-guid)
- [コントロール パネルの Bluetooth アプリケーションが Windows 7 で不足している理由](#why-the-control-panel-bluetooth-application-is-missing-in-windows-7)
- [Bluetooth アイコンがタスク バーに表示されない理由](#why-the-bluetooth-icon-does-not-appear-in-the-taskbar)
- [Windows は、Bluetooth 無線ファームウェアの更新プログラムをサポートします。](#windows-support-for-bluetooth-radio-firmware-updates)
- [パススルー コマンドのベンダー固有の Windows のサポート](#windows-support-for-vendor-specific-pass-through-commands)
- [Windows は、ベンダーから提供されたプロファイルをサポートします。](#windows-support-for-vendor-supplied-profiles)
- [Bluetooth のプロファイルと既定で有効になっているプロトコル](#bluetooth-profiles-and-protocols-that-are-enabled-by-default)
- [グループ ポリシーが Bluetooth ラジオのインストールをブロックする方法](#how-group-policy-can-block-bluetooth-radio-installation)
- [Windows 8 および Windows 8.1 によって発行されたデバイス ID のプロファイル レコードを変更する方法](#how-to-change-the-device-id-profile-record-published-by-windows-8-and-windows-8.1)

## <a name="bluetooth-host-controllers-supported-in-windows"></a>Bluetooth のホスト コント ローラーの Windows でサポートされています

、Windows では、Bluetooth 無線を外付けドングルとしてパッケージ化またはコンピューター内に埋め込まれたできますが、その 1 つのコンピューターの USB ポートに接続する必要があります。 PC カード インターフェイスまたは Windows 7 および Windows Vista に含まれている Bluetooth スタックが Bluetooth 無線経由の接続、PCI、I2C、シリアル Secure Digital I/O (SDIO)、コンパクト フラッシュをサポートしていません。 Windows 8 および Windows 8.1 では、サード パーティ製のバス ドライバーを使用してラジオを代替のトランスポートを経由して接続を追加できます。 拡張可能なトランスポートのセクションを参照してください、 [Bluetooth デバイス参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_bltooth/)詳細についてはします。

## <a name="forcing-the-bluetooth-stack-to-load-if-windows-cannot-match-the-device-id-windows-vista"></a>Windows がデバイス ID (Windows Vista) に一致しない場合は読み込みに Bluetooth スタックの強制

新しい Bluetooth 無線は、デバイスの Windows に含まれている Bluetooth INF (Bth.inf) 内の Id のいずれかとも一致しない可能性があります。 これは Windows がデバイスの Bluetooth スタックをロードすることを防ぎます。 Ihv は、次の方法のいずれかで、ラジオがネイティブの Bluetooth スタックで動作するを確認してください。

- ラジオ Bth.inf を参照する、INF を作成します。 Bluetooth 無線のベンダー固有の INF ファイルの例は、次を参照してください[付録 b:。Windows Vista で使用するため、ベンダー提供の INF ファイルの例](bluetooth-faq--appendix-b.md)します。
- 適切な互換性があり、subcompatible ID を指定するデバイスのファームウェアで拡張の互換性の OS の ID 記述子を格納します。 については、互換性 ID OS ディスクリプターを拡張を参照してください。 [Microsoft OS ディスクリプター](https://go.microsoft.com/fwlink/p/?linkid=308932)します。
- 強制的に読み込む Bluetooth スタック

次の手順は、デバイス マネージャーを使用して、新しいオプションを読み込む Bluetooth スタックを強制する方法をまとめたものです。

1. コントロール パネルのデバイス マネージャーのアプリケーションを実行し、デバイスの一覧で、Bluetooth 無線を識別します。
2. ドライバー ソフトウェアの更新ウィザードを実行するには、Bluetooth 無線の項目を右クリックして**ドライバー ソフトウェアの更新**します。
3. ウィザードを使用して、強制的に Bluetooth スタックをインストールします。

この手順の詳細については、次を参照してください[付録 a:。Windows Vista の新しいハードウェアに付属の Bluetooth ドライバーをインストールする方法](bluetooth-faq--appendix-a.md)します。

## <a name="how-to-ensure-in-box-support-for-bluetooth-radios-in-windows-vista"></a>Windows Vista での Bluetooth ラジオのインボックス サポートを確認する方法

Ihv は、Windows で box サポートに、Bluetooth 無線があることを確認するには、次の手順を実行する必要があります。

- 無線拡張互換性 ID の OS の機能の記述子をサポートしていることを確認します。 詳細については、[Microsoft OS ディスクリプター](https://go.microsoft.com/fwlink/p/?linkid=617154)を参照してください。
- Windows 認定プログラムの承認、Bluetooth 無線ハードウェアと関連付けられている INF ファイルを取得します。 Bluetooth 無線のベンダー固有の INF ファイルの例は、次を参照してください[付録 b:。Windows Vista で使用するため、ベンダー提供の INF ファイルの例](bluetooth-faq--appendix-b.md)します。
- パートナー センターを使用して、INF ファイルを Windows Update を通じて使用できるようにするには

Windows Vista のインボックス Bth.inf ファイルへの無線を追加することはありません。

## <a name="whether-third-party-inf-files-should-use-the-microsoft-defined-class-guid"></a>サード パーティ製の INF ファイルがマイクロソフトによって定義されたクラス GUID を使用するかどうか

Ihv は、インボックス Bluetooth INF ファイル (Bth.inf) を参照する INF ファイルのみの Bluetooth デバイスに Microsoft によって定義されたクラスのグローバル一意識別子 (GUID) ({e0cbf06c cd8b 4647 bb8a 263b43f0f974}) を使用してください。 これは、デバイスが、ネイティブ Windows 共同インストーラー、サービス、および通知エリア アイコンを使用していることを意味します。 Bluetooth スタックを実装する Ihv は、ベンダー固有クラス GUID を作成し、WLK テスト ツールを使用して、スタックが未分類の Windows 認定プログラムに準拠していることを確認する必要があります。

## <a name="why-the-control-panel-bluetooth-application-is-missing-in-windows-7"></a>コントロール パネルの Bluetooth アプリケーションが Windows 7 で不足している理由

Windows 7 では、コントロール パネルの Bluetooth アプリケーションがデバイスとプリンターに組み込まれます。 したがって、Bluetooth 無線の設定を調整して、Bluetooth のデバイスを管理する、新しい Bluetooth の追加デバイスのみ実行できますからデバイスとプリンター内。

## <a name="why-the-bluetooth-icon-does-not-appear-in-the-taskbar"></a>Bluetooth アイコンがタスク バーに表示されない理由

Bluetooth のアイコンがタスク バーに表示されない場合、次の理由の 1 つ以上が考えられます。

- Bluetooth 無線がになっています。
- Bluetooth 無線がエミュレーション モードです。
- **Bluetooth 設定**ダイアログ ボックスで、 **Bluetooth アイコン、通知領域に表示する** チェック ボックスが選択されていません。

## <a name="windows-support-for-bluetooth-radio-firmware-updates"></a>Windows は、Bluetooth 無線ファームウェアの更新プログラムをサポートします。

現時点では、Windows に含まれている Bluetooth スタックはファームウェアの更新プログラムを直接サポートされません。 ただし、Bluetooth 無線が USB ポート経由で接続して、Windows は、USB デバイス ファームウェアの更新 (DFU) 仕様に準拠しているファームウェアの更新プログラムをサポートしています。 Ihv は、ファームウェアの更新と再起動、ラジオ、DFU インターフェイスを介して、Bluetooth 無線通信を行うユーザー モード ユーティリティを作成できます。

## <a name="windows-support-for-vendor-specific-pass-through-commands"></a>パススルー コマンドのベンダー固有の Windows のサポート

Windows 8.1、Windows 8、Windows 7、および Windows Vista SP2 には、ベンダー固有のパススルー コマンドのサポートが含まれます。 これらのカーネル モード インターフェイスは、WDK に記載されています。

## <a name="windows-support-for-vendor-supplied-profiles"></a>Windows は、ベンダーから提供されたプロファイルをサポートします。

Windows 8.1、Windows 8、Windows 7、および Windows Vista は、ベンダーから提供された Bluetooth のプロファイルをサポートします。 ただし、Windows XP されていません。 INF ファイル (Bth.inf) でのボックスには、Bluetooth SIG によって標準化されたそれらのプロファイル用の Guid が含まれます。

ユーザーのコンピューターに Bluetooth デバイスとペアにデバイスのプロファイルが Bth.inf に記載されているプロファイルと比較されます。 デバイスのプロファイルには、それらのプロファイルのいずれかと一致しません、ユーザーは適切なベンダのソフトウェアを提供することを確認するダイアログ ボックスを表示します。

ベンダー固有のプロファイルをベンダーは、独自の GUID を使用し、ベンダー固有の INF ファイルで参照する必要があります。 この INF ファイルを使用して、インクルードを使用できます、ディレクティブ、適切な Bth.inf セクションとディレクティブを参照する必要があります。 ベンダー固有の INF ファイルの例は、次を参照してください[付録 b:。Windows Vista で使用するため、ベンダー提供の INF ファイルの例](bluetooth-faq--appendix-b.md)します。

## <a name="bluetooth-profiles-and-protocols-that-are-enabled-by-default"></a>Bluetooth のプロファイルと既定で有効になっているプロトコル

彼は Windows に付属する Bluetooth スタックは、いくつかの Bluetooth プロファイルのみのインボックス サポートを提供します。 ベンダーは、USB および PCI の場合と同じ他の Bluetooth プロファイルをサポートするために必要なサービスを実装する必要があります。 Windows が既定で有効になっている Bluetooth のプロファイルを使用できます: サポートされているプロファイルと呼ばれる: 物理デバイス オブジェクト (Pdo) を生成します。 これにより、プロファイルを有効にするには、必要なドライバーの既定の読み込みができます。 SupportedServices と UnsupportedServices の値を調べることで、レジストリでサポートされているプロファイルを識別することができます、 **HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\サービス\\Bthport\\パラメーター**キー。

> [!NOTE]
> Bthport キーは、Bluetooth デバイスをインストールした後にのみ、レジストリに追加されます。

次の表は、Windows をサポートする Bth.inf でプロファイルを一覧表示します。

|サービス ID|説明|
|----|----|
|{00001101-0000-1000-8000-00805f9b34fb}|SPP|
|{00001103-0000-1000-8000-00805f9b34fb}|DUN
|{00001124-0000-1000-8000-00805f9b34fb}|HID|
|{00001126-0000-1000-8000-00805f9b34fb}|HCRP|

### <a name="windows-xp-bluetooth-profiles"></a>Windows XP の Bluetooth のプロファイル

次の表には、サポートされていない Bluetooth のプロファイルとプロトコルが一覧表示します。 このコンテキストで「サポートされていない」ことである Windows の PDO または devnode 生成または新しいハードウェアの追加ウィザードを表示は自動的に注意してください。 そのため、一部のボックスでプロファイルとプロトコルはサポートされていないかのように処理されます。 たとえば、SDP、PDO は必要ありませんが、Bluetooth サービス ID をボックスでプロトコルです。 SDP プロトコルはための PDO 作成されないようにするでサポートされていない Bth.inf としてマークされています。

|サービス ID|インボックス|説明|
|----|----|----|
|{0000110a-0000-1000-8000-00805f9b34fb}|いいえ|オーディオ ソース|
|{0000110c-0000-1000-8000-00805f9b34fb}|いいえ|AV リモート ターゲット|
|{00001001-0000-1000-8000-00805f9b34fb}|いいえ|グループの参照サービス|
|{00001111-0000-1000-8000-00805f9b34fb}|いいえ|Fax サービス|
|{0000111f-0000-1000-8000-00805f9b34fb}|いいえ|ハンズフリー オーディオ ゲートウェイ|
|{00001112-0000-1000-8000-00805f9b34fb}|いいえ|ヘッドセット オーディオ ゲートウェイ|
|{00001104-0000-1000-8000-00805f9b34fb}|いいえ|赤外線モバイル通信 (IRMC) 同期サービス|
|{00001107-0000-1000-8000-00805f9b34fb}|いいえ|IRMC 同期コマンド|
|{00001106-0000-1000-8000-00805f9b34fb}|はい|Obex ファイル転送|
|{00001105-0000-1000-8000-00805f9b34fb}|はい|オブジェクトのプッシュ|
|{00001117-0000-1000-8000-00805f9b34fb}|いいえ|パン グループ アドホック ネットワーク (GN)|
|{00001116-0000-1000-8000-00805f9b34fb}|いいえ|ネットワーク アクセス ポイント (NAP) にパンします。|
|{00001115-0000-1000-8000-00805f9b34fb}|はい|パン U|
|{0000112e-0000-1000-8000-00805f9b34fb}|いいえ|クライアント機器 (外字エディター) サービスの電話帳|
|{0000112f-0000-1000-8000-00805f9b34fb}|いいえ|サーバー機器 (PSE) サービスの電話帳|
|{00001200-0000-1000-8000-00805f9b34fb}|はい|PnP サービス|
|{00001002-0000-1000-8000-00805f9b34fb}|いいえ|パブリック グループの参照サービス|
|{00001000-0000-1000-8000-00805f9b34fb}|はい|SDP|
|{0000112d-0000-1000-8000-00805f9b34fb}|いいえ|Sim のアクセス|

Ihv が自分のデバイス用の PDO を自動的に生成する Windows をしない場合、サービスの GUID サポートされていないサービスの一覧に追加できます。 例については、Bth.inf を参照してください。

## <a name="how-group-policy-can-block-bluetooth-radio-installation"></a>グループ ポリシーが Bluetooth ラジオのインストールをブロックする方法

グループ ポリシーを使用して、Bluetooth 無線のインストールをブロックする方法の詳細については、"禁止されているデバイスのインストールを禁止する のセクションを参照してください[グループ ポリシーと使用状況を制御するデバイスのインストールをステップ バイ ステップ ガイド](https://go.microsoft.com/fwlink/p/?linkid=324335).

Bluetooth 無線の次の互換性のある Id を使用します。

USB\\クラス\_(USB ベースの無線) の E0 MS\_BTHX\_BTHMINI (USB 以外の無線) の

> [!NOTE]
> Bluetooth ドライバーのサポートは、既にインストールされている場合この削除されません。 また、このポリシーは、プレインストールのイメージに適用する必要があります。

## <a name="how-to-change-the-device-id-profile-record-published-by-windows-8-and-windows-81"></a>Windows 8 および Windows 8.1 によって発行されたデバイス ID のプロファイル レコードを変更する方法

デバイス ID のプロファイルでは、リモート デバイスに id 情報を提供するために使用できる SDP レコードを定義します。 以前と現在の Windows バージョンでは、ペアになっているデバイスで公開されているデバイス ID のレコードを使用するがで、汎用の Bluetooth サービスのデバイスに固有のハードウェア Id を提供します。

Windows 8 以降、Windows はリモートの Bluetooth デバイスに Windows 8 デバイスを識別するためにローカルのデバイス ID レコードを発行もします。 Oem が特定の Windows 8 デバイスを特定するのには、既定値を調整できます。 これらの値が、HKLM 下で、次の表のように定義されている\\システム\\CCS\\サービス\\BTHPORT\\パラメーター レジストリ キー。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="odd">
<th align="left"><p>ValueName</p></th>
<th align="left"><p>型</p></th>
<th align="left"><p>説明</p></th>
<th align="left"><p>既定値</p></th>
</tr>
</thead>
<tbody>
<tr class="even">
<td align="left"><p>DIDVendorIDSource</p></td>
<td align="left"><p>DWORD</p></td>
<td align="left"><p>0x01 = Bluetooth SIG 名前空間</p>
<p>0x02 = USB フォーラム名前空間</p></td>
<td align="left"><p>0x01</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DIDVendorID</p></td>
<td align="left"><p>DWORD</p></td>
<td align="left"><p>OEM VendorID の指定</p></td>
<td align="left"><p>0x06-Microsoft のベンダー ID</p></td>
</tr>
<tr class="even">
<td align="left"><p>DIDProductID</p></td>
<td align="left"><p>DWORD</p></td>
<td align="left"><p>指定された ProductID の OEM</p></td>
<td align="left"><p>0x01-Microsoft Windows</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DIDVersion</p></td>
<td align="left"><p>DWORD</p></td>
<td align="left"><p>OEM 指定された製品バージョン</p></td>
<td align="left"><p>0x0800 – Windows 8</p></td>
</tr>
</tbody>
</table>
