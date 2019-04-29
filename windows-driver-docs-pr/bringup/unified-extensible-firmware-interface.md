---
title: 統一された拡張ファームウェア インターフェイス (UEFI)
description: 統一された拡張ファームウェア インターフェイス (UEFI)
ms.date: 05/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5736e2f9b0e135a62483059be3c9cbab5aded93c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337374"
---
# <a name="unified-extensible-firmware-interface-uefi"></a>統一された拡張ファームウェア インターフェイス (UEFI) 


Windows 10 バージョン 1703 (このドキュメントの執筆時点) で、時点では、Microsoft には、UEFI 仕様バージョン 2.3.1c が必要です。 UEFI.org が仕様書を更新し、これらの更新プログラムのソースの改善に継続的にため、この要件が最終的に変更されます。

Microsoft では、2.5 と 2.6 の UEFI 仕様にいくつかの語句のあいまいさがあったとします。 そのためここに更新していないこれらの仕様のバージョン。 ただし、仕様バージョンでは、UEFI のソース コード ツリーには影響しません。 

UEFI のコードを実装するときにメイン ブランチから最新のビットを使用して、最新の UEFI 仕様のドキュメントからのガイダンスを使用して構築された、ソース ブランチがビルドされたことを確認してください。

さまざまなセキュリティ機能に関連する UEFI 仕様ドキュメントで更新されます機能があります。 たとえば、UEFI 仕様 2.6「4.6 EFI 構成テーブルとテーブルのプロパティ」セクションでは 107 ページ具体的にはの追加"EFI_MEMORY_ATTRIBUTES_TABLE"のサポートします。

-   メモリの属性テーブル (MAT):

    -   EFI\_メモリ\_属性\_テーブル。 UEFI ランタイム全体を、このテーブルで記述する必要があります。

    -   すべてのエントリは、EFI の属性を含める必要があります\_メモリ\_RO、EFI\_メモリ\_XP、またはその両方です。 メモリは、読み取り可能かつ実行可能、または書き込み可能かつ非実行可能のいずれかであることが必要です。

時点で、Windows 10 バージョン 1703、セキュア ブート モードに関する UEFI 仕様に最新の更新プログラムは、Windows によって完全にサポートされていません。 今後の Windows の新しいセキュリティで保護のブート モードを調査中ですのサポート リリースします。

## <a name="related-resources"></a>関連リソース

[UEFI 仕様のドキュメント](https://www.uefi.org/specifications)





