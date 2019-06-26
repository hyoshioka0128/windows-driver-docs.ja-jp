---
title: セキュア ブート
description: セキュア ブート
ms.date: 08/06/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7d7b555b7660de79c9c8367f98a09f46a0986d2e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353957"
---
# <a name="secure-boot"></a>セキュア ブート


セキュア ブートは、お使いの PC は、PC の製造元によって信頼されているソフトウェアのみを使用して起動することを確認するプロセスです。 セキュア ブートでは、Microsoft に限定されていないと、Microsoft は、以下のリンクで定義されている特定の要件を持っている場合は、UEFI 仕様のドキュメントで定義します。

PC を起動、ファームウェア ブート ソフトウェア、ファームウェア ドライバー (オプション Rom) およびオペレーティング システムを含むの各部分の署名によって確認されます。 署名が適切な場合は、PC が再起動、ファームウェア、オペレーティング システムに制御します。

セキュア ブートは Windows オペレーティング システムに必要です。Windows 8、8.1、および 10、およびも UEFI 仕様ドキュメントの一部です。セクションを参照して[27.1 セキュリティで保護された Boot](https://uefi.org/sites/default/files/resources/UEFI_2_3_1_C.pdf)の詳細については、UEFI 仕様のドキュメント。

セキュア ブートの Windows の要件に関する詳細については、次を参照してください。 **System.Fundamentals.Firmware.UEFISecureBoot**で、 **WHCP システム仕様 1607**以下のリンク。

## <a name="related-resources"></a>関連リソース

[ハードウェア セキュリティの検証可能性に関する仕様](https://docs.microsoft.com/windows-hardware/test/hlk/testref/hardware-security-testability-specification)

[Windows ハードウェア互換性プログラムの仕様とポリシー](https://docs.microsoft.com/windows-hardware/design/compatibility/whcp-specifications-policies)

[WHCP システム仕様 1607](https://go.microsoft.com/fwlink/?linkid=866948)

[セキュア ブートとメジャー ブート:マルウェアに対する初期ブート コンポーネントのセキュリティ強化](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn653311(v=vs.85))

[Windows 8.1 のセキュア ブート キーの作成と管理のガイダンス](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/dn747883(v=win.10))



