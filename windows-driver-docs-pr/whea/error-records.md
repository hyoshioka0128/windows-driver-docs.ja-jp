---
title: エラー レコード
description: エラー レコード
ms.assetid: 080da29a-b5cb-45a5-848d-048d9612ee2a
keywords:
- Windows ハードウェアエラーアーキテクチャ WDK、エラーレコード
- WHEA WDK、エラーレコード
- エラー WDK WHEA、エラーレコード
- WDK WHEA のエラーレコード
- エラーレコード形式 WDK WHEA
- エラーレコードヘッダー WDK WHEA
- エラーレコードセクション WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa1ea1c1e4ac6a34690afa23b471e36cbcd6bdc9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844414"
---
# <a name="error-records"></a>エラー レコード


Windows ハードウェアエラーアーキテクチャ (WHEA) は、標準のエラーレコード形式を使用して、すべてのプラットフォームハードウェアエラーを表します。 その結果、システムファームウェア、Windows オペレーティングシステム、およびユーザーモードアプリケーションは、すべて同じエラーレコード形式に基づいてハードウェアエラー報告と復旧メカニズムを設計できます。

WHEA によって使用されるエラーレコードの形式は、「 [Unified Extensible Firmware Interface (UEFI) 仕様](https://go.microsoft.com/fwlink/p/?linkid=69484)のバージョン2.2 の付録 N」で説明されている*一般的なプラットフォームエラーレコード*に基づいています。

次の図は、エラーレコードの一般的な形式を示しています。

![エラーレコードの一般的な形式を示す図](images/whearecord.png)

エラーレコードは、エラーレコードヘッダーの後に1つ以上の固定長エラーレコードセクション記述子が続くもので構成されます。 各エラーレコードセクション記述子には、エラーデータまたは情報データを含む、関連付けられた可変長のエラーレコードセクションがあります。 エラーレコードには、少なくとも1つのエラーレコードセクションが含まれている必要があります。

エラーレコードには、エラーレコードセクションとセクション記述子を動的に追加するための追加のバッファー領域を含めることができます。 追加のバッファー領域を使用して、既存のエラーレコードセクションのサイズを動的に増やすこともできます。

エラーレコードは、 [**whea\_エラー\_レコード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_record)の構造によって記述されます。エラーレコードヘッダーは、 [**whea\_エラー\_レコード\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_record_header)構造によって記述され、エラーレコードのセクション記述子はそれぞれ[**WHEA\_エラー\_レコード\_セクション\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_record_section_descriptor)の構造によって記述されます。

各エラーレコードセクションには、次のセクションの種類のいずれかを指定できます。

<a href="" id="hardware-error-packet"></a>ハードウェアエラーパケット  
このエラーレコードセクションには、エラーを報告した低レベルのハードウェアエラーハンドラー (LLHEH) によってオペレーティングシステムに渡されたハードウェアエラーパケットが含まれています。 このセクションに含まれるデータは、 [WHEA\_エラー\_パケット](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff560465(v=vs.85))構造によって説明されています。

<a href="" id="generic-processor-error"></a>汎用プロセッサエラー  
このエラーレコードセクションには、特定のプロセッサアーキテクチャに固有ではないプロセッサエラーデータが含まれています。 このセクションに含まれるデータは、 [**WHEA\_プロセッサ\_GENERIC\_ERROR\_section**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_processor_generic_error_section)構造体によって説明されています。

<a href="" id="x86-x64-processor-error"></a>x86/x64 プロセッサエラー  
このエラーレコードセクションには、x86 または x64 プロセッサアーキテクチャに固有のプロセッサエラーデータが含まれています。 このセクションに含まれるデータは、 [**WHEA\_XPF\_PROCESSOR\_ERROR\_section**](https://msdn.microsoft.com/library/windows/hardware/ff560655)構造体によって説明されています。 次の図は、プロセッサエラーデータを含むデータ構造が変数 Info メンバーに格納される方法を示しています。 

![プロセッサエラーデータ](images/wheaxpfsection.gif)

<a href="" id="itanium-processor-error"></a>Itanium プロセッサエラー  
このエラーレコードセクションには、Itanium プロセッサアーキテクチャに固有のプロセッサエラーデータが含まれています。 このエラーレコードセクションに含まれるエラーデータの形式の詳細については、「 [Intel Itanium プロセッサファミリシステムアブストラクションレイヤーの仕様](https://go.microsoft.com/fwlink/p/?linkid=72212)」を参照してください。

<a href="" id="itanium-processor-firmware-error-record-reference"></a>Itanium プロセッサファームウェアのエラーレコードの参照  
このエラーレコードセクションには、Itanium プロセッサアーキテクチャに固有のファームウェアエラーレコードへの参照が含まれています。 このエラー記録セクションは、 [**WHEA\_ファームウェア\_エラー\_レコード\_参照**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_firmware_error_record_reference)構造によって記述されています。

<a href="" id="platform-memory-error"></a>プラットフォームメモリエラー  
このエラーレコードセクションには、プラットフォームメモリのエラーデータが含まれています。 このセクションに含まれるデータは、 [**WHEA\_MEMORY\_ERROR\_section**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_memory_error_section)構造体によって説明されています。

<a href="" id="nonmaskable-interrupt"></a>Nonmaskable 割り込み  
このエラーレコードセクションには、nonmaskable interrupt (NMI) データが含まれています。 このセクションに含まれるデータは、 [**WHEA\_NMI\_エラー\_セクション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_nmi_error_section)構造によって説明されています。

<a href="" id="pci-express-error"></a>PCI Express エラー  
このエラーレコードセクションには、PCI Express エラーデータが含まれています。 このセクションに含まれるデータは、 [**WHEA\_PCIEXPRESS\_ERROR\_section**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_pciexpress_error_section)構造体によって説明されています。

<a href="" id="pci-pci-x-bus-error"></a>PCI/PCI-X バスエラー  
このエラーレコードセクションには、PCI/PCI-X バスのエラーデータが含まれています。 このセクションに含まれるデータは、 [**WHEA\_PCIXBUS\_ERROR\_section**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_pcixbus_error_section)構造体によって説明されています。

<a href="" id="pci-pci-x-device-error"></a>PCI/PCI X デバイスエラー  
このエラーレコードセクションには、PCI/PCI デバイスのエラーデータが含まれています。 このセクションに含まれるデータは、 [**WHEA\_PCIXDEVICE\_ERROR\_section**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_pcixdevice_error_section)構造体によって説明されています。

前の一覧のいずれかのセクションの種類に適さない追加のハードウェアエラーデータの場合は、データを格納するようにプラットフォーム固有のエラーレコードセクションを定義できます。 定義されているプラットフォーム固有のエラーレコードセクションの種類ごとに、エラーレコードセクションの種類を識別する対応する GUID を定義する必要があります。 この GUID は、すべての WHEA の**Sectiontype**メンバーに指定されています。 [ **\_レコード\_セクション\_記述子の\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_record_section_descriptor) 、その型のエラーレコードセクションを記述します。

前の一覧のいずれかのセクションの種類または定義されているプラットフォーム固有のエラーレコードセクションには適合しない追加のハードウェアエラーデータがある場合は、データを格納するために一般的なエラーレコードセクションが使用されます。

 

 




