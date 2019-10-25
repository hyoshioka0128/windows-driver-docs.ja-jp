---
title: ELAM ドライバーの要件
description: ドライバーのインストールでは、オンラインとオフラインのインストールに既存のツールを使用し、一般的な INF 処理によってドライバーを登録する必要があります。
ms.assetid: B00B4361-B531-4D28-A521-0F8B3B48CEA4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5cfff0b6fa5eb5d67bbc9594ff4ed3b6e1dab465
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828820"
---
# <a name="elam-driver-requirements"></a>ELAM ドライバーの要件


ドライバーのインストールでは、オンラインとオフラインのインストールに既存のツールを使用し、一般的な INF 処理によってドライバーを登録する必要があります。  ELAM ドライバーコードのサンプルについては、次を参照してください: https://github.com/Microsoft/Windows-driver-samples/tree/master/security/elam 

## <a name="am-driver-installation"></a>ドライバーのインストール時


ドライバーのインストールの互換性を確保するために、ELAM ドライバーは、他のすべてのブート開始ドライバーと同様に、ブート開始ドライバーとして自己アドバタイズします。 INF は、開始の種類を SERVICE_BOOT_START (0) に設定します。これは、ドライバーがブートローダーによって読み込まれ、カーネルの初期化中に初期化される必要があることを示します。 ELAM ドライバーは、そのグループを "初期起動" としてアドバタイズします。 次のセクションで説明するように、このグループのドライバーの初期起動動作は Windows で実装されます。

ELAM ドライバー INF の driver install セクションの例を次に示します。

```cpp
[SampleAV.Service]
DisplayName    = %SampleAVServiceName%
Description    = %SampleAVServiceDescription%
ServiceType    = 1       ; SERVICE_KERNEL_DRIVER
StartType      = 0       ; SERVICE_BOOT_START
ErrorControl   = 3       ; SERVICE_ERROR_CRITICAL
LoadOrderGroup = “Early-Launch”
```

AM ドライバーはデバイスを所有していないため、ドライバーをサービスとしてレジストリに追加するだけで済むように、AM ドライバーをレガシとしてインストールする必要があります。 (AM ドライバーが通常の PNP ドライバーとしてインストールされている場合は、レジストリの enum セクションに追加されるため、PDO 参照が使用されます。これにより、ドライバーのアンロード時に望ましくない動作が発生します)。

また、ELAM ドライバーの INF ファイルに[Signatureattributes セクション](inf-signatureattributes-section.md)を含める必要があります。 

## <a name="backup-driver-installation"></a>バックアップドライバーのインストール

Elam ドライバーが誤って破損した場合の復旧メカニズムを提供するために、ELAM インストーラーでは、ドライバーのコピーもバックアップ場所にインストールします。 これにより、WinRE はクリーンコピーを取得して、インストールを回復することができます。

インストーラーは、に格納されている**BackupPath**キーからバックアップファイルの場所を読み取ります。

```cpp
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\EarlyLaunch
```

その後、インストーラーによって、レジストリキーに指定されたフォルダーにバックアップコピーが格納されます。

## <a name="am-driver-initialization"></a>AM ドライバーの初期化


Windows ブートローダー Winload は、Windows カーネルにハンドオフする前に、すべてのブート開始ドライバーとその依存 Dll をメモリに読み込みます。 ブート開始ドライバーは、ディスクスタックが初期化される前に初期化する必要があるデバイスドライバーを表します。 これらのドライバーには、その他のドライバー、ディスクスタックとボリュームマネージャー、およびオペレーティングシステムデバイス用のファイルシステムドライバーとバスドライバーが含まれます。

## <a name="am-driver-callback-interface"></a>AM ドライバーコールバックインターフェイス


ELAM ドライバーは、コールバックを使用して、すべてのブート開始ドライバーと依存 DLL の説明を PnP マネージャーに提供します。また、すべてのブートイメージを既知の正常なバイナリ、既知の無効なバイナリ、または不明なバイナリとして分類することができます。

既定のオペレーティングシステムポリシーは、既知の無効なドライバーおよび Dll を初期化することはありません。 ポリシーは構成でき、ブート構成証明の一部として Winload によって測定されます。

PnP では、ポリシーと、AM ドライバーによって提供される分類を使用して、各ブートイメージを初期化するかどうかを決定します。

### <a name="registry-callbacks"></a>レジストリコールバック

初期起動ドライバーでは、レジストリまたはブートドライバーのコールバックを使用して、各ブート開始ドライバーの入力として使用される構成データを監視および検証できます。 構成データは、Winload によって読み込まれるシステムレジストリハイブに格納され、ブートドライバーの初期化時に使用できます。

> [!NOTE]
> ELAM レジストリハイブに対する変更は、システムが起動する前に破棄されます。
> そのため、ELAM ドライバーは、レジストリに書き込むのではなく、標準 Windows イベントトレーシング (ETW) ログを使用する必要があります。

