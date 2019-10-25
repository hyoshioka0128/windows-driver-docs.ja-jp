---
title: Bluetooth ホストラジオのサポート
ms.assetid: 7AA53797-F8DC-4FA6-9A19-E20289AF50CA
description: Windows での Bluetooth ホストのラジオサポートに関する質問と回答の一覧を示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f5240c496d110a3027d041cbc8782b574c8296c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832167"
---
# <a name="bluetooth-host-radio-support"></a>Bluetooth ホストの無線のサポート

このトピックでは、Bluetooth ラジオのサポートに関してよく寄せられる質問への回答を示します。

## <a name="bluetooth-host-controllers-supported-in-windows"></a>Windows でサポートされている Bluetooth ホストコントローラー

Windows では、Bluetooth ラジオを外部ドングルとしてパッケージ化するか、コンピューター内に埋め込むことができますが、コンピューターの USB ポートのいずれかに接続する必要があります。 Windows 7 および Windows Vista に含まれている Bluetooth スタックは、PCI、I2C、シリアル、セキュアデジタル i/o (SDIO)、コンパクト、または PC カードインターフェイスを介した Bluetooth ラジオ接続をサポートしていません。 Windows 8 と Windows 8.1 では、代替トランスポートを介して接続された無線をサードパーティ製のバスドライバーを使用して追加できます。 詳細については、「 [Bluetooth デバイスリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_bltooth/)」の拡張可能な転送に関するセクションを参照してください。

## <a name="forcing-the-bluetooth-stack-to-load-if-windows-cannot-match-the-device-id-windows-vista"></a>Windows がデバイス ID と一致しない場合に、Bluetooth スタックを強制的に読み込む (Windows Vista)

新しい Bluetooth ラジオが、Windows に含まれている Bluetooth INF (Bth .inf) のどのデバイス Id とも一致しない可能性があります。 これにより、Windows がデバイスの Bluetooth スタックを読み込めなくなります。 Ihv は、次のいずれかの方法で、そのラジオがネイティブの Bluetooth スタックで動作することを確認する必要があります。

