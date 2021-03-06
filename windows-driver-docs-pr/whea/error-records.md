---
title: エラー レコード
description: エラー レコード
ms.assetid: 080da29a-b5cb-45a5-848d-048d9612ee2a
keywords:
- Windows ハードウェア アーキテクチャ WDK のエラー、エラー レコード
- WHEA WDK、エラー レコード
- WDK WHEA、エラー レコードのエラー
- WDK WHEA を記録するエラー
- WDK WHEA エラー レコードの形式
- WDK WHEA エラー レコードのヘッダー
- エラー レコード セクション WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18c8d54f2a454eed32681229b62f2cfd7d10b4e5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362588"
---
# <a name="error-records"></a>エラー レコード


Windows ハードウェア エラー アーキテクチャ (WHEA) では、標準エラー レコードの形式を使用して、すべてのプラットフォームのハードウェア エラーを表します。 その結果、システム ファームウェアでは、Windows オペレーティング システム、およびユーザー モード アプリケーションでは、同じエラー レコードの形式に基づくすべてのハードウェア エラー レポートと回復メカニズムを設計できます。

WHEA で使用されるエラー レコードの形式がに基づいて、*共通プラットフォーム エラー レコード*の version 2.2 の付録 N」の説明に従って、 [Unified Extensible Firmware Interface (UEFI) 仕様](https://go.microsoft.com/fwlink/p/?linkid=69484).

次の図は、エラー レコードの一般的な形式を示します。

![エラー レコードの一般的な形式を示す図](images/whearecord.png)

エラー レコードは、1 つまたは複数の固定長エラー レコード セクション記述子続くエラー レコード ヘッダーで構成されます。 各エラーの記録セクション記述子には、エラー データと情報のデータを含む可変長の関連するエラー レコード セクションがあります。 エラー レコードには、少なくとも 1 つのエラー レコードのセクションを含める必要があります。

エラー レコードには、エラー レコードのセクションとセクション記述子の動的な追加の余分なバッファー領域を含めることができます。 余分なバッファー領域がエラー レコードの既存のセクションのサイズを動的に増加することもできます。

エラー レコードは、 [ **WHEA\_エラー\_レコード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_error_record)構造によってエラー レコードのヘッダーが説明されている、 [ **WHEA\_エラー\_レコード\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_error_record_header)構造、およびエラーの記録セクション記述子がそれぞれで説明されている、 [ **WHEA\_エラー\_レコード\_セクション\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_error_record_section_descriptor)構造体。

各エラー レコード セクションには、次のセクションの種類のいずれかを指定できます。

<a href="" id="hardware-error-packet"></a>ハードウェア エラー パケット  
このエラーの記録セクションには、エラーが報告された低レベル ハードウェア エラー ハンドラー (LLHEH) によって、オペレーティング システムに渡されたハードウェア エラー パケットが含まれています。 このセクションに含まれているデータは、 [WHEA\_エラー\_パケット](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff560465(v=vs.85))構造体。

<a href="" id="generic-processor-error"></a>ジェネリックのプロセッサのエラー  
このエラー レコード セクションには、特定のプロセッサ アーキテクチャに固有ではないプロセッサ エラー データが含まれます。 このセクションに含まれているデータは、 [ **WHEA\_プロセッサ\_ジェネリック\_エラー\_セクション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_processor_generic_error_section)構造体。

<a href="" id="x86-x64-processor-error"></a>x86 または x64 プロセッサのエラー  
このエラー レコード セクションには、x86 または x64 プロセッサ アーキテクチャに固有のプロセッサのエラー データが含まれています。 このセクションに含まれているデータは、 [ **WHEA\_XPF\_プロセッサ\_エラー\_セクション**](https://msdn.microsoft.com/library/windows/hardware/ff560655)構造体。 次の図では、VariableInfo メンバー内のプロセッサのエラー データを含むデータ構造体の格納方法を示します。 

![プロセッサのエラー データ](images/wheaxpfsection.gif)

<a href="" id="itanium-processor-error"></a>Itanium プロセッサのエラー  
このエラー レコード セクションには、Itanium プロセッサ アーキテクチャに固有のプロセッサのエラー データが含まれています。 このエラーの記録セクションに含まれているエラー データの書式設定に関する詳細については、次を参照してください。、 [Intel Itanium プロセッサ ファミリのシステムの抽象化層の仕様](https://go.microsoft.com/fwlink/p/?linkid=72212)します。

<a href="" id="itanium-processor-firmware-error-record-reference"></a>Itanium プロセッサ ファームウェア エラー レコードのリファレンス  
このエラー レコード セクションには、Itanium プロセッサ アーキテクチャに固有のファームウェア エラー レコードへの参照が含まれています。 によってこのエラーの記録セクションが説明されている、 [ **WHEA\_ファームウェア\_エラー\_レコード\_参照**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_firmware_error_record_reference)構造体。

<a href="" id="platform-memory-error"></a>プラットフォーム メモリ エラー  
このエラー レコード セクションには、プラットフォーム メモリ エラーのデータが含まれています。 このセクションに含まれているデータは、 [ **WHEA\_メモリ\_エラー\_セクション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_memory_error_section)構造体。

<a href="" id="nonmaskable-interrupt"></a>マスク不可能割り込み  
このエラー レコード セクションには、マスク不可能割り込み (NMI) データが含まれています。 このセクションに含まれているデータは、 [ **WHEA\_NMI\_エラー\_セクション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_nmi_error_section)構造体。

<a href="" id="pci-express-error"></a>PCI Express エラー  
このエラー レコード セクションには、PCI Express エラー データが含まれています。 このセクションに含まれているデータは、 [ **WHEA\_PCIEXPRESS\_エラー\_セクション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_pciexpress_error_section)構造体。

<a href="" id="pci-pci-x-bus-error"></a>X-PCI/PCI バス エラー  
このエラーの記録セクションには、X-PCI/PCI バス エラー データが含まれています。 このセクションに含まれているデータは、 [ **WHEA\_PCIXBUS\_エラー\_セクション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_pcixbus_error_section)構造体。

<a href="" id="pci-pci-x-device-error"></a>X-PCI/PCI デバイス エラー  
このエラーの記録セクションには、PCI/PCI-x デバイス エラー データが含まれています。 このセクションに含まれているデータは、 [ **WHEA\_PCIXDEVICE\_エラー\_セクション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_pcixdevice_error_section)構造体。

前の一覧にセクションの種類のいずれかに適合しない追加のハードウェア エラー データ、データを格納するプラットフォーム固有のエラー レコードのセクションを定義できます。 プラットフォーム固有のエラー レコードで定義されているエラーの種類を識別するための対応する GUID の種類ごとにレコードのセクションを定義する必要があります。 この GUID がで指定された、 **SectionType**いずれかのメンバー [ **WHEA\_エラー\_レコード\_セクション\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_error_record_section_descriptor)エラー レコードのセクションの型を記述する構造体。

前の一覧にセクションの種類のいずれかにまたは定義されているプラットフォーム固有のエラー レコード セクションには適合しない追加のハードウェア エラーのデータがある場合は、一般的なエラー レコードのセクションがデータを格納する使用されます。

 

 




