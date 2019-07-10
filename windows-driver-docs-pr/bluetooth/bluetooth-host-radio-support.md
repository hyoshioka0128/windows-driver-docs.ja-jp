---
title: Bluetooth のホスト オプションのサポート
ms.assetid: 7AA53797-F8DC-4FA6-9A19-E20289AF50CA
description: Windows で Bluetooth ホスト オプションのサポートに関する質問と回答の一覧を示します
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bb7186d8d86e0ec85c310427359b7ed100cdf4d
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716815"
---
# <a name="bluetooth-host-radio-support"></a>Bluetooth ホストの無線のサポート

このトピックでは、Bluetooth 無線のサポートに関する一般的な質問に対する回答を提供します。

## <a name="bluetooth-host-controllers-supported-in-windows"></a>Bluetooth のホスト コント ローラーの Windows でサポートされています

、Windows では、Bluetooth 無線を外付けドングルとしてパッケージ化またはコンピューター内に埋め込まれたできますが、その 1 つのコンピューターの USB ポートに接続する必要があります。 PC カード インターフェイスまたは Windows 7 および Windows Vista に含まれている Bluetooth スタックが Bluetooth 無線経由の接続、PCI、I2C、シリアル Secure Digital I/O (SDIO)、コンパクト フラッシュをサポートしていません。 Windows 8 および Windows 8.1 では、サード パーティ製のバス ドライバーを使用してラジオを代替のトランスポートを経由して接続を追加できます。 拡張可能なトランスポートのセクションを参照してください、 [Bluetooth デバイス参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_bltooth/)詳細についてはします。

## <a name="forcing-the-bluetooth-stack-to-load-if-windows-cannot-match-the-device-id-windows-vista"></a>Windows がデバイス ID (Windows Vista) に一致しない場合は読み込みに Bluetooth スタックの強制

新しい Bluetooth 無線は、デバイスの Windows に含まれている Bluetooth INF (Bth.inf) 内の Id のいずれかとも一致しない可能性があります。 これは Windows がデバイスの Bluetooth スタックをロードすることを防ぎます。 Ihv は、次の方法のいずれかで、ラジオがネイティブの Bluetooth スタックで動作するを確認してください。