これらのコールバックは、ELAM ドライバーの有効期間を通じて有効であり、ドライバーがアンロードされるときに登録が解除されます。 For more info, see:

* [**Cmregisterの例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-cmregistercallbackex)
* [**CmRegisterCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-cmregistercallback)
* [**CmUnRegisterCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-cmunregistercallback)

### <a name="boot-driver-callbacks"></a>ブートドライバーのコールバック

[**IoRegisterBootDriverCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioregisterbootdrivercallback)と[**Iounregisterbootdrivercallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iounregisterbootdrivercallback)を使用して、 [*BOOT_DRIVER_CALLBACK_FUNCTION*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-boot_driver_callback_function)の登録と登録解除を行います。

このコールバックは、すべてのブート開始ドライバーが初期化され、コールバック機能が機能しなくなった場合など、Windows から ELAM ドライバーへのステータスの更新を提供します。

### <a name="callback-type"></a>コールバックの種類

[**BDCB_CALLBACK_TYPE 列挙体**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ne-ntddk-_bdcb_callback_type)は、次の2種類のコールバックを記述します。

-   ELAM ドライバー (BdCbStatusUpdate) にステータスの更新を提供するコールバック
-   イメージを初期化する前に起動時ドライバーと依存 Dll を分類するために、AM ドライバーによって使用されるコールバック (BdCbInitializeImage)

2つのコールバック型には、コールバックに固有の追加情報を提供する一意のコンテキスト構造があります。

ステータス更新コールバックのコンテキスト構造には、Windows コールアウトを記述する列挙型が1つ含まれています。

イメージの初期化コールバックのコンテキスト構造はより複雑で、読み込まれたイメージごとにハッシュと証明書の情報が含まれています。 また、この構造体には、AM ドライバーがドライバーの分類の種類を格納する出力パラメーターであるフィールドも含まれます。

ステータス更新コールバックから返されたエラーは致命的なエラーとして扱われ、システムのバグチェックにつながります。 これにより、ELAM ドライバーは、状態が AM ポリシーの外部に到達したことを示すことができます。 たとえば、AM ランタイムドライバーが読み込まれて初期化されていない場合、初期起動ドライバーは、プレアンロードコールバックを失敗させて、Windows が AM ドライバーが読み込まれていない状態にならないようにすることができます。

イメージは、イメージの初期化コールバックからエラーが返されたときに、不明として扱われます。 不明なドライバーが初期化されているか、OS ポリシーに基づいて初期化がスキップされています。

## <a name="malware-signatures"></a>マルウェアの署名

マルウェアの署名データは、AM ISV によって決定されますが、少なくとも、承認済みのドライバーハッシュの一覧が含まれている必要があります。 署名データは、Winload によって読み込まれる HKLM の新しい "初期起動ドライバー" ハイブにレジストリに格納されます。 各 AM ドライバーには、バイナリラージオブジェクト (BLOB) を格納するための一意のキーがあります。 レジストリパスとキーの形式は次のとおりです。

```cpp
HKLM\ELAM\<VendorName>\
```

キー内では、ベンダーは任意の値を自由に定義して使用することができます。
メジャーブートによって測定される3つの定義済みバイナリ blob 値があり、ベンダーはそれぞれを使用することができます。

-   数え
-   ポリシー
-   Config

ELAM ハイブは、起動時マルウェア対策によってパフォーマンスが使用された後にアンロードされます。 ユーザーモードサービスが署名データを更新する場合は、ファイルの場所 \\Windows\\System32\\config\\ELAM から hive ファイルをマウントする必要があります。 たとえば、UUID を生成して文字列に変換し、hive をマウントする一意のキーとして使用することができます。
これらのデータ Blob のストレージと取得形式は ISV に残されていますが、AM ドライバーがデータの整合性を検証できるように、署名データに署名する必要があります。

**マルウェアの署名の検証**

