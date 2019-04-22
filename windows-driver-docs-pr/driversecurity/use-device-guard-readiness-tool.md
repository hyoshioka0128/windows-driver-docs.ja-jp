---
title: Device Guard Readiness Tool を使用して HVCI ドライバーの互換性を評価する
description: デバイス ガード準備ツールを使用して、ドライバー コードの HVCI ドライバーの互換性を評価するこれらの手順に従います。
ms.assetid: ''
ms.date: 02/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d4a31a354f05f96623fc1bfc30e32e9f9c4f203
ms.sourcegitcommit: fb8b1d2e18dd727e8a479b04c9e6051e7e9fa484
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/18/2019
ms.locfileid: "58845549"
---
# <a name="use-the-device-guard-readiness-tool-to-evaluate-hvci-driver-compatibility"></a>Device Guard Readiness Tool を使用して HVCI ドライバーの互換性を評価する

## <a name="overview"></a>概要

デバイス ガードの準備ツールの機能を多くのさまざまなセキュリティ拡張機能をサポートする PC を作成するための要件を確認してください。 このセクションでは、ハイパーバイザーで保護されたコードの整合性 (HVCI) 環境で実行するドライバーの能力を評価するツールを使用する方法について説明します。 

HVCI ドライバー Device Guard の互換性をテストするための OS とハードウェアの要件:

1. Windows:すべてのバージョンの Windows Pro、Windows 10 Enterprise、Windows Server、Windows 10 IoT Enterprise が (S モードではサポートされていません) などの Windows で使用できます。

2. ハードウェア :SLAT と仮想化拡張機能をサポートする最新のハードウェア。

準備ツールを使用してセキュリティで保護のブートなど、追加の要件を評価するには、準備ツールのダウンロードに含まれる readme.txt ファイルを参照してください。