* ラジオ Bth.inf を参照する、INF を作成します。 Bluetooth 無線のベンダー固有の INF ファイルの例は、次を参照してください[付録 b:。Windows Vista で使用するため、ベンダー提供の INF ファイルの例](bluetooth-faq--appendix-b.md)します。
* 適切な互換性があり、subcompatible ID を指定するデバイスのファームウェアで拡張の互換性の OS の ID 記述子を格納します。 については、互換性 ID OS ディスクリプターを拡張を参照してください。 [Microsoft OS ディスクリプター](https://go.microsoft.com/fwlink/p/?linkid=308932)します。
* 強制的に読み込む Bluetooth スタック

次の手順では、デバイス マネージャーを使用して、強制的に新しいオプションを読み込む Bluetooth スタック。

1. コントロール パネルのデバイス マネージャーのアプリケーションを実行し、デバイスの一覧で、Bluetooth 無線を識別します。
2. ドライバー ソフトウェアの更新ウィザードを実行するには、Bluetooth 無線の項目を右クリックして**ドライバー ソフトウェアの更新**します。
3. ウィザードを使用して、強制的に Bluetooth スタックをインストールします。

この手順の詳細については、次を参照してください[付録 a:。Windows Vista の新しいハードウェアに付属の Bluetooth ドライバーをインストールする方法](bluetooth-faq--appendix-a.md)します。

## <a name="ensure-in-box-support-for-bluetooth-radios"></a>Bluetooth ラジオのインボックス サポートを確認します。

Ihv は、Windows で box サポートに、Bluetooth 無線があることを確認するには、次の手順を実行する必要があります。

* 無線拡張互換性 ID の OS の機能の記述子をサポートしていることを確認します。 詳細については、次を参照してください。 [Microsoft OS ディスクリプター](https://docs.microsoft.com/windows-hardware/drivers/usbcon/microsoft-os-1-0-descriptors-specification)します。
* Windows 認定プログラムの承認、Bluetooth 無線ハードウェアと関連付けられている INF ファイルを取得します。 Bluetooth 無線のベンダー固有の INF ファイルの例は、次を参照してください[付録 b:。Windows Vista で使用するため、ベンダー提供の INF ファイルの例](bluetooth-faq--appendix-b.md)します。
* パートナー センターを使用して、INF ファイルを Windows Update を通じて使用できるようにするには

インボックス Bth.inf ファイルへの無線を追加することはありません。

## <a name="should-third-party-inf-files-use-the-microsoft-defined-class-guid"></a>サード パーティ製の INF ファイルは、マイクロソフトによって定義されたクラス GUID を使用する必要があります。

Ihv は、インボックス Bluetooth INF ファイル (Bth.inf) を参照する INF ファイルのみの Bluetooth デバイスに Microsoft によって定義されたクラスのグローバル一意識別子 (GUID) ({e0cbf06c cd8b 4647 bb8a 263b43f0f974}) を使用してください。 これは、デバイスが、ネイティブ Windows 共同インストーラー、サービス、および通知エリア アイコンを使用していることを意味します。 Bluetooth スタックを実装する Ihv は、ベンダー固有クラス GUID を作成し、WLK テスト ツールを使用して、スタックが未分類の Windows 認定プログラムに準拠していることを確認する必要があります。

## <a name="why-the-control-panel-bluetooth-application-is-missing"></a>コントロール パネルの Bluetooth アプリケーションが存在しない理由

コントロール パネルの Bluetooth アプリケーションは、デバイスとプリンターに組み込まれています。 したがって、Bluetooth 無線の設定を調整して、Bluetooth のデバイスを管理する、新しい Bluetooth の追加デバイスのみ実行できますからデバイスとプリンター内。

## <a name="why-the-bluetooth-icon-might-not-appear-in-the-taskbar"></a>Bluetooth のアイコンがタスク バーに表示されない原因

Bluetooth のアイコンがタスク バーに表示されない場合、次の理由の 1 つ以上が考えられます。

* Bluetooth 無線がになっています。
* Bluetooth 無線がエミュレーション モードです。
* **Bluetooth 設定**ダイアログ ボックスで、 **Bluetooth アイコン、通知領域に表示する** チェック ボックスが選択されていません。

## <a name="windows-support-for-bluetooth-radio-firmware-updates"></a>Windows は、Bluetooth 無線ファームウェアの更新プログラムをサポートします。

現時点では、Windows に含まれている Bluetooth スタックはファームウェアの更新プログラムを直接サポートされません。 ただし、Bluetooth 無線が USB ポート経由で接続して、Windows は、USB デバイス ファームウェアの更新 (DFU) 仕様に準拠しているファームウェアの更新プログラムをサポートしています。 Ihv は、ファームウェアの更新と再起動、ラジオ、DFU インターフェイスを介して、Bluetooth 無線通信を行うユーザー モード ユーティリティを作成できます。

## <a name="windows-support-for-vendor-specific-pass-through-commands"></a>パススルー コマンドのベンダー固有の Windows のサポート

Windows には、ベンダー固有のパススルー コマンドのサポートが含まれています。 これらのカーネル モード インターフェイスは、WDK に記載されています。

## <a name="windows-support-for-vendor-supplied-profiles"></a>Windows は、ベンダーから提供されたプロファイルをサポートします。

Windows では、ベンダーから提供された Bluetooth のプロファイルをサポートします。 INF ファイル (Bth.inf) でのボックスには、Bluetooth SIG によって標準化されたそれらのプロファイル用の Guid が含まれます。

ユーザーのコンピューターに Bluetooth デバイスとペアにデバイスのプロファイルが Bth.inf に記載されているプロファイルと比較されます。 デバイスのプロファイルには、それらのプロファイルのいずれかと一致しません、ユーザーは適切なベンダのソフトウェアを提供することを確認するダイアログ ボックスを表示します。

ベンダー固有のプロファイルをベンダーは、独自の GUID を使用し、ベンダー固有の INF ファイルで参照する必要があります。 この INF ファイルを使用して、インクルードを使用できます、ディレクティブ、適切な Bth.inf セクションとディレクティブを参照する必要があります。 ベンダー固有の INF ファイルの例は、次を参照してください[付録 b:。Windows Vista で使用するため、ベンダー提供の INF ファイルの例](bluetooth-faq--appendix-b.md)します。

## <a name="bluetooth-profiles-and-protocols-that-are-enabled-by-default"></a>Bluetooth のプロファイルと既定で有効になっているプロトコル

Windows に含まれている Bluetooth スタックでは、いくつかの Bluetooth プロファイルのみのインボックス サポートを提供します。 ベンダーは、USB および PCI の場合と同じ他の Bluetooth プロファイルをサポートするために必要なサービスを実装する必要があります。 Windows が既定で有効になっている Bluetooth のプロファイルを使用できます: サポートされているプロファイルと呼ばれる: 物理デバイス オブジェクト (Pdo) を生成します。 これにより、プロファイルを有効にするには、必要なドライバーの既定の読み込みができます。 SupportedServices と UnsupportedServices の値を調べることで、レジストリでサポートされているプロファイルを識別することができます、 **HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\サービス\\Bthport\\パラメーター**キー。

> [!NOTE]
> Bthport キーは、Bluetooth デバイスをインストールした後にのみ、レジストリに追加されます。

次の表は、Windows をサポートする Bth.inf でプロファイルを一覧表示します。

|サービス ID|説明|
|----|----|
|{00001101-0000-1000-8000-00805f9b34fb}|SPP|
|{00001103-0000-1000-8000-00805f9b34fb}|DUN
|{00001124-0000-1000-8000-00805f9b34fb}|HID|
|{00001126-0000-1000-8000-00805f9b34fb}|HCRP|

### <a name="windows-bluetooth-profiles"></a>Windows Bluetooth のプロファイル

Bluetooth 対応デバイスまたは Windows 10 を実行している PC を使用するアクセサリの場合、デバイスはサポートされている Bluetooth プロファイルのいずれかを使用する必要があります。 最新の一覧を参照してください。 [Bluetooth のサポートされているプロファイル](https://support.microsoft.com/help/10568/windows-10-supported-bluetooth-profiles)します。

Ihv が自分のデバイス用の PDO を自動的に生成する Windows をしない場合、サービスの GUID サポートされていないサービスの一覧に追加できます。 例については、Bth.inf を参照してください。

## <a name="how-group-policy-can-block-bluetooth-radio-installation"></a>グループ ポリシーが Bluetooth ラジオのインストールをブロックする方法

グループ ポリシーを使用して、Bluetooth 無線のインストールをブロックする方法の詳細については、"禁止されているデバイスのインストールを禁止する のセクションを参照してください[グループ ポリシーと使用状況を制御するデバイスのインストールをステップ バイ ステップ ガイド](https://go.microsoft.com/fwlink/p/?linkid=324335).

Bluetooth 無線の次の互換性のある Id を使用します。

USB\\クラス\_(USB ベースの無線) の E0 MS\_BTHX\_BTHMINI (USB 以外の無線) の

> [!NOTE]
> Bluetooth ドライバーのサポートは、既にインストールされている場合この削除されません。 また、このポリシーは、プレインストールのイメージに適用する必要があります。

## <a name="how-to-change-the-device-id-profile-record-published-by-windows"></a>Windows によって発行されたデバイス ID のプロファイル レコードを変更する方法

デバイス ID のプロファイルでは、リモート デバイスに id 情報を提供するために使用できる SDP レコードを定義します。 以前と現在の Windows バージョンでは、ペアになっているデバイスで公開されているデバイス ID のレコードを使用するがで、汎用の Bluetooth サービスのデバイスに固有のハードウェア Id を提供します。

Windows では、リモートの Bluetooth デバイスに Windows デバイスを識別するためにローカルのデバイス ID レコードも公開します。 既定値は、Oem が特定の Windows デバイスを区別しやすくして調整できます。 これらの値が、HKLM 下で、次の表のように定義されている\\システム\\CCS\\サービス\\BTHPORT\\パラメーター レジストリ キー。

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