マルウェアの署名データの整合性を確認する方法は、各 AM ISV に残されています。 [CNG 暗号プリミティブ関数](https://docs.microsoft.com/windows/desktop/SecCNG/cng-cryptographic-primitive-functions)は、マルウェアの署名データのデジタル署名と証明書の検証を支援するために使用できます。

**マルウェアの署名エラー**

ELAM ドライバーが署名データの整合性をチェックし、そのチェックが失敗した場合、または署名データがない場合でも、ELAM ドライバーの初期化は成功します。 この場合、各ブートドライバーでは、各初期化コールバックについて、ELAM ドライバーが "unknown" を返す必要があります。 さらに、ELAM ドライバーは、開始後にこの情報をランタイムの AM コンポーネントに渡す必要があります。

## <a name="unloading-the-am-driver"></a>AM ドライバーのアンロード


コールバック StatusType が BdCbStatusPrepareForUnload である場合、これは、すべてのブートドライバが初期化されていること、および AM ドライバがアンロードされる準備が整っていることを、AM ドライバに示します。 アンロードする前に、初期起動時のドライバーがコールバックを登録解除する必要があります。 コールバック中に登録解除を行うことはできません。ドライバーが Driverunload 中に指定できる DriverUnload 関数で実行する必要があります。

マルウェア対策の継続性を維持し、適切なハンドオフを保証するには、初期起動 AM ドライバーがアンロードされる前に、ランタイム AM エンジンを起動する必要があります。 これは、ランタイムの AM エンジンは、起動時のドライバーによって検証されるブートドライバーである必要があることを意味します。

## <a name="performance"></a>パフォーマンス


ドライバーは、次の表に定義されているパフォーマンス要件を満たしている必要があります。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>シナリオ</p></td>
<td align="left"><p>開始時刻</p></td>
<td align="left"><p>終了時刻</p></td>
<td align="left"><p>上限</p></td>
</tr>
<tr class="even">
<td align="left"><p>読み込まれた起動に不可欠なドライバーを評価してから初期化できるようにします。 これには、ステータス更新コールバックも含まれます。</p></td>
<td align="left"><p>カーネルは、マルウェア対策ドライバーにコールバックして、読み込まれた起動に不可欠なドライバーを評価します。</p></td>
<td align="left"><p>マルウェア対策ドライバーは評価結果を返します。</p></td>
<td align="left"><p>0.5 ミリ秒</p></td>
</tr>
<tr class="odd">
<td align="left"><p>読み込まれたすべてのブートクリティカルドライバーを評価する</p></td>
<td align="left"><p>カーネルは、マルウェア対策ドライバーにコールバックして、最初に読み込まれたブートの重要なドライバーを評価します。</p></td>
<td align="left"><p>マルウェア対策ドライバーは、最後の起動に不可欠なドライバーの評価結果を返します。</p></td>
<td align="left"><p>50ミリ秒</p></td>
</tr>
<tr class="even">
<td align="left"><p>フットプリント (ドライバー + メモリ内の構成データ)</p></td>
<td align="left"><p>該当なし</p></td>
<td align="left"><p>該当なし</p></td>
<td align="left"><p>128 Kb</p></td>
</tr>
</tbody>
</table>

 

## <a name="initializing-drivers"></a>ドライバーの初期化


ブートドライバーが ELAM ドライバーによって評価されると、カーネルは ELAM から返された分類を使用して、ドライバーを初期化するかどうかを判断します。 この決定はポリシーによって規定され、次のレジストリに格納されます。

```cpp
HKLM\System\CurrentControlSet\Control\EarlyLaunch\DriverLoadPolicy
```

これは、ドメインに参加しているクライアントでグループポリシーを使用して構成できます。 マルウェア対策ソリューションでは、管理対象外シナリオでこの機能をエンドユーザーに公開することが必要になる場合があります。 DriverLoadPolicy には次の値が定義されています。
```cpp
PNP_INITIALIZE_DRIVERS_DEFAULT 0x0  (initializes known Good drivers only)
PNP_INITIALIZE_UNKNOWN_DRIVERS 0x1  
PNP_INITIALIZE_BAD_CRITICAL_DRIVERS 0x3 (this is the default setting)
PNP_INITIALIZE_BAD_DRIVERS 0x7
```

## <a name="boot-failures"></a>起動エラー


初期化ポリシーが原因でブートドライバーがスキップされた場合、カーネルはリスト内の次のブートドライバーの初期化を試行し続けます。 これは、ドライバーがすべて初期化されるか、またはスキップされたブートドライバーがブートにとって重要であるために、起動に失敗するまで続行されます。 ディスクスタックが開始された後にクラッシュが発生した場合は、クラッシュダンプが発生します。また、不足しているドライバーに関する情報が含まれています。 これを WinRE で使用して、エラーの原因を特定し、修復を試みることができます。

## <a name="elam-and-measured-boot"></a>ELAM とメジャーブート


ELAM ドライバーがポリシー違反 (たとえば、ルートキット) を検出した場合、すぐに[**Tbsi_Revoke_Attestation**](https://docs.microsoft.com/windows/desktop/api/tbs/nf-tbs-tbsi_revoke_attestation)を呼び出して、システムが良好な状態であることを示す pcr を無効にする必要があります。 システム上の TPM がないなど、測定されたブートで問題が発生した場合、関数はエラーを返します。

**Tbsi_Revoke_Attestation**はカーネルモードから呼び出すことができます。 指定されていない値で PCR [12] を拡張し、TPM のイベントカウンターをインクリメントします。 両方のアクションが必要であるため、ここから作成されたすべての引用符で信頼が解除されます。 その結果、測定されたブートログには、tpm の残りの時間に対する TPM の現在の状態は反映されません。また、リモートシステムは、システムのセキュリティの状態にある信頼を形成できません。
