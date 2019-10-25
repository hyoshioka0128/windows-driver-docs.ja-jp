---
title: Device Guard Readiness Tool を使用して HVCI ドライバーの互換性を評価する
description: デバイスガード準備ツールを使用して、ドライバーコードの HVCI ドライバーの互換性を評価するには、次の手順に従います。
ms.assetid: ''
ms.date: 02/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: f63b97117a4df00fa2af082e400d9ba23cfc4850
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825174"
---
# <a name="use-the-device-guard-readiness-tool-to-evaluate-hvci-driver-compatibility"></a>Device Guard Readiness Tool を使用して HVCI ドライバーの互換性を評価する

## <a name="overview"></a>概要

Device Guard 準備ツールは、さまざまなセキュリティ強化機能をサポートする PC を作成するためのいくつかの要件を確認するように設計されています。 このセクションでは、このツールを使用して、ドライバーがハイパーバイザーで保護されたコード整合性 (HVCI) 環境で実行できるかどうかを評価する方法について説明します。 

HVCI ドライバー Device Guard の互換性をテストするための OS とハードウェアの要件:

1. Windows: windows Pro、Windows 10 Enterprise、Windows Server、Windows 10 IoT Enterprise (S モードではサポートされていません) など、すべてのバージョンの Windows で使用できます。

2. ハードウェア: SLAT を使用した仮想化拡張機能をサポートする最近のハードウェア。

セキュアブートなどの追加の要件を評価する準備ツールを使用するには、準備ツールのダウンロードに含まれている readme.txt ファイルを参照してください。

