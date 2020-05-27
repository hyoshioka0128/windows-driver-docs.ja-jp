---
title: セキュア ブート
description: セキュア ブート
ms.date: 05/22/2020
ms.localizationpriority: medium
ms.openlocfilehash: 24434249c43f48c1eb7383145c1657fd4f47cc47
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851739"
---
# <a name="secure-boot"></a>セキュア ブート

セキュアブートは、pc の製造元によって信頼されているソフトウェアのみを使用して PC が起動されるようにするためのプロセスです。 セキュアブートは Microsoft 専用ではなく、UEFI 仕様ドキュメントで定義されています。ただし、Microsoft では、以下のリンクで特定の要件が定義されています。

PC が起動すると、ファームウェアは、ファームウェアドライバー (オプション Rom) やオペレーティングシステムなど、各ブートソフトウェアの署名を確認します。 署名が適切な場合、PC が起動され、ファームウェアによってオペレーティングシステムに制御が与えられます。

Windows オペレーティングシステムでは、セキュアブートが必要です。Windows 8、8.1、10、および UEFI 仕様のドキュメントの一部でもあります。詳細については、27.1 「UEFI 仕様ドキュメントの[セキュアブート](https://uefi.org/sites/default/files/resources/UEFI_2_3_1_C.pdf)」セクションを参照してください。

セキュアブートの Windows 要件の詳細については、以下の「System.fundamentals.firmware.cs.uefisecureboot.connectedstandby **-1607** 」のリンクにある「**システムの基礎**」を参照してください。

## <a name="related-resources"></a>関連リソース

[ハードウェア セキュリティの検証可能性に関する仕様](https://docs.microsoft.com/windows-hardware/test/hlk/testref/hardware-security-testability-specification)

[Windows ハードウェア互換性プログラムの仕様とポリシー](https://docs.microsoft.com/windows-hardware/design/compatibility/whcp-specifications-policies)

[WHCP-Systems-Specification-1607 (ZIP ダウンロード)](https://go.microsoft.com/fwlink/?linkid=866948)

[セキュアブートとメジャーブート: マルウェアに対する初期ブートコンポーネントのセキュリティ強化](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn653311(v=vs.85))

[Windows 8.1 セキュアブートキーの作成と管理のガイダンス](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/dn747883(v=win.10))