* Bth .inf を参照するラジオ用の INF を作成します。 Bluetooth ラジオ用ベンダー固有の INF ファイルの例については、「[付録 B: Windows Vista で使用するベンダー提供の Inf ファイルの例](bluetooth-faq--appendix-b.md)」を参照してください。
* 拡張互換 ID OS 記述子をデバイスファームウェアに格納します。この記述子は、互換性のある適切な ID と互換 ID を指定します。 拡張互換 ID OS 記述子の詳細については、「 [MICROSOFT OS 記述子](https://go.microsoft.com/fwlink/p/?linkid=308932)」を参照してください。
* Bluetooth スタックを強制的に読み込む

次の手順では、デバイスマネージャーを使用して、新しい無線用に Bluetooth スタックを強制的に読み込みます。

1. コントロールパネルデバイスマネージャーアプリケーションを実行し、デバイスの一覧で Bluetooth ラジオを識別します。
2. ドライバーソフトウェアの更新ウィザードを実行するには、Bluetooth ラジオ項目を右クリックし、**ドライバーソフトウェアの更新** を選択します。
3. ウィザードを使用して、Bluetooth スタックを強制的にインストールします。

この手順の詳細については、「[付録 a: Windows Vista の新しいハードウェアにインボックス Bluetooth ドライバーをインストールする方法](bluetooth-faq--appendix-a.md)」を参照してください。

## <a name="ensure-in-box-support-for-bluetooth-radios"></a>Bluetooth ラジオのインボックスサポートを確認する

Ihv は、次の手順を実行して、Bluetooth ラジオが Windows で box のサポートを受けられるようにする必要があります。

* ラジオが拡張された compat ID OS 機能記述子をサポートしていることを確認します。 詳細については、「 [MICROSOFT OS 記述子](https://docs.microsoft.com/windows-hardware/drivers/usbcon/microsoft-os-1-0-descriptors-specification)」を参照してください。
* Bluetooth ラジオハードウェアおよび関連する INF ファイルの Windows 認定プログラムの承認を取得します。 Bluetooth ラジオ用ベンダー固有の INF ファイルの例については、「[付録 B: Windows Vista で使用するベンダー提供の Inf ファイルの例](bluetooth-faq--appendix-b.md)」を参照してください。
* パートナーセンターを使用して、で INF ファイルを使用できるように Windows Update

ラジオをインボックスの Bth .inf ファイルに追加することはできなくなりました。

## <a name="should-third-party-inf-files-use-the-microsoft-defined-class-guid"></a>サードパーティ製の INF ファイルで Microsoft 定義のクラス GUID を使用する必要がある

Ihv は、Bluetooth デバイスに対して、Microsoft 定義のグローバル一意識別子 (GUID) ({e0cbf06c cd8b 4647 bb8a 263b43f0f974}) を使用する必要があります。このような INF ファイルに含まれるのは、インボックス Bluetooth INF ファイル (Bth .inf) を参照するファイルのみです。 これは、デバイスがネイティブの Windows co インストーラー、サービス、通知領域アイコンを使用することを意味します。 独自の Bluetooth スタックを実装する Ihv は、ベンダー固有のクラス GUID を作成し、WLK テストツールを使用して、そのスタックが未分類の Windows 認定プログラムに準拠していることを確認する必要があります。

## <a name="why-the-control-panel-bluetooth-application-is-missing"></a>コントロールパネルの Bluetooth アプリケーションが見つからない理由

コントロールパネルの Bluetooth アプリケーションは、デバイスとプリンターに組み込まれました。 したがって、Bluetooth ラジオの設定の調整、Bluetooth デバイスの管理、新しい Bluetooth デバイスの追加は、デバイスとプリンター内からのみ実行できます。

## <a name="why-the-bluetooth-icon-might-not-appear-in-the-taskbar"></a>Bluetooth アイコンがタスクバーに表示されない理由

Bluetooth アイコンがタスクバーに表示されない場合は、次の1つまたは複数の理由が考えられます。

* Bluetooth ラジオがオフになっています。
* Bluetooth ラジオはエミュレーションモードです。
* **[Bluetooth 設定]** ダイアログボックスの **[通知領域に Bluetooth アイコンを表示]** する チェックボックスはオフになっています。

## <a name="windows-support-for-bluetooth-radio-firmware-updates"></a>Bluetooth ラジオファームウェア更新プログラムの Windows サポート

現時点では、Windows に含まれている Bluetooth スタックは、ファームウェアの更新プログラムを直接サポートしていません。 ただし、USB ポートを介して接続されている Bluetooth ラジオの場合、Windows は USB デバイスファームウェア更新 (DFU) 仕様に準拠したファームウェア更新プログラムをサポートします。 Ihv は、DFU インターフェイス経由で Bluetooth ラジオと通信するユーザーモードユーティリティを作成して、ファームウェアの更新を実行し、ラジオを再起動することができます。

## <a name="windows-support-for-vendor-specific-pass-through-commands"></a>ベンダー固有のパススルーコマンドに対する Windows のサポート

Windows には、ベンダー固有のパススルーコマンドのサポートが含まれています。 これらのカーネルモードインターフェイスは、「WDK」に記載されています。

## <a name="windows-support-for-vendor-supplied-profiles"></a>ベンダーが提供するプロファイルの Windows サポート

Windows では、ベンダーが提供する Bluetooth プロファイルがサポートされています。 Bluetooth SIG によって標準化されたこれらのプロファイルの Guid は、box INF ファイル (Bth .inf) に含まれています。

ユーザーが Bluetooth デバイスをコンピューターとペアリングすると、デバイスのプロファイルは、Bth .inf に記載されているプロファイルと比較されます。 デバイスプロファイルがこれらのプロファイルのいずれとも一致しない場合、ユーザーには、適切なベンダーソフトウェアを提供するかどうかを確認するダイアログボックスが表示されます。

ベンダー固有のプロファイルを必要とするベンダーは、独自の GUID を使用して、ベンダー固有の INF ファイルでそれを参照する必要があります。 この INF ファイルでは、インクルードおよび要求ディレクティブを使用して、適切な Bth のセクションとディレクティブを参照できます。 ベンダー固有の INF ファイルの例については、「[付録 B: Windows Vista で使用するベンダー提供の Inf ファイルの例](bluetooth-faq--appendix-b.md)」を参照してください。

## <a name="bluetooth-profiles-and-protocols-that-are-enabled-by-default"></a>既定で有効になっている Bluetooth プロファイルとプロトコル

Windows に組み込まれている Bluetooth スタックは、一部の Bluetooth プロファイルに対してのみ、インボックスサポートを提供します。 ベンダーは、USB および PCI の場合と同様に、他の Bluetooth プロファイルをサポートするために必要なサービスを実装する必要があります。 Windows では、物理デバイスオブジェクト (PDOs) を生成するために、既定で有効になっている Bluetooth プロファイル (サポートされているプロファイルと呼ばれます) を使用できます。 これにより、プロファイルを有効にするために必要なドライバーの既定の読み込みが有効になります。 レジストリでサポートされているプロファイルを特定するには、[ **HKEY\_LOCAL\_MACHINE\\System\\CurrentControlSet\\Services] の下にある [supportedservices] と [UnsupportedServices] の値を参照してください\\Bthport \\Parameters**キー。

> [!NOTE]
> Bthport キーは、Bluetooth デバイスをインストールした後にのみレジストリに追加されます。

次の表に、Windows でサポートされているプロファイルの一覧を示します。

|サービス ID|説明|
|----|----|
|{00001101-0000-10008-8000-00805f9b34fb}|SPP|
|{00001103-0000-10008-8000-00805f9b34fb}|アップ
|{000011240000-10008-8000-00805f9b34fb}|HID|
|{00001126-0000-10008-8000-00805f9b34fb}|HCRP|

### <a name="windows-bluetooth-profiles"></a>Windows Bluetooth プロファイル

Bluetooth 対応のデバイスまたはアクセサリが、Windows 10 を実行している PC で動作するようにするには、デバイスはサポートされているいずれかの Bluetooth プロファイルを使用する必要があります。 [サポートされている Bluetooth プロファイル](https://support.microsoft.com/help/10568/windows-10-supported-bluetooth-profiles)の最新の一覧を参照してください。

Ihv がデバイスの PDO を自動的に生成しないようにする場合、サポートされていないサービスの一覧にサービス GUID を追加できます。 例については、「Bth .inf」を参照してください。

## <a name="how-group-policy-can-block-bluetooth-radio-installation"></a>Bluetooth ラジオのインストールをブロックグループポリシー方法

グループポリシーを使用して Bluetooth ラジオのインストールをブロックする方法の詳細については、「ステップバイステップガイド」の「禁止されたデバイスのインストールを禁止する」セクションを参照して、[グループポリシーを使用したデバイスのインストールと使用の制御に](https://go.microsoft.com/fwlink/p/?linkid=324335)関するセクションを参照してください。

Bluetooth ラジオには、次の互換性のある Id を使用します。

Usb\\クラス\_E0 (USB ベース無線の場合) MS\_BTHX\_BTHX (非 USB ラジオの場合)

> [!NOTE]
> これにより、Bluetooth ドライバーのサポートが既にインストールされている場合は削除されません。 また、このポリシーをプレインストールイメージに適用する必要があります。

## <a name="how-to-change-the-device-id-profile-record-published-by-windows"></a>Windows によって発行されたデバイス ID プロファイルレコードを変更する方法

デバイス ID プロファイルは、リモートデバイスに id 情報を提供するために使用できる SDP レコードを定義します。 以前のバージョンと現在のバージョンの Windows では、ペアリングされたデバイスで発行されたデバイス ID レコードを使用して、一般的な Bluetooth サービスにデバイス固有のハードウェア Id を提供しています。

また、windows は、ローカルデバイス ID レコードを発行して、Windows デバイスをリモート Bluetooth デバイスと識別します。 Oem は、特定の Windows デバイスをより明確に識別できるように、既定値を調整できます。 これらの値は、HKLM\\システム\\CCS\\services\\BTHPORT\\Parameters レジストリキーの下にある次の表のように定義されています。

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
<th align="left"><p>タスクバーの検索ボックスに</p></th>
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
<td align="left"><p>OEM 指定の VendorID</p></td>
<td align="left"><p>0x06 – Microsoft ベンダー ID</p></td>
</tr>
<tr class="even">
<td align="left"><p>DIDProductID</p></td>
<td align="left"><p>DWORD</p></td>
<td align="left"><p>OEM 指定の ProductID</p></td>
<td align="left"><p>0x01 – Microsoft Windows</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DIDVersion</p></td>
<td align="left"><p>DWORD</p></td>
<td align="left"><p>OEM 指定の製品バージョン</p></td>
<td align="left"><p>0x0800 – Windows 8</p></td>
</tr>
</tbody>
</table>
