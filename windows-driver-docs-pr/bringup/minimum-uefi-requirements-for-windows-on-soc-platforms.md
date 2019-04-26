---
title: SoC プラットフォーム上の Windows に対する最小限の UEFI 要件
description: SoC プラットフォーム上の Windows に対する最小限の UEFI 要件
ms.assetid: 32743d69-83a2-4658-8652-6d624e75e3db
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8cfb1408e1c2d1a19cb9bd0fd2bc25dd22821568
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337596"
---
# <a name="minimum-uefi-requirements-for-windows-on-soc-platforms"></a>SoC プラットフォーム上の Windows に対する最小限の UEFI 要件


統一された Extensible Firmware Interface (UEFI) では、Windows を実行している SoC プラットフォームの必要なブート ファームウェアです。 このセクションでは、SoC プラットフォームで Windows を実行するための UEFI の実装要件について説明します。 監視とこれらの要件への準拠により、Windows の適切な機能を保証は役立ちます。

SoC ベース コンピューティング システムに、いくつかの制限と、この一連の要件が適用されます。 このガイダンスは、従来 netbook のフォーム ファクターとワイヤレスのマルチタッチ専用のモバイル デバイスの両方のサポートにより、Windows の完全な機能のセットを想定しています。 そのため自体にこのようなシステムで広く使用されるテクノロジに制限されます。 このドキュメントでカバーされないテクノロジを実装するシステム、UEFI 仕様を参照してください[UEFI 仕様](https://go.microsoft.com/fwlink/p/?LinkId=218221)します。

Windows では、Unified Extensible Firmware Interface (UEFI) Version 2.3.1 に基づいてまたはそれ以降のファームウェアのリビジョンをサポートします。

**注**  Windows UEFI 2.3.1 で定義されている機能のサブセットをサポートする仕様。 Windows の実装には、ファームウェアのリビジョンをより高いを比較する明示的なチェックはありません。 このドキュメントで説明するために必要なサポートが含まれている場合、オペレーティング システムは、ファームウェアのリビジョンをより高いをサポートします。

 

## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>トピック</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="uefi-requirements-that-apply-to-all-windows-platforms.md" data-raw-source="[UEFI requirements that apply to all Windows editions on SoC platforms](uefi-requirements-that-apply-to-all-windows-platforms.md)">SoC のプラットフォームですべての Windows エディションに適用される UEFI 要件</a></p></td>
<td><p>このトピックでは、デスクトップのエディション (Home、Pro、Enterprise、および Education) および Windows 10 Mobile、Windows 10 に適用される UEFI 要件について説明します。</p></td>
</tr>
<tr class="even">
<td><p><a href="uefi-requirements-specific-to-windows-mobile.md" data-raw-source="[UEFI requirements for Windows 10 Mobile](uefi-requirements-specific-to-windows-mobile.md)">Windows 10 Mobile の UEFI 要件</a></p></td>
<td><p>UEFI 要件だけでなく<a href="uefi-requirements-that-apply-to-all-windows-platforms.md" data-raw-source="[UEFI requirements that apply to all Windows editions](uefi-requirements-that-apply-to-all-windows-platforms.md)">Windows のすべてのエディションに適用される UEFI 要件</a>、Windows 10 Mobile を実行しているデバイスは、このトピックで説明する追加の要件を満たすも必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><a href="uefi-requirements-for-usb-flashing-support.md" data-raw-source="[UEFI requirements for USB flashing support](uefi-requirements-for-usb-flashing-support.md)">USB サポートが点滅の UEFI 要件</a></p></td>
<td><p>Microsoft は、エンジニア リングと、製造環境で使用するためのいくつかの USB ベースの点滅ソリューションを提供します。 これらのツールで使用するデバイスで、デバイスの UEFI 環境は、このトピックに記載の要件を満たす必要があります。</p></td>
</tr>
</tbody>
</table>

 

 

 




