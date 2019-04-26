---
title: ELAM ドライバーの要件
description: ドライバーのインストールは、一般的な INF 処理によって、ドライバーの登録、オンラインおよびオフラインのインストールの既存のツールを使用する必要があります。
ms.assetid: B00B4361-B531-4D28-A521-0F8B3B48CEA4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 005cc3daaee4e66308dbbfea2e97782b4f2d7963
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346174"
---
# <a name="elam-driver-requirements"></a>ELAM ドライバーの要件


ドライバーのインストールは、一般的な INF 処理によって、ドライバーの登録、オンラインおよびオフラインのインストールの既存のツールを使用する必要があります。  サンプル ELAM ドライバーのコードについては、次を参照してください。 https://github.com/Microsoft/Windows-driver-samples/tree/master/security/elam 

## <a name="am-driver-installation"></a>ドライバーのインストールには


ドライバーのインストールの互換性を確保、ELAM ドライバーは、自身を他のすべてのブート開始ドライバーのようなブート開始ドライバーとしてアドバタイズします。 INF ドライバーをブート ローダーによって読み込まれ、カーネルの初期化時に初期化することを示します SERVICE_BOOT_START (0) にスタートアップの種類を設定します。 ELAM ドライバーは、「早期起動」としてそのグループをアドバタイズします。 このグループ内のドライバーの事前起動の動作は、次のセクションで説明されていると、Windows で実装されます。

次は、INF ELAM ドライバーのドライバーのインストール セクションの例です。

```cpp
[SampleAV.Service]
DisplayName    = %SampleAVServiceName%
Description    = %SampleAVServiceDescription%
ServiceType    = 1       ; SERVICE_KERNEL_DRIVER
StartType      = 0       ; SERVICE_BOOT_START
ErrorControl   = 3       ; SERVICE_ERROR_CRITICAL
LoadOrderGroup = “Early-Launch”
```

AM、ドライバーが任意のデバイスを所有していないためには、ドライバーがレジストリにサービスとして追加のみように、レガシとして AM ドライバーをインストールする必要があります。 (通常の PNP ドライバーとして午前ドライバーをインストールすると場合、レジストリの列挙型」セクションに追加され、したがってドライバーをアンロードするときに望ましくない動作につながる、PDO の参照があります。)

含める必要があります、 [SignatureAttributes セクション](inf-signatureattributes-section.md)ELAM ドライバーの INF ファイルにします。 

## <a name="backup-driver-installation"></a>バックアップのドライバーのインストール

ELAM ドライバーが誤って破損していることを復旧メカニズムを提供するには、ELAM インストーラーは、ドライバーのコピーをバックアップの場所にもインストールされます。 これにより、クリーンなコピーを取得し、インストールを回復する WinRE が許可されます。

インストーラーからバックアップ ファイルの場所を読み取り、 **BackupPath**にキーが格納されています。

```cpp
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\EarlyLaunch
```

インストーラーは、レジストリ キーで指定されたフォルダーのバックアップ コピーを配置します。

## <a name="am-driver-initialization"></a>ドライバーの初期化中します。


Windows ブート ローダー、Winload、読み込みすべてのブート開始ドライバーとその依存 Dll、Windows カーネルに渡す前にメモリにします。 ブート開始ドライバーは、ディスク スタックが初期化されている前に初期化する必要があるデバイス ドライバーを表します。 他のユーザー ディスク スタックとボリューム マネージャー、およびファイル システム ドライバーやオペレーティング システム用のバス ドライバーの間で、これらのドライバーが含まれます。

## <a name="am-driver-callback-interface"></a>ドライバーのコールバック インターフェイスをいます


ELAM ドライバー、PnP マネージャーのすべてのブート開始ドライバーおよび依存する DLL は、説明を提供するコールバックを使用して、既知の適切なバイナリ、既知の無効なバイナリまたは不明のバイナリとしてすべてのブート イメージを分類できます。

既定のオペレーティング システム ポリシーでは既知の不良のドライバーと Dll の初期化ありません。 ポリシーを構成し、ブート構成証明の一部として Winload で測定されます。

PnP ポリシーとを使用して、分類、AM ドライバーによって提供される各ブート イメージを初期化するかどうかを決定します。

### <a name="registry-callbacks"></a>レジストリのコールバック

早期起動ドライバーでは、監視し、各ブート開始ドライバーの入力として使用される構成データの検証をレジストリまたはブート ドライバーのコールバックを使用できます。 構成データは、Winload によって読み込まれ、使用可能なブート ドライバーの初期化時に、システム レジストリ ハイブに格納されます。 これらのコールバックは、ELAM ドライバーの有効期間を通じて有効な登録解除されます、ドライバーが読み込まれると。 For more info, see:

