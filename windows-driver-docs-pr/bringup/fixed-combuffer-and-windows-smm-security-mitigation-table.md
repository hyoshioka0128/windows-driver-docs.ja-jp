---
title: 固定 ComBuffer と Windows SMM セキュリティ リスク軽減テーブル (WSMT)
description: 固定 ComBuffer と Windows SMM セキュリティ リスク軽減テーブル (WSMT)
ms.date: 05/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1b573858b60ced40ee8ae2c7e8f302389fabe440
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537768"
---
# <a name="fixed-combuffer-and-windows-smm-security-mitigation-table-wsmt"></a>固定 ComBuffer と Windows SMM セキュリティ リスク軽減テーブル (WSMT)


Windows SMM セキュリティ リスク軽減テーブル (WSMT) は、特定のセキュリティ機能をシステムに実装されていることを示すフラグを含む ACPI 名前空間で説明されている静的なテーブルです。

保護の Flags フィールドでは、システム ファームウェアの BIOS のセキュリティ対策を特定の有無を示します。 サポートされるバージョンの Windows オペレーティング システムを読み、Windows SMM Security テーブルの ACPI インタープリターを開始する前に、初期化中に早い段階。 Windows オペレーティング システムは、有効化、無効にする、またはこれら SMM 保護フラグの有無に基づいて特定のセキュリティ機能を解除機能することができます。

保護フラグ固定\_COMM\_BUFFERS、および通信\_バッファー\_入れ子になった\_PTR\_に、保護がシステム管理割り込み (Smi) の再設計ファームウェア ベンダーに依存読み取りのみまたは書き込みを MMIO EFI に割り当てられたメモリは、リージョンの「許可」リストを実行してください。  ポインターが SMM の外部では、「安全」リージョンである必要がありますのみことを確認するのに十分ではありません。  これは、ため、SMM が混乱の deputy Windows 主力"Guard"機能を使用しないことになることはできません。 上記の保護フラグは、入力検証とポインター チェックのみを参照してくださいし、SMM ページ保護を使用して強制が現在必要としません。

次のバージョンの Windows では、WSMT のサポートが含まれます。

-   Windows Server Technical Preview 2016

-   Windows 10 Version 1607

-   Windows 10 Version 1703

## <a name="related-resources"></a>関連リソース

[Windows SMM セキュリティ緩和策テーブル (WSMT)](https://go.microsoft.com/fwlink/p/?LinkId=786943)