関連するデバイスの基本テストに関する詳細については、次を参照してください。 [Device.DevFund テスト](https://docs.microsoft.com/windows-hardware/test/hlk/testref/device-devfund-tests)します。

## <a name="implement-device-guard-compatible-code"></a>Device Guard の互換性のあるコードを実装します。

Device Guard の互換性のあるコードを実装するには、次のドライバー コードになっていることを確認します。

- 既定では、NX にオプトインします。
- NX Api/フラグを使用して、メモリの割り当て (NonPagedPoolNx)
- 書き込み可能な実行可能ファイルのセクションでは使用しません
- 実行可能なシステム メモリを直接変更しようとはしません
- カーネルの動的なコードを使用しません
- 実行可能ファイルとしてデータ ファイルを読み込みません
- セクションの配置は 0x1000 の倍数 (ページ\_サイズ)。 例: ドライバー\_配置 0x1000 を =

次のシステム用に予約されていない Ddi の一覧を受ける可能性があります。

|                                                                                                      |
|------------------------------------------------------------------------------------------------------|
| DDI 名                                                                                             |
| [**ExAllocatePool**](https://msdn.microsoft.com/library/windows/hardware/ff544501)                                                          |
| [**ExAllocatePoolWithQuota**](https://msdn.microsoft.com/library/windows/hardware/ff544506)                                        |
| [**ExAllocatePoolWithQuotaTag**](https://msdn.microsoft.com/library/windows/hardware/ff544513)                                  |
| [**Exallocatepoolwithtag に**](https://msdn.microsoft.com/library/windows/hardware/ff544520)                                            |
| [**ExAllocatePoolWithTagPriority**](https://msdn.microsoft.com/library/windows/hardware/ff544523)                            |
| [**ExInitializeNPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff545301)                        |
| [**ExInitializeLookasideListEx**](https://msdn.microsoft.com/library/windows/hardware/ff545298)                                |
| [**MmAllocateContiguousMemory**](https://msdn.microsoft.com/library/windows/hardware/ff554460)                                  |
| [**MmAllocateContiguousMemorySpecifyCache**](https://msdn.microsoft.com/library/windows/hardware/ff554464)          |
| [**MmAllocateContiguousMemorySpecifyCacheNode**](https://msdn.microsoft.com/library/windows/hardware/ff554469)  |
| [**MmAllocateContiguousNodeMemory**](https://msdn.microsoft.com/library/windows/hardware/jj602795)                          |
| [**MmCopyMemory**](https://msdn.microsoft.com/library/windows/hardware/dn342884)                                                              |
| [**MmMapIoSpace**](https://msdn.microsoft.com/library/windows/hardware/ff554618)                                                              |
| [**MmMapLockedPages**](https://msdn.microsoft.com/library/windows/hardware/ff554622)                                                      |
| [**MmMapLockedPagesSpecifyCache**](https://msdn.microsoft.com/library/windows/hardware/ff554629)                              |
| [**MmProtectMdlSystemAddress**](https://msdn.microsoft.com/library/windows/hardware/ff554670)                                    |
| [**ZwAllocateVirtualMemory**](https://msdn.microsoft.com/library/windows/hardware/ff566416)                                        |
| [**ZwCreateSection**](https://msdn.microsoft.com/library/windows/hardware/ff566428)                                                        |
| [**ZwMapViewOfSection**](https://msdn.microsoft.com/library/windows/hardware/ff566481)                                                  |
| [**NtCreateSection**](https://msdn.microsoft.com/library/windows/hardware/ff556473)                                                        |
| [**NtMapViewOfSection**](https://msdn.microsoft.com/library/windows/hardware/ff556551)                                                  |
| [**ClfsCreateMarshallingArea**](https://msdn.microsoft.com/library/windows/hardware/ff541520)                                    |
| NDIS                                                                                                 |
| [**NdisAllocateMemoryWithTagPriority**](https://msdn.microsoft.com/library/windows/hardware/ff561606)                  |
| ストレージ                                                                                              |
| [**StorPortGetDataInBufferSystemAddress**](https://msdn.microsoft.com/library/windows/hardware/jj553720)             |
| [**StorPortGetSystemAddress**](https://msdn.microsoft.com/library/windows/hardware/ff567100)                                     |
| [**ChangerClassAllocatePool**](https://msdn.microsoft.com/library/windows/hardware/ff551402)                                     |
| ディスプレイ                                                                                              |
| [*DxgkCbMapMemory*](https://msdn.microsoft.com/library/windows/hardware/ff559533)                                                         |
| [**VideoPortAllocatePool**](https://msdn.microsoft.com/library/windows/hardware/ff570180)                                           |
| オーディオ ミニポート                                                                                       |
| [**IMiniportDMus::NewStream**](https://msdn.microsoft.com/library/windows/hardware/ff536701)                                        |
| [**IMiniportMidi::NewStream**](https://msdn.microsoft.com/library/windows/hardware/ff536710)                                        |
| [**IMiniportWaveCyclic::NewStream**](https://msdn.microsoft.com/library/windows/hardware/ff536723)                            |
| [**IPortWavePci::NewMasterDmaChannel**](https://msdn.microsoft.com/library/windows/hardware/ff536916)                      |
| [**IMiniportWavePci::NewStream**](https://msdn.microsoft.com/library/windows/hardware/ff536735)                                  |
| オーディオ ポート クラス                                                                                     |
| [**PcNewDmaChannel**](https://msdn.microsoft.com/library/windows/hardware/ff537712)                                                         |
| [**PcNewResourceList**](https://msdn.microsoft.com/library/windows/hardware/ff537717)                                                     |
| [**PcNewResourceSublist**](https://msdn.microsoft.com/library/windows/hardware/ff537718)                                               |
| IFS                                                                                                  |
| [**FltAllocatePoolAlignedWithTag**](https://msdn.microsoft.com/library/windows/hardware/ff541762)                              |
| [**FltAllocateContext**](https://msdn.microsoft.com/library/windows/hardware/ff541710)                                                    |
| WDF                                                                                                  |
| [**WdfLookasideListCreate**](https://msdn.microsoft.com/library/windows/hardware/ff548694)                                             |
| [**WdfMemoryCreate**](https://msdn.microsoft.com/library/windows/hardware/ff548706)                                                           |
| [**WdfDeviceAllocAndQueryProperty**](https://msdn.microsoft.com/library/windows/hardware/ff545882)                             |
| [**WdfDeviceAllocAndQueryPropertyEx**](https://msdn.microsoft.com/library/windows/hardware/dn265599)                         |
| [**WdfFdoInitAllocAndQueryProperty**](https://msdn.microsoft.com/library/windows/hardware/ff547239)                           |
| [**WdfFdoInitAllocAndQueryPropertyEx**](https://msdn.microsoft.com/library/windows/hardware/dn265612)                       |
| [**WdfIoTargetAllocAndQueryTargetProperty**](https://msdn.microsoft.com/library/windows/hardware/ff548585)             |
| [**WdfRegistryQueryMemory**](https://msdn.microsoft.com/library/windows/hardware/ff549920)                                             |


## <a name="using-the-dgr-tool"></a>DGR ツールを使用します。

デバイス ガード準備ツールを使用するには、次の手順を完了します。

-   **テスト PC を準備します。**

    *有効にする仮想化ベースのコードの整合性の保護*-システムの実行情報アプリ (msinfo32)。 次の項目を探します。「Device Guard 仮想化ベースのセキュリティです。」 これが表示されます。"Running"。

    または、PowerShell での情報を表示するために使用できる管理ツールを使用して確認するための WMI インターフェイスもできます。

    ```console
    Get-CimInstance –ClassName Win32_DeviceGuard –Namespace root\Microsoft\Windows\DeviceGuard
    ```

    表示される出力を中断する方法については、次を参照してください。[コードの整合性の仮想化ベースの保護を有効にする](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-exploit-guard/enable-virtualization-based-protection-of-code-integrity)します。

    *Device Guard を無効にする*-準備ツールを実行中に Device Guard する必要がありますを無効にする、テスト対象の PC で Device Guard は、読み込みからドライバーを妨げる可能性し、ドライバーはテスト用に準備ツールを使用できませんに注意してください。

    *任意の署名を有効にするテスト*- BCDEdit を使用してテストの署名を有効にすることも、符号なしの開発のドライバーのインストールを許可します。

    ```console
    bcdedit /set TESTSIGNING ON 
    ```

-   **テスト ドライバーをインストールします。**

    ターゲット テスト PC には、目的のテスト ドライバーをインストールします。

    **重要な**開発ドライバーをテストして、コードの問題に対処したら、最終的な運用環境のドライバーを再テストします。 さらに、ドライバーをテスト、HLK を使用します。 詳細については、次を参照してください。[ハイパーバイザー コードの整合性の準備のテスト](https://msdn.microsoft.com/library/windows/hardware/dn955152)します。



-   **デバイス ガード準備ツールをインストールします。**

    **警告**  
    デバイス ガードの準備ツールは、レジストリ値を変更し、セキュリティで保護された boot などの機能に影響を与える可能性があります、テスト、データやアプリケーションが含まれていない PC を使用します。 テストの実行後、必要なセキュリティ構成を再確立するために Windows を再インストールしたい場合があります。

    1. ここからツールをダウンロードします。[Device Guard と Credential Guard のハードウェアの適合性ツール](https://www.microsoft.com/download/details.aspx?id=53337)します。

    2. ターゲット コンピューターのテスト ツールを解凍します。

-   **未署名のスクリプトの実行を許可するように PowerShell を構成します。**

    準備ツールは、PowerShell スクリプトです。 準備ツールのスクリプトを使用するには、管理者の PowerShell スクリプトを開きます。

    スクリプトの実行を許可する実行ポリシーが設定されていない場合する必要があります手動で設定する、次に示すよう。

    ```powershell
    Set-ExecutionPolicy Unrestricted
    ```

-   **HVCI を有効にする準備ツールを実行します。**

    1. Powershell では、準備ツールの解凍先ディレクトリに移動します。

    2. HVCI を有効にする準備ツールを実行します。

    ```powershell
    DG_Readiness_Tool.ps1 -Enable HVCI
    ```

    3. PC を再起動します。

-   **HVCI 機能を評価するスクリプトを実行します。**

    1. HVCI をサポートするために、ドライバーの能力を評価する準備ツールを実行します。

    ```powershell
    DG_Readiness_Tool.ps1 -Capable HVCI
    ```

-   **出力を評価します。**

    画面への出力は色分け表示されています。

    |                   |                                                                                                   |
    |-------------------|---------------------------------------------------------------------------------------------------|
    | 赤 - エラー      | 要素が不足しているか、未構成を妨げる有効化と配布グループ/重心を使用します。                |
    | 黄 - 警告 | 有効にし、配布グループ/重心を使用して、このデバイスを使用できますが、追加のセキュリティ上の利点が削除されます。 |
    | 緑 - メッセージ  | このデバイスは完全に準拠した DG/CG 要件です。                                           |

    既定では、画面に出力だけでなく詳細な出力とログ ファイルが c: で配置されている\\DGLogs

    デバイス ガードの準備ツールの出力には、5 つの手順 (またはセクション) があります。 手順 1 が含まれています、ドライバーの互換性情報です。

    ```text
     ====================== Step 1 Driver Compat ====================== 
    ```

    緑色で表示ドライバーは、識別された HVCI 互換性の問題がない必要があります。 ドライバー名が緑色で表示されますがアクティブで、読み込まれた場合は、特定のドライバーを評価する場合は、HVCI 互換性テストに成功します。

    ログの最後に、次に示す「互換性のない HVCI カーネル ドライバーのモジュール」セクションを見つけます。

    ```text
    InCompatible HVCI Kernel Driver Modules found

    Module: TestDriver1.sys
        Reason: section alignment failures:             9
    Module: TestDriver2.sys
        Reason: execute pool type count:                3
    ```

    上記のサンプルでは、2 つのドライバーが互換性なしと識別されます。 TestDriver1.sys はメモリのセクションのアラインメント エラーを備え、TestDriver2.sys 実行可能なメモリ領域を使用するように構成されたプールがあります。

    7 種類のデバイス ドライバーの非互換性の統計情報が使用しても、! verifier デバッガー拡張機能。 詳細については、! verifier 拡張機能を参照してください[ **! verifier**](https://msdn.microsoft.com/library/windows/hardware/ff565591)します。

    ```text
            Execute Pool Type Count:                3
            Execute Page Protection Count:          0
            Execute Page Mapping Count:             0
            Execute-Write Section Count:            0
            Section Alignment Failures:             0
            Unsupported Relocs Count:               0
            IAT in Executable Section Count:        0
    ```



次の表を使用して、出力を解釈を HVCI 非互換性のさまざまな種類の修正に必要なドライバー コードの変更内容を確認します。



<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>

<tr class="odd">
<td align="left"><strong>警告</strong></td>
<td align="left"><strong>引き換え</strong></td>
</tr>

<tr class="even">
<td align="left"><p>プールの種類を実行します。</p></td>
<td align="left"><p>呼び出し元は、プールの実行可能ファイルの種類を指定します。 メモリの割り当てを実行可能なメモリを要求する関数を呼び出しています。</p>
<p>すべてプールの種類が非実行可能ファイルの NX フラグが含まれていることを確認します。</p>
</td>
</tr>

<tr class="odd">
<td align="left"><p>ページ保護を実行します。</p></td>
<td align="left"><p>呼び出し元は、実行可能ファイルのページ保護を指定します。</p>
<p>「実行なし」ページの保護のマスクを指定します。</p>
</td>
</tr>

<tr class="even">
<td align="left"><p>ページ マッピングを実行します。</p></td>
<td align="left"><p>呼び出し元は、実行可能なメモリ記述子のリスト (MDL) マッピングを指定します。</p>
<p> MdlMappingNoExecute が使用されるマスクに含まれていることを確認します。 詳細については、次を参照してください<a href="https://msdn.microsoft.com/library/windows/hardware/ff554559.aspx" data-raw-source="[MmGetSystemAddressForMdlSafe](https://msdn.microsoft.com/library/windows/hardware/ff554559.aspx)">MmGetSystemAddressForMdlSafe。</a></p>
</td>
</tr>

<tr class="odd">
<td align="left"><p>セクションの実行-書き込み</p></td>
<td align="left"><p>イメージには、実行可能ファイル/書き込み可能なセクションが含まれています。</p>
</td>
</tr>

<tr class="even">
<td align="left"><p>セクション配置エラー</p>
</td>
<td align="left"><p>イメージには、ページに合わせるないセクションが含まれています。</p>
<p>セクションの配置は、0x1000 (PAGE_SIZE) の倍数である必要があります。 例: DRIVER_ALIGNMENT 0X1000 を =</p></td>
</tr>


<tr class="even">
<td align="left"><p>実行可能ファイルのセクション内の IAT</p></td>
<td align="left"><p>インポート アドレス テーブル (IAT) は、メモリの実行可能ファイルのセクションをすることはできません。</p>
<p>この問題は、メモリの読み取りと実行 (RX) のみセクションでは、IAT がある場合に発生します。 つまり、OS は場所の正しいアドレスを設定する IAT への書き込みできません参照される DLL です。 </p>
<p> これは、発生する 1 つの方法が使用する場合、 <a href="https://docs.microsoft.com/cpp/build/reference/merge-combine-sections" data-raw-source="[/MERGE (Combine Sections)](https://docs.microsoft.com/cpp/build/reference/merge-combine-sections)">/MERGE (セクションの結合)</a>コード リンク オプション。 たとえば場合 .rdata (読み取り専用に初期化されたデータ) は .text データ (実行可能コード) とマージは、メモリの実行可能ファイルのセクションでは最終的が iat を介したことができます。  </p>
</td>
</tr>

</tbody>
</table>


---------

サポートされていない Relocs

<p>Windows 10 バージョン 1507、Windows 10 をバージョン 1607 を使用されるアドレス空間レイアウト Randomization (ASLR)、問題のためにも発生アドレスの配置とメモリの再配置します。  オペレーティング システムでは、リンカーが ASLR が割り当てられている実際の場所にその既定のベース アドレスをセットから、アドレスを再配置する必要があります。 この再配置は、ページの境界にまたがることはできません。  たとえば、ページ内のオフセット 0x3FFC に開始される 64 ビットのアドレス値を検討してください。 アドレス値は、オフセット 0x0003 で次のページには、経由で重複しています。 重複する relocs のこの型は、Windows 10 バージョン 1703 以前サポートされていません。</p>

<p>構造体のグローバル型変数の初期化子は、リンカーが straddling 再配置を回避するために変数を移動できないような方法でレイアウトという別のグローバルな不整合へのポインターを持つ、このような状況が発生します。 リンカーは、変数に移動しようとしていますが、状況にいない可能性がある (たとえば大規模な不整合構造体または構造体の不整合の大きな配列) そうことがあります。 使用してモジュールをアセンブルする必要があります、適切な場所、 <a href="https://docs.microsoft.com/cpp/build/reference/gy-enable-function-level-linking" data-raw-source="[/Gy (COMDAT)](https://docs.microsoft.com/cpp/build/reference/gy-enable-function-level-linking)">/Gy (COMDAT)</a>可能な限りモジュール コードを配置するリンカーを許可するオプション。</p>



```cpp
#include <pshpack1.h>

typedef struct _BAD_STRUCT {
      USHORT Value;
      CONST CHAR *String;
} BAD_STRUCT, * PBAD_STRUCT;

#include <poppack.h>

#define BAD_INITIALIZER0 { 0, "BAD_STRING" },
#define BAD_INITIALIZER1 \
      BAD_INITIALIZER0      \
      BAD_INITIALIZER0      \
      BAD_INITIALIZER0      \
      BAD_INITIALIZER0      \
      BAD_INITIALIZER0      \
      BAD_INITIALIZER0      \
      BAD_INITIALIZER0      \
      BAD_INITIALIZER0      

#define BAD_INITIALIZER2 \
      BAD_INITIALIZER1      \
      BAD_INITIALIZER1      \
      BAD_INITIALIZER1      \
      BAD_INITIALIZER1      \
      BAD_INITIALIZER1      \
      BAD_INITIALIZER1      \
      BAD_INITIALIZER1      \
      BAD_INITIALIZER1      

#define BAD_INITIALIZER3 \
      BAD_INITIALIZER2      \
      BAD_INITIALIZER2      \
      BAD_INITIALIZER2      \
      BAD_INITIALIZER2      \
      BAD_INITIALIZER2      \
      BAD_INITIALIZER2      \
      BAD_INITIALIZER2      \
      BAD_INITIALIZER2      

#define BAD_INITIALIZER4 \
      BAD_INITIALIZER3      \
      BAD_INITIALIZER3      \
      BAD_INITIALIZER3      \
      BAD_INITIALIZER3      \
      BAD_INITIALIZER3      \
      BAD_INITIALIZER3      \
      BAD_INITIALIZER3      \
      BAD_INITIALIZER3      

BAD_STRUCT MayHaveStraddleRelocations[4096] = { // as a global variable
      BAD_INITIALIZER4
};
```

この問題は発生することも、アセンブラー コードの使用に関連するその他の状況があります。

---------


## <a name="script-customization"></a>スクリプトのカスタマイズ

レジストリと Device Guard と Credential Guard UEFI ロックなしにスクリプトのカスタマイズには、その値の一覧を次に示します。

HVCI と UEFI ロックなしの重心を有効にします。

```reg
REG ADD "HKLM\SYSTEM\CurrentControlSet\Control\DeviceGuard" /v "EnableVirtualizationBasedSecurity" /t REG_DWORD /d 1 /f' 
REG ADD "HKLM\SYSTEM\CurrentControlSet\Control\DeviceGuard" /v "RequirePlatformSecurityFeatures" /t REG_DWORD /d 1 /f' 
```

## <a name="driver-verifier-code-integrity"></a>Driver Verifier のコードの整合性

使用して、ドライバーの検証コードの整合性オプション フラグ (0x02000000) 追加を有効にするのには、この機能への準拠を検証するかを確認します。 これが、コマンドラインから有効にするには、次のコマンドを使用します。

```console
verifier.exe /flags 0x02000000 /driver <driver.sys>
```
Verifier GUI を使用する場合は、このオプションを選択するには、選択*カスタム設定を作成*(開発者)、コードの次のように選択します。*次*、し、_整合性チェックをコード_。

現在のドライバー検証ツールの情報を表示するのに検証ツール コマンド ライン/query オプションを使用することができます。

```console
verifier /query 
```