関連するデバイスの基本テストの詳細については、「[デバイスの DevFund テスト](https://docs.microsoft.com/windows-hardware/test/hlk/testref/device-devfund-tests)」を参照してください。

## <a name="implement-device-guard-compatible-code"></a>Device Guard と互換性のあるコードを実装する

Device Guard と互換性のあるコードを実装するには、ドライバーコードが次のことを実行していることを確認してください。

- 既定で NX に設定する
- メモリ割り当てに NX Api/フラグを使用します (NonPagedPoolNx)
- 書き込み可能および実行可能ファイルの両方のセクションを使用しない
- 実行可能なシステムメモリを直接変更しません。
- カーネルで動的コードを使用しない
- 実行可能ファイルとしてデータファイルを読み込みません
- セクションのアラインメントは、0x1000 (PAGE\_SIZE) の倍数です。 例: DRIVER\_ALIGNMENT = 0x1000

システムで使用するために予約されていない次の DDIs の一覧は、影響を受ける可能性があります。

|                                                                                                      |
|------------------------------------------------------------------------------------------------------|
| DDI 名                                                                                             |
| [**ExAllocatePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepool)                                                          |
| [**ExAllocatePoolWithQuota**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithquota)                                        |
| [**ExAllocatePoolWithQuotaTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithquotatag)                                  |
| [**Exallocatepoolwithtag に**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)                                            |
| [**ExAllocatePoolWithTagPriority**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtagpriority)                            |
| [**ExInitializeNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializenpagedlookasidelist)                        |
| [**Exststokasiアス Stex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializelookasidelistex)                                |
| [**MmAllocateContiguousMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousmemory)                                  |
| [**MmAllocateContiguousMemorySpecifyCache**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousmemoryspecifycache)          |
| [**MmAllocateContiguousMemorySpecifyCacheNode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousmemoryspecifycachenode)  |
| [**MmAllocateContiguousNodeMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousnodememory)                          |
| [**MmCopyMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmcopymemory)                                                              |
| [**MmMapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmapiospace)                                                              |
| [**MmMapLockedPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpages)                                                      |
| [**MmMapLockedPagesSpecifyCache**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpagesspecifycache)                              |
| [**MmProtectMdlSystemAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprotectmdlsystemaddress)                                    |
| [**ZwAllocateVirtualMemory**](https://msdn.microsoft.com/library/windows/hardware/ff566416)                                        |
| [**Zw/** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatesection)                                                        |
| [**ZwMapViewOfSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwmapviewofsection)                                                  |
| [**Ntています**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatesection)                                                        |
| [**NtMapViewOfSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwmapviewofsection)                                                  |
| [**ClfsCreateMarshallingArea**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfscreatemarshallingarea)                                    |
| NDIS                                                                                                 |
| [**NdisAllocateMemoryWithTagPriority**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatememorywithtagpriority)                  |
| 記憶域                                                                                              |
| [**StorPortGetDataInBufferSystemAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportgetdatainbuffersystemaddress)             |
| [**StorPortGetSystemAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportgetsystemaddress)                                     |
| [**ChangerClassAllocatePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mcd/nf-mcd-changerclassallocatepool)                                     |
| [ディスプレイ]                                                                                              |
| [*DxgkCbMapMemory*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_map_memory)                                                         |
| [**VideoPortAllocatePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportallocatepool)                                           |
| オーディオミニポート                                                                                       |
| [**IMiniportDMus:: NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iminiportdmus-newstream)                                        |
| [**IMiniportMidi:: NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportmidi-newstream)                                        |
| [**IMiniportWaveCyclic:: NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavecyclic-newstream)                            |
| [**IPortWavePci::NewMasterDmaChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepci-newmasterdmachannel)                      |
| [**IMiniportWavePci:: NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-newstream)                                  |
| オーディオポートクラス                                                                                     |
| [**PcNewDmaChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewdmachannel)                                                         |
| [**PcNewResourceList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewresourcelist)                                                     |
| [**PcNewResourceSublist**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewresourcesublist)                                               |
| IFS                                                                                                  |
| [**FltAllocatePoolAlignedWithTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatepoolalignedwithtag)                              |
| [**FltAllocateContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatecontext)                                                    |
| WDF                                                                                                  |
| [**Wdfstasiアス Stcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdflookasidelistcreate)                                             |
| [**WdfMemoryCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycreate)                                                           |
| [**WdfDeviceAllocAndQueryProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceallocandqueryproperty)                             |
| [**WdfDeviceAllocAndQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceallocandquerypropertyex)                         |
| [**WdfFdoInitAllocAndQueryProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitallocandqueryproperty)                           |
| [**WdfFdoInitAllocAndQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitallocandquerypropertyex)                       |
| [**WdfIoTargetAllocAndQueryTargetProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetallocandquerytargetproperty)             |
| [**WdfRegistryQueryMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistryquerymemory)                                             |


## <a name="using-the-dgr-tool"></a>DGR ツールの使用

Device Guard 準備ツールを使用するには、次の手順を実行します。

-   **テスト PC を準備する**

    *コードの整合性の仮想化ベースの保護を有効にする*-システム情報アプリ (msinfo32) を実行します。 "Device Guard Virtualization based security" という項目を探します。 "Running" と表示されます。

    または、PowerShell で情報を表示するために使用できる管理ツールを使用してチェックするための WMI インターフェイスも用意されています。

    ```console
    Get-CimInstance –ClassName Win32_DeviceGuard –Namespace root\Microsoft\Windows\DeviceGuard
    ```

    表示される出力を中断する方法の詳細については、「[コードの整合性の仮想化ベースの保護を有効に](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-exploit-guard/enable-virtualization-based-protection-of-code-integrity)する」を参照してください。

    *Device guard を無効*にする-準備ツールの実行中は、デバイスの保護機能によってドライバーの読み込みが妨げられる可能性があるため、テスト対象の PC で device guard を無効にする必要があることに注意してください。

    *記録テスト署名を有効*にする-署名されていない開発ドライバーをインストールできるようにするには、BCDEdit を使用してテスト署名を有効にすることをお勧めします。

    ```console
    bcdedit /set TESTSIGNING ON 
    ```

-   **テストドライバーのインストール**

    ターゲットテスト PC に必要なテストドライバーをインストールします。

    **重要** 開発ドライバーをテストし、コードの問題を解決したら、最終的な実稼働ドライバーを再テストします。 また、HLK を使用してドライバーをテストします。 詳細については、「[ハイパーバイザーコード整合性準備テスト](https://docs.microsoft.com/windows-hardware/test/hlk/testref/b972fc52-2468-4462-9799-6a1898808c86)」を参照してください。



-   **Device Guard 準備ツールをインストールする**

    **警告**  
    Device Guard 準備ツールがレジストリ値を変更し、セキュアブートなどの機能に影響を与える可能性があるため、データやアプリケーションが含まれていないテスト PC を使用します。 テストを実行した後、Windows を再インストールして、必要なセキュリティ構成を再確立することができます。

    1. こちらからツールをダウンロードしてください。 [Device guard と Credential guard ハードウェア準備ツール](https://www.microsoft.com/download/details.aspx?id=53337)。

    2. ターゲットのテストコンピューターでツールを解凍します。

-   **署名されていないスクリプトを実行できるように PowerShell を構成します。**

    準備ツールは PowerShell スクリプトです。 準備ツールのスクリプトを使用するには、管理者の PowerShell スクリプトを開きます。

    実行ポリシーがまだ実行中のスクリプトを許可するように設定されていない場合は、次のように手動で設定する必要があります。

    ```powershell
    Set-ExecutionPolicy Unrestricted
    ```

-   **準備ツールを実行して HVCI を有効にする**

    1. Powershell で、準備ツールを解凍したディレクトリに移動します。

    2. 準備ツールを実行して HVCI を有効にします。

    ```powershell
    DG_Readiness_Tool.ps1 -Enable HVCI
    ```

    3. 指示に従って、PC を再起動します。

-   **スクリプトを実行して HVCI 機能を評価する**

    1. 準備ツールを実行して、HVCI をサポートするドライバーの機能を評価します。

    ```powershell
    DG_Readiness_Tool.ps1 -Capable HVCI
    ```

-   **出力を評価する**

    画面への出力は色分けされています。

    |                   |                                                                                                   |
    |-------------------|---------------------------------------------------------------------------------------------------|
    | 赤-エラー      | DG/CG の有効化と使用を禁止する要素が見つからないか、構成されていません。                |
    | 黄-警告 | このデバイスは、DG/CG の有効化と使用に使用できますが、追加のセキュリティ上の利点はありません。 |
    | 緑-メッセージ  | このデバイスは、DG/CG 要件に完全に準拠しています。                                           |

    既定では、画面への出力に加えて、詳細な出力を含むログファイルは C:\\DGLogs にあります。

    Device Guard 準備ツールの出力には、5つの手順 (またはセクション) があります。 手順 1. には、ドライバーの互換性情報が含まれています。

    ```text
     ====================== Step 1 Driver Compat ====================== 
    ```

    緑色で表示されるドライバーは、HVCI の互換性の問題を特定していません。 特定のドライバーの評価に関心がある場合、ドライバー名が緑色で表示され、アクティブで読み込まれている場合は、HVCI 互換性テストに合格しています。

    次に示す "互換性のない HVCI カーネルドライバーモジュール" セクションを、ログの末尾に向かって見つけます。

    ```text
    InCompatible HVCI Kernel Driver Modules found

    Module: TestDriver1.sys
        Reason: section alignment failures:             9
    Module: TestDriver2.sys
        Reason: execute pool type count:                3
    ```

    上に示したサンプルでは、2つのドライバーが互換性なしとして識別されます。 TestDriver1 にメモリセクションアラインメントエラーがあり、TestDriver2 には実行可能メモリ領域を使用するように構成されたプールがあります。

    デバイスドライバーの非互換性の7種類の統計情報は、! verifier デバッガー拡張機能を使用して使用することもできます。 ! Verifier 拡張機能の詳細については、「 [ **! verifier**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-verifier)」を参照してください。

    ```text
            Execute Pool Type Count:                3
            Execute Page Protection Count:          0
            Execute Page Mapping Count:             0
            Execute-Write Section Count:            0
            Section Alignment Failures:             0
            Unsupported Relocs Count:               0
            IAT in Executable Section Count:        0
    ```



次の表を使用して、出力を解釈し、さまざまな種類の HVCI 非互換性を修正するために必要なドライバーコードの変更を決定します。



<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>

<tr class="odd">
<td align="left"><strong>警告</strong></td>
<td align="left"><strong>償還</strong></td>
</tr>

<tr class="even">
<td align="left"><p>プールの種類の実行</p></td>
<td align="left"><p>呼び出し元は、実行可能なプールの種類を指定しました。 実行可能メモリを要求するメモリ割り当て関数の呼び出し。</p>
<p>すべてのプールの種類に実行可能でない NX フラグが含まれていることを確認してください。</p>
</td>
</tr>

<tr class="odd">
<td align="left"><p>ページ保護の実行</p></td>
<td align="left"><p>呼び出し元は、実行可能ページの保護を指定しました。</p>
<p>"No execute" ページ保護マスクを指定します。</p>
</td>
</tr>

<tr class="even">
<td align="left"><p>ページマッピングの実行</p></td>
<td align="left"><p>呼び出し元は、実行可能なメモリ記述子リスト (MDL) マッピングを指定しました。</p>
<p> 使用するマスクに MdlMappingNoExecute が含まれていることを確認します。 詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer" data-raw-source="[MmGetSystemAddressForMdlSafe](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)">MmGetSystemAddressForMdlSafe</a> 」を参照してください。</p>
</td>
</tr>

<tr class="odd">
<td align="left"><p>実行/書き込みセクション</p></td>
<td align="left"><p>イメージには、実行可能ファイルと書き込み可能セクションが含まれています。</p>
</td>
</tr>

<tr class="even">
<td align="left"><p>セクションのアラインメントエラー</p>
</td>
<td align="left"><p>このイメージには、ページがアラインされていないセクションが含まれています。</p>
<p>セクションのアラインメントは、0x1000 (PAGE_SIZE) の倍数である必要があります。 例: DRIVER_ALIGNMENT = 0x1000</p></td>
</tr>


<tr class="even">
<td align="left"><p>実行可能なセクションの IAT</p></td>
<td align="left"><p>インポートアドレステーブル (IAT) は、メモリの実行可能なセクションである必要はありません。</p>
<p>この問題は、IAT がメモリの読み取りおよび実行 (RX) のみのセクションにある場合に発生します。 これは、参照されている DLL の正しいアドレスを設定するために、OS が IAT に書き込むことができないことを意味します。 </p>
<p> この問題を発生させる方法の1つとして、コードリンクで<a href="https://docs.microsoft.com/cpp/build/reference/merge-combine-sections" data-raw-source="[/MERGE (Combine Sections)](https://docs.microsoft.com/cpp/build/reference/merge-combine-sections)">/merge (セクションの結合)</a>オプションを使用する方法があります。 たとえば、.rdata (読み取り専用で初期化されたデータ) をテキストデータ (実行可能コード) にマージすると、IAT がメモリの実行可能なセクションに存在する可能性があります。  </p>
</td>
</tr>

</tbody>
</table>


---------

サポートされていない Relocs 含ん

<p>Windows 10 バージョン1507では、アドレス空間レイアウトのランダム化 (ASLR) が使用され1607ているため、アドレスの配置とメモリの再配置で問題が発生する可能性があります。  オペレーティングシステムは、リンカーによって既定のベースアドレスが ASLR に割り当てられた実際の場所に設定されている場所からアドレスを再配置する必要があります。 この再配置では、ページの境界をまたがることはできません。  たとえば、ページのオフセット0x3FFC で始まる64ビットアドレス値を考えてみます。 このアドレス値は、オフセット0x0003 の次のページに重なっています。 この種類の重複する relocs 含んは、Windows 10 バージョン1703より前ではサポートされていません。</p>

<p>このような状況は、グローバル構造体型の変数初期化子が、及ぶ再配置を避けるために変数を移動できないようにレイアウトされた別のグローバルへのポインターが不整合になっている場合に発生する可能性があります。 リンカーは変数を移動しようとしますが、それができない場合もあります (たとえば、大規模なミスアライメントの構造体や、ミスアライメントされた構造体の大きな配列など)。 必要に応じて、 <a href="https://docs.microsoft.com/cpp/build/reference/gy-enable-function-level-linking" data-raw-source="[/Gy (COMDAT)](https://docs.microsoft.com/cpp/build/reference/gy-enable-function-level-linking)">/gy (COMDAT)</a>オプションを使用してモジュールを組み立て、リンカーがモジュールコードを可能な限りアラインできるようにする必要があります。</p>



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

アセンブラーコードの使用に関連する他の状況もあります。この問題は、この問題が発生する可能性があります。

---------


## <a name="script-customization"></a>スクリプトのカスタマイズ

次に示すのは、Regkeys とその値の一覧です。この一覧には、スクリプトをデバイスガードと Credential Guard に対してカスタマイズし、UEFI ロックを使用しないようにしてください。

UEFI ロックを使用せずに HVCI と CG を有効にするには:

```reg
REG ADD "HKLM\SYSTEM\CurrentControlSet\Control\DeviceGuard" /v "EnableVirtualizationBasedSecurity" /t REG_DWORD /d 1 /f' 
REG ADD "HKLM\SYSTEM\CurrentControlSet\Control\DeviceGuard" /v "RequirePlatformSecurityFeatures" /t REG_DWORD /d 1 /f' 
```

## <a name="driver-verifier-code-integrity"></a>ドライバーの検証ツールのコードの整合性

Driver Verifier コード整合性オプションフラグ (0x02000000) を使用して、この機能に準拠しているかどうかを検証する追加のチェックを有効にします。 これをコマンドラインから有効にするには、次のコマンドを使用します。

```console
verifier.exe /flags 0x02000000 /driver <driver.sys>
```
検証ツールを使用する場合にこのオプションを選択するには、[*カスタム設定の作成*] (コード開発者向け) を選択し、[*次へ*] を選択して、[_コードの整合性チェック_] を選択します。

Verifier コマンドライン/query オプションを使用して、現在のドライバーの検証ツールの情報を表示できます。

```console
verifier /query 
```







