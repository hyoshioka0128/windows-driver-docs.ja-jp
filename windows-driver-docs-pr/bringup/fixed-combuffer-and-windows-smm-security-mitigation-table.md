---
title: 固定された ComBuffer と Windows SMM Security Mitigation Table (WSMT)
description: 固定された ComBuffer と Windows SMM Security Mitigation Table (WSMT)
ms.date: 05/22/2020
ms.localizationpriority: medium
ms.openlocfilehash: dafaa17592ad7878e9c011c4f005fc87e0731ad6
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851966"
---
# <a name="fixed-combuffer-and-windows-smm-security-mitigation-table-wsmt"></a>固定された ComBuffer と Windows SMM Security Mitigation Table (WSMT)

Windows SMM セキュリティ軽減策の表 (WSMT) は、システムに特定のセキュリティ機能が実装されていることを示すフラグを含む、ACPI 名前空間で説明されている静的テーブルです。

[保護フラグ] フィールドは、システムのファームウェアに特定の BIOS セキュリティの軽減策が存在することを示します。 Windows オペレーティングシステムのサポートされているバージョンは、初期段階で、ACPI インタープリターの開始前に、Windows の SMM セキュリティテーブルで読み込まれます。 Windows オペレーティングシステムでは、これらの SMM 保護フラグの存在に基づいて、特定のセキュリティ機能を有効、無効、または無効にすることができます。

保護フラグ固定された \_ 通信 \_ バッファーおよび通信 \_ バッファーの入れ子になった PTR 保護は、 \_ \_ \_ ファームウェアベンダーによって、システム管理の割り込み (smis) を再設計することによって、MMIO と EFI で割り当てられたメモリを含む領域の "許可" リストに対する読み取りまたは書き込みのみを行います。ポインターが SMM の外部にあることを確認するだけでは十分ではありません。これらは、これらの "安全な" リージョン内である必要があります。これにより、Windows の主力の "ガード" 機能をバイパスできる混乱の deputy になる可能性があります。 上記の保護フラグは、入力の検証とポインターのチェックのみを指し、現在、SMM ページ保護による強制は必要ありません。

WSMT のサポートは、次のバージョンの Windows に含まれています。

- Windows Server Technical Preview 2016

- Windows 10 Version 1607

- Windows 10 Version 1703

## <a name="related-resources"></a>関連リソース

[Windows SMM のセキュリティ対策に関する表 (WSMT)](https://go.microsoft.com/fwlink/p/?LinkId=786943)
