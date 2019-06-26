---
title: パーティション レイアウト
description: パーティション レイアウト
ms.assetid: 59ac7ec7-1b96-4fe1-a221-d8422e60072d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58197b0a15049649ef2e9d48bc93c1e2df3a8667
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364538"
---
# <a name="windows-10-mobile-partition-layout"></a>Windows 10 Mobile のパーティション レイアウト


Windows 10 Mobile、Microsoft およびシリコン ベンダー (SV) で記憶域のパーティションとパーティションのサイズを構成します。 十分な大きさの現在のすべてのコンポーネントと、電話の有効期間の更新を許可するように、パーティションを設計する必要があります。 スマート フォンでは、パーティションのサイズが設定され後、サイズを変更するだけの方法は、フラッシュ クリーンな完全な更新プログラム、電話のすべてのデータをワイプでデバイスを更新し直すことです。

指定された要件を満たしている必要があります、スマート フォンの記憶域サブシステム[2.2 のセクションします。Windows 10 Mobile の最小ハードウェア要件のメモリ、](https://docs.microsoft.com/windows-hardware/design/minimum/minimum-hardware-requirements-overview#section_2.0_-_minimum_hardware_requirements_for_windows_10_mobile)します。

<div class="alert">
<strong>注: </strong> Oem は追加しないと、削除、または、Microsoft と SV が設計されたレイアウトでのパーティションを変更します。 これにより、電話の更新プログラムによって、電話のすべてのソフトウェアと構成データを処理できることを確認します。 OEM コンポーネント通常に組み込まれている (プリロード済みのアプリケーションとネイティブ サービス) のメインの OS パーティション (データの事前に読み込まれたマップなど)、データのパーティションまたはデバイス (デバイスに固有の読み取り専用の構成データ) のパーティションをプロビジョニングします。
</div>
 

## <a name="span-idpartitionlistspanspan-idpartitionlistspanspan-idpartitionlistspanpartition-list"></a><span id="Partition_list"></span><span id="partition_list"></span><span id="PARTITION_LIST"></span>パーティションの一覧


次の図は、必要なストレージ パーティションを示します。

![パーティション レイアウト](images/oem-bringup-partitionlayout.png)

## <a name="span-idpartitionrequirementsspanspan-idpartitionrequirementsspanspan-idpartitionrequirementsspanpartition-requirements"></a><span id="Partition_requirements"></span><span id="partition_requirements"></span><span id="PARTITION_REQUIREMENTS"></span>パーティションの要件


次の表では、各パーティションの要件をまとめたものです。 すべてのサイズは論理的です。記憶域メディア上で使用される実際の領域が異なる場合があります。 (これは、ユーザー データのパーティションと SD カードを除くすべてのパーティションから成る) システム パーティションのサイズを定義するときに、シリコン ベンダーは、個別のパーティションの空き領域の要件に従う必要があります。 これによりが含まれているが、その他の言語などのソフトウェア資産に制限されていません。 この要件は、必須で、有効期間を通じて、スマート フォンを更新できることを保証するために必要です。

<table>
<colgroup>
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パーティション</th>
<th align="left">目次</th>
<th align="left">ファイル システム</th>
<th align="left">マウント ポイント</th>
<th align="left">暗号化</th>
<th align="left">サイズ</th>
<th align="left">空き領域が今後の更新プログラム用に予約されています</th>
<th align="left">所有者</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DPP</p></td>
<td align="left"><p>デバイス データのプロビジョニング</p></td>
<td align="left"><p>FAT</p></td>
<td align="left"><p>C:\DPP</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>8 MB</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>マイクロソフト</p></td>
</tr>
<tr class="even">
<td align="left"><p>SV パーティション</p></td>
<td align="left"><p>UEFI ファームウェアとその他の SV 固有のパーティション</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>マウント ポイントがありません。</p></td>
<td align="left"><p>状況によって異なる</p></td>
<td align="left"><p>変数</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>SV/OEM</p></td>
</tr>
<tr class="odd">
<td align="left"><p>EFI システム パーティション</p></td>
<td align="left"><p>ブート マネージャー、ブート構成データベース、UEFI アプリケーション</p></td>
<td align="left"><p>FAT</p></td>
<td align="left"><p>C:\ESP</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>32 MB (最小)</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>マイクロソフト</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラッシュ ダンプのパーティション (製品版でないイメージのみに存在する場合)</p></td>
<td align="left"><p>クラッシュ ダンプからのデータ</p></td>
<td align="left"><p>NTFS</p></td>
<td align="left"><p>C:\CrashDump</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>変数のこのパーティションのサイズの値によって異なります、 <strong>SOC</strong>イメージの構築に使用された OEMInput ファイル内の要素。</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>マイクロソフト</p></td>
</tr>
<tr class="odd">
<td align="left"><p>メインの OS (ブート パーティション)</p></td>
<td align="left"><p>OS では、OS、システム レジストリ ハイブ、OEM の事前に読み込まれたアプリケーションを更新します。</p></td>
<td align="left"><p>NTFS</p></td>
<td align="left"><p>C:&lt;/p&gt;</td>
<td align="left"><p>〇</p></td>
<td align="left"><p>約 1.5 GB</p>
</td>
<td align="left"><p>250 MB</p>
</td>
<td align="left"><p>マイクロソフト</p></td>
</tr>
<tr class="even">
<td align="left"><p>データのパーティション</p></td>
<td align="left"><p>ユーザー データ、ユーザーのレジストリ ハイブ、アプリケーション、アプリケーション データ、ページのファイル。</p></td>
<td align="left"><p>NTFS</p></td>
<td align="left"><p>C:\Data</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>他のパーティションでは使用されません eMMC ストレージの残りの部分。 約 256 MB は、ページファイルに使用されます。</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>マイクロソフト</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SD カード</p></td>
<td align="left"><p>ユーザー データ (音楽、画像など)</p></td>
<td align="left"><p>FAT/exFAT</p></td>
<td align="left"><p>変数</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>変数</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>マイクロソフト</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddeviceprovisioningpartitionspanspan-iddeviceprovisioningpartitionspanspan-iddeviceprovisioningpartitionspandevice-provisioning-partition"></a><span id="Device_provisioning_partition"></span><span id="device_provisioning_partition"></span><span id="DEVICE_PROVISIONING_PARTITION"></span>デバイス プロビジョニングのパーティション

パーティション (DPP) をプロビジョニングするデバイスには、特定のデバイスのプロビジョニングのデータが含まれています。 製品の検証が含まれていて、工場で調整するには通常、無線や GPS などのコンポーネントの構成情報とキー。 デバイスに固有であるために、任意のイメージの更新または FFU から除外されます。

このパーティションは、サイズ 8 MB にあるものとします。

<div class="alert">
<strong>重要:</strong> DPP パーティション レイアウトの最初のパーティションとして保護手段をプロビジョニング情報の上書きする必要があります、その他のパーティションのサイズ、その後、変更があります。
</div>

### <a name="span-idsiliconvendorpartitionsspanspan-idsiliconvendorpartitionsspanspan-idsiliconvendorpartitionsspansilicon-vendor-partitions"></a><span id="Silicon_vendor_partitions"></span><span id="silicon_vendor_partitions"></span><span id="SILICON_VENDOR_PARTITIONS"></span>シリコン ベンダー パーティション

SV には、独自のコンポーネント用のパーティションを定義できます。 これらのパーティションの 1 つは、UEFI (Unified Extensible Firmware Interface) のパーティションの UEFI アプリケーションを使用できるシステム操作のプリミティブのセットに標準的なインターフェイスが含まれています。 モデムのデータには、SV パーティションも必要です。


### <a name="span-idefisystempartitionspanspan-idefisystempartitionspanspan-idefisystempartitionspanefi-system-partition"></a><span id="EFI_system_partition"></span><span id="efi_system_partition"></span><span id="EFI_SYSTEM_PARTITION"></span>EFI システム パーティション

EFI システム パーティションには、Windows ブート マネージャー (BootMgr) とブート構成データベース (BCD) が含まれています。 BootMgr は、メインの OS や OS の更新などの上位レベルのオペレーティング システムの読み込みを担当します。 さらに、EFI システム パーティションには、さまざまな FFU アプリケーションなどの UEFI アプリケーション、およびバッテリの充電中のアプリケーションが含まれています。

このパーティションは、32 MB のサイズの最小値になります。

### <a name="span-idcrashdumppartitionspanspan-idcrashdumppartitionspanspan-idcrashdumppartitionspancrash-dump-partition"></a><span id="Crash_dump_partition"></span><span id="crash_dump_partition"></span><span id="CRASH_DUMP_PARTITION"></span>クラッシュ ダンプのパーティション

非小売イメージには、携帯電話が予期せず再起動したときに発生するクラッシュ ダンプからデータを格納するクラッシュ ダンプのパーティションが含まれます。

このパーティションのサイズの値によって異なります、 **SOC**イメージの構築に使用された OEMInput ファイル内の要素。

### <a name="span-idmainospartitionspanspan-idmainospartitionspanspan-idmainospartitionspanmain-os-partition"></a><span id="Main_OS_partition"></span><span id="main_os_partition"></span><span id="MAIN_OS_PARTITION"></span>メインの OS パーティション

メインの OS パーティション、ブート パーティションとも呼ばれますには、すべてのオペレーティング システム イメージを構成するコンポーネントが含まれています。 これには、OEM のカスタマイズとプリロード済みのアプリケーションが含まれます。

このパーティションのサイズは、OEM のカスタマイズと事前に読み込まれたアプリケーションで使用される領域の量によって異なります。 

* **OS ベースライン**: ~ 870 MB、実際には、OS のサイズは、変数の数によって異なりますなどの言語の数に含まれるイメージ。 4 GB のメインの OS のパーティションを圧縮された電話、OS は約 20 ~ 25%、圧縮されていない OS よりも小さいです。
* **OS 更新**: ~ 50 MB
* **OEM は、アプリケーションをプリロード**: 最大 100 MB、最初の起動時の発生後にインストールするアプリケーションの残りのユーザーのストレージの 5% を最初にブート操作中にインストールするアプリケーション
* **今後の更新プログラム用に予約**:電話での記憶域の量によって、変数です。 詳細については、次の列を参照してください。

一般に、このパーティションの書き込み可能なファイルの数は、更新プログラムのための十分な領域を確保する最小の可能な限りに制限される必要があります。 このパーティションには、更新プログラムのための成長のために予約された領域が含まれています。

-   4 GB のストレージだけで電話では、このパーティションは、メインの OS パーティションの圧縮後に約 250 MB の予約済み領域を持っています。

-   4 gb 以上のストレージと圧縮されていないメイン OS パーティションの電話では、このパーティションは、約 250 MB の予約済み領域を持っています。

<div class="alert">
<strong>注:</strong>  Oem を使用して今後の更新プログラムの追加の空き領域を追加することができます、 <strong>AdditionalMainOSFreeSectorsRequest</strong>デバイス プラットフォームの XML ファイル内の要素。
</div>


### <a name="span-iddatapartitionspanspan-iddatapartitionspanspan-iddatapartitionspandata-partition"></a><span id="Data_partition"></span><span id="data_partition"></span><span id="DATA_PARTITION"></span>データのパーティション

このパーティションの内部記憶域では、ユーザー データ、アプリケーション、およびアプリケーションの状態を格納します。 EMMC 上の領域の残りの部分を使用するパーティションのサイズを自動的に調整します。

<div class="alert">
<strong>重要:</strong> データのパーティション レイアウトの最後のパーティションがあります。
</div>

### <a name="span-idsdcardspanspan-idsdcardspanspan-idsdcardspansd-card"></a><span id="SD_card"></span><span id="sd_card"></span><span id="SD_CARD"></span>SD カード

ユーザーがリムーバブル データのパーティションは、SD カードに格納されたデータを参照します。 SD カードは、特定の種類のユーザー データの格納に使用される別のボリュームとして扱われます。 SD カード上のコンテンツは、システムからユーザーがいつでもと、そのため、電話のコア機能にとって重要な情報を含めることはできません。
 


