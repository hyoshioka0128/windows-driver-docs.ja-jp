---
title: WHEA データ型の名前変更
description: WHEA データ型の名前変更
ms.assetid: e2c511a2-fd6e-4c7a-a47f-eb9b9f917bb4
keywords:
- Windows ハードウェア エラー アーキテクチャ WDK、名前が変更されたデータ型
- WHEA WDK、名前が変更されたデータ型
- ハードウェア エラー WDK WHEA、名前が変更されたデータ型
- WDK WHEA の名前が変更されたデータ型
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dbdff7bf7984bae7fa28fb08980a3683522f632f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579560"
---
# <a name="renamed-whea-data-types"></a>WHEA データ型の名前変更


Windows 7 Windows Driver Kit (WDK) でを起動するには、さまざまな WHEA データ型は、WDK の以前のバージョンから変更されています。 WDK の名前付け規則の名前付け規則に一貫性のあるされるため、これらの変更の大半が行われました、*共通プラットフォーム エラー レコード*形式。 この形式がバージョン 2.2 の付録 N で説明されている、 [Unified Extensible Firmware Interface (UEFI) 仕様](https://go.microsoft.com/fwlink/p/?linkid=69484)します。

Windows 7 のこのセクションで示されたデータ型が改訂されていません。 たとえば、list および名前が変更された構造内のメンバーの型変更されていませんが、メンバー自体が変更されました。

新しい開発している場合[プラットフォーム固有のハードウェア エラー ドライバー (PSHED) プラグイン](platform-specific-hardware-error-driver-plug-ins2.md)Windows 7 およびそれ以降のバージョンの WDK で定義されている新しい WHEA データ型の名前を使用します。

既存の PSHED Windows 7 およびそれ以降のバージョンの WDK でプラグインを構築する場合は、前の WHEA データ型の名前を引き続き使用できます。 これを行うには、次を追加、*ソース*プラグインをビルドするために使用するファイル。

`C_DEFINES = $(C_DEFINES) /DWHEA_DOWNLEVEL_TYPE_NAMES`

ただし、既存 PSHED プラグインを強くお勧め WHEA のデータ型は、Windows 7 およびそれ以降のバージョンの WDK で定義されている名前を使用して変更することです。

次の表は、WHEA データ型の前者と新しい名前を一覧表示します。

### <a href="" id="renamed-whea-globally-unique-identifiers--guids-"></a> WHEA の名前が変更されたグローバル一意識別子 (Guid)

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>以前の名前 (Windows 7 よりも前の WDK バージョン)</th>
<th>新しい名前 (Windows 7 の WDK 以降)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IPF_PROCESSOR_SPECIFIC_SECTION_GUID</p></td>
<td><p>IPF_PROCESSOR_ERROR_SECTION_GUID</p></td>
</tr>
<tr class="even">
<td><p>IPF_SAL_RECORD_REFERENCE_SECTION_GUID</p></td>
<td><p>FIRMWARE_ERROR_RECORD_REFERENCE_GUID</p></td>
</tr>
<tr class="odd">
<td><p>PCIEXPRESS_SECTION_GUID</p></td>
<td><p>PCIEXPRESS_ERROR_SECTION_GUID</p></td>
</tr>
<tr class="even">
<td><p>PCIX_BUS_SECTION_GUID</p></td>
<td><p>PCIXBUS_ERROR_SECTION_GUID</p></td>
</tr>
<tr class="odd">
<td><p>PCIX_COMPONENT_SECTION_GUID</p></td>
<td><p>PCIXBUS_ERROR_SECTION_GUID</p></td>
</tr>
<tr class="even">
<td><p>PLATFORM_MEMORY_SECTION_GUID</p></td>
<td><p>MEMORY_ERROR_SECTION_GUID</p></td>
</tr>
<tr class="odd">
<td><p>PROCESSOR_GENERIC_SECTION_GUID</p></td>
<td><p>PROCESSOR_GENERIC_ERROR_SECTION_GUID</p></td>
</tr>
<tr class="even">
<td><p>X86_PROCESSOR_SPECIFIC_SECTION_GUID</p></td>
<td><p>XPF_PROCESSOR_ERROR_SECTION_GUID</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="renamed-whea-defines"></a> 名前が変更された WHEA を定義します

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>以前の名前 (Windows 7 よりも前の WDK バージョン)</th>
<th>新しい名前 (Windows 7 の WDK 以降)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WHEA_SECTION_DESCRIPTOR_REVISION</p></td>
<td><p>WHEA_ERROR_RECORD_SECTION_DESCRIPTOR_REVISION</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="renamed-whea-structures-and-unions"></a> 名前が変更された WHEA 構造体と共用体

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>以前の名前 (Windows 7 よりも前の WDK バージョン)</th>
<th>新しい名前 (Windows 7 の WDK 以降)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WHEA_FIRMWARE_RECORD</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560520" data-raw-source="[&lt;strong&gt;WHEA_FIRMWARE_ERROR_RECORD_REFERENCE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560520)"><strong>WHEA_FIRMWARE_ERROR_RECORD_REFERENCE</strong></a></p></td>
</tr>
<tr class="even">
<td><p>WHEA_GENERIC_PROCESSOR_ERROR</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560607" data-raw-source="[&lt;strong&gt;WHEA_PROCESSOR_GENERIC_ERROR_SECTION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560607)"><strong>WHEA_PROCESSOR_GENERIC_ERROR_SECTION</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>WHEA_GENERIC_PROCESSOR_ERROR_VALIDBITS</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560610" data-raw-source="[&lt;strong&gt;WHEA_PROCESSOR_GENERIC_ERROR_SECTION_VALIDBITS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560610)"><strong>WHEA_PROCESSOR_GENERIC_ERROR_SECTION_VALIDBITS</strong></a></p></td>
</tr>
<tr class="even">
<td><p>WHEA_MEMORY_ERROR</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560565" data-raw-source="[&lt;strong&gt;WHEA_MEMORY_ERROR_SECTION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560565)"><strong>WHEA_MEMORY_ERROR_SECTION</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>WHEA_MEMORY_ERROR_VALIDBITS</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560568" data-raw-source="[&lt;strong&gt;WHEA_MEMORY_ERROR_SECTION_VALIDBITS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560568)"><strong>WHEA_MEMORY_ERROR_SECTION_VALIDBITS</strong></a></p></td>
</tr>
<tr class="even">
<td><p>WHEA_NMI_ERROR</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560571" data-raw-source="[&lt;strong&gt;WHEA_NMI_ERROR_SECTION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560571)"><strong>WHEA_NMI_ERROR_SECTION</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>WHEA_PCIEXPRESS_ERROR</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560576" data-raw-source="[&lt;strong&gt;WHEA_PCIEXPRESS_ERROR_SECTION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560576)"><strong>WHEA_PCIEXPRESS_ERROR_SECTION</strong></a></p></td>
</tr>
<tr class="even">
<td><p>WHEA_PCIEXPRESS_ERROR_VALIDBITS</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560580" data-raw-source="[&lt;strong&gt;WHEA_PCIEXPRESS_ERROR_SECTION_VALIDBITS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560580)"><strong>WHEA_PCIEXPRESS_ERROR_SECTION_VALIDBITS</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>WHEA_PCIXBUS_ERROR</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560583" data-raw-source="[&lt;strong&gt;WHEA_PCIXBUS_ERROR_SECTION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560583)"><strong>WHEA_PCIXBUS_ERROR_SECTION</strong></a></p></td>
</tr>
<tr class="even">
<td><p>WHEA_PCIXBUS_ERROR_VALIDBITS</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560585" data-raw-source="[&lt;strong&gt;WHEA_PCIXBUS_ERROR_SECTION_VALIDBITS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560585)"><strong>WHEA_PCIXBUS_ERROR_SECTION_VALIDBITS</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>WHEA_PCIXDEVICE_ERROR</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560589" data-raw-source="[&lt;strong&gt;WHEA_PCIXDEVICE_ERROR_SECTION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560589)"><strong>WHEA_PCIXDEVICE_ERROR_SECTION</strong></a></p></td>
</tr>
<tr class="even">
<td><p>WHEA_PCIXDEVICE_ERROR_VALIDBITS</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560591" data-raw-source="[&lt;strong&gt;WHEA_PCIXDEVICE_ERROR_SECTION_VALIDBITS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560591)"><strong>WHEA_PCIXDEVICE_ERROR_SECTION_VALIDBITS</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>WHEA_XPF_PROCESSOR_ERROR</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560655" data-raw-source="[&lt;strong&gt;WHEA_XPF_PROCESSOR_ERROR_SECTION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560655)"><strong>WHEA_XPF_PROCESSOR_ERROR_SECTION</strong></a></p></td>
</tr>
<tr class="even">
<td><p>WHEA_XPF_PROCESSOR_ERROR_VALIDBITS</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560657" data-raw-source="[&lt;strong&gt;WHEA_XPF_PROCESSOR_ERROR_SECTION_VALIDBITS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560657)"><strong>WHEA_XPF_PROCESSOR_ERROR_SECTION_VALIDBITS</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 