* [**CmRegisterCallbackEx**](https://msdn.microsoft.com/library/windows/hardware/ff541921)
* [**CmRegisterCallback**](https://msdn.microsoft.com/library/windows/hardware/ff541918)
* [**CmUnRegisterCallback**](https://msdn.microsoft.com/library/windows/hardware/ff541928)

### <a name="boot-driver-callbacks"></a>ブート ドライバーのコールバック

使用[ **IoRegisterBootDriverCallback** ](https://msdn.microsoft.com/library/windows/hardware/hh439379)と[ **IoUnRegisterBootDriverCallback** ](https://msdn.microsoft.com/library/windows/hardware/hh439394)登録、の登録を解除する[ *BOOT_DRIVER_CALLBACK_FUNCTION*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-boot_driver_callback_function)します。

このコールバックは、すべてのブート開始ドライバーが初期化されているし、コールバック機能が動作しなくを含む、ELAM ドライバーを Windows からステータスの更新を提供します。

### <a name="callback-type"></a>コールバックの種類

[ **BDCB_CALLBACK_TYPE 列挙**](https://msdn.microsoft.com/library/windows/hardware/hh406352)コールバックの 2 つの種類について説明します。

-   コールバック状態が更新され、ELAM ドライバー (BdCbStatusUpdate) を提供します。
-   イメージ (BdCbInitializeImage) を初期化する前に、ブート開始ドライバーと依存 Dll を分類する AM ドライバーによって使用されるコールバック

2 つのコールバック型では、コールバックに固有の追加情報を提供する一意のコンテキスト構造があります。

ステータス更新コールバックのコンテキストの構造体には、Windows の吹き出しを記述する 1 つの列挙型が含まれています。

イメージの初期化のコールバックの context 構造は複雑に読み込まれた各イメージのハッシュと証明書の情報を含むです。 さらに、構造体には、AM ドライバーがドライバーの分類の種類を格納する出力パラメーターであるフィールドが含まれています。

ステータスの更新コールバックから返されたエラーは致命的なエラーとして扱われます、システムのバグ チェックにつながります。 これは、ELAM ドライバーに、マルウェア対策ポリシーの外部で、状態に達したときを示す機能を提供します。 たとえば、AM のランタイム ドライバーに読み込まれ初期化されませんが、早期起動ドライバーが失敗を Windows が AM なしの状態に移行することを防ぐために準備のアンロードにコールバック ドライバーが読み込まれます。

イメージは、イメージの初期化のコールバックからエラーが返されるときに、"不明"として扱われます。 不明なドライバーが初期化またはが初期化時にスキップ ベース OS のポリシー。

## <a name="malware-signatures"></a>マルウェアの署名

マルウェアの署名のデータは、AM、ISV によって決まりますが、少なくとも、ハッシュのドライバーの承認済みリストを含める必要があります。 署名のデータは、hklm Winload によって読み込まれる新しい"早期起動 Drivers"hive でレジストリに格納されます。 各 AM ドライバーでは、その署名バイナリ ラージ オブジェクト (BLOB) を格納するための一意キーを持ちます。 キーとレジストリ パスの形式があります。

```cpp
HKLM\ELAM\<VendorName>\
```

キー内で、ベンダーが自由に定義し、値のいずれかを使用します。
、メジャー ブートで計測される 3 つの定義済みのバイナリ blob 値があるし、各仕入先が使用可能性があります。

-   測定
-   ポリシー
-   Config

ELAM hive がアンロード、使用後に起動時マルウェア対策によってパフォーマンスを得るです。 ファイルの場所から hive ファイルをマウントする必要があります署名データを更新する場合、ユーザー モード サービス\\Windows\\System32\\config\\ELAM します。 など、UUID を生成、文字列に変換、および、hive のマウント先に一意のキーとして使用する可能性があります。
これらの Blob のデータの保存と取得の形式は、ISV、一任しますが、午前ドライバーは、データの整合性を検証できるように、署名データを署名する必要があります。

**マルウェアの署名を検証します。**

マルウェアの署名のデータの整合性を検証するためのメソッドは、各 AM ISV までままです。 [CNG 暗号化プリミティブ関数](https://msdn.microsoft.com/library/windows/desktop/aa833130)はデジタル署名と証明書をマルウェアの署名データを確認するために利用できます。

**マルウェアの署名のエラー**

ELAM ドライバーは、署名のデータとそのチェックの整合性が失敗した場合、または、ELAM ドライバーの初期化が成功した署名データがない場合にチェックします。 場合、 ここでは、各ブート ドライバーの ELAM ドライバーは「不明」各初期化のコールバックで返す必要があります。 さらに、ELAM ドライバーは、開始した後、午前のランタイム コンポーネントには、この情報を渡す必要があります。

## <a name="unloading-the-am-driver"></a>AM ドライバーをアンロード


コールバック StatusType BdCbStatusPrepareForUnload が、これは、AM ドライバーをすべてブート ドライバーであることを示す値が初期化され、アンロードすること AM ドライバーを準備する必要があります。 をアンロードする前に、起動時 AM ドライバーはそのコールバックの登録を解除する必要があります。 登録解除のコールバック中に発生することはできません代わりに、ドライバーを DriverEntry 中に指定できる DriverUnload 関数で発生するがあります。

マルウェア保護の継続性を維持し、適切なハンドオフことを確認するには、早期起動 AM driver がアンロードされているよりも前、AM をランタイム エンジンを開始する必要があります。 これは、AM をランタイム エンジンで、起動時 AM ドライバーによって確認されるブート ドライバーがあることを意味します。

## <a name="performance"></a>パフォーマンス


ドライバーでは、次の表で定義されているパフォーマンス要件を満たす必要があります。

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
<td align="left"><p>Start Time</p></td>
<td align="left"><p>終了時刻</p></td>
<td align="left"><p>上限</p></td>
</tr>
<tr class="even">
<td align="left"><p>初期化することを許可する前に読み込まれたブートの不可欠なドライバーを評価します。 これには、状態の更新プログラムのコールバックも含まれています。</p></td>
<td align="left"><p>カーネルに読み込まれたブートの不可欠なドライバーを評価するマルウェア対策ドライバーにコールバックします。</p></td>
<td align="left"><p>マルウェア対策ドライバーでは、評価結果を返します。</p></td>
<td align="left"><p>0.5ms</p></td>
</tr>
<tr class="odd">
<td align="left"><p>すべての読み込まれたブートの不可欠なドライバーを評価します。</p></td>
<td align="left"><p>最初のブートが読み込まれた不可欠なドライバーを評価するマルウェア対策ドライバーにカーネル呼び出し。</p></td>
<td align="left"><p>マルウェア対策ドライバーでは、最後のブートの不可欠なドライバーの評価結果を返します。</p></td>
<td align="left"><p>50 ミリ秒</p></td>
</tr>
<tr class="even">
<td align="left"><p>フット プリント (ドライバーと構成のメモリ内データ)</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>128 kB</p></td>
</tr>
</tbody>
</table>

 

## <a name="initializing-drivers"></a>ドライバーの初期化


ELAM ドライバーがブート ドライバーが評価されると、カーネルは、ドライバーを初期化するのにかどうかを決定するのに ELAM によって返された分類を使用します。 この決定はポリシーによって異なり、ここでレジストリに格納されます。

```cpp
HKLM\System\CurrentControlSet\Control\EarlyLaunch\DriverLoadPolicy
```

これは、ドメインに参加しているクライアントでグループ ポリシーを通じて構成できます。 マルウェア対策ソリューションは、管理対象外のシナリオでエンドユーザーには、この機能を公開する可能性があります。 DriverLoadPolicy は、次の値が定義されています。
```cpp
PNP_INITIALIZE_DRIVERS_DEFAULT 0x0  (initializes known Good drivers only)
PNP_INITIALIZE_UNKNOWN_DRIVERS 0x1  
PNP_INITIALIZE_BAD_CRITICAL_DRIVERS 0x3 (this is the default setting)
PNP_INITIALIZE_BAD_DRIVERS 0x7
```

## <a name="boot-failures"></a>起動エラー


初期化ポリシーにより、ブート ドライバーがスキップされる場合は、一覧で [次へ] のブート ドライバーを初期化しようとする、カーネルが続行されます。 これは、ドライバーはすべて初期化、またはスキップされた boot ドライバーがブートに不可欠なため、起動に失敗するまでは続きます。 ディスク スタックが開始した後に、クラッシュが発生した場合は、クラッシュ ダンプがあり、不足しているドライバーに関する情報が追加、クラッシュ、またはその理由に関する情報が含まれています。 エラーの原因を特定して、修復しようとしています。 WinRE で使用できます。

## <a name="elam-and-measured-boot"></a>ELAM とメジャー ブート


すぐに呼び出す必要がありますが、ELAM ドライバーは、ポリシー違反 (ルートキットの例) が検出される場合[ **Tbsi_Revoke_Attestation** ](https://docs.microsoft.com/windows/desktop/api/tbs/nf-tbs-tbsi_revoke_attestation)でしたが良好な状態で示される PCRs を無効にします。 関数は、measured boot、たとえば、システム上の TPM をなしに問題がある場合、エラーを返します。

**Tbsi_Revoke_Attestation**カーネル モードから呼び出すことができます。 指定されていない値で PCR [12] を拡張し、TPM でイベント カウンターをインクリメントします。 フォワードここから作成されるすべての引用符で囲まれた信頼関係が壊れているために、両方のアクションは必要に応じて、です。 結果として、メジャー ブート ログは、TPM の電源が入っている時間の残りの TPM の現在の状態を反映していないと、リモート システムをシステムのセキュリティ状態のフォームを信頼することにすることはできません。
