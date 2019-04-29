---
title: システムを使用して、ターゲットを CHID を対象とします。
description: システムを使用して、ターゲットを CHID を対象とします。
ms.date: 05/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 05f94ca402648d357df71dafcd799f463d67f7cc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337383"
---
# <a name="target-a-system-using-chid-targeting"></a>システムを使用して、ターゲットを CHID を対象とします。

コンピューターのハードウェア Id (CHID) s をとおして Oem に、Windows 開発者 Kit(WDK) ツール (ComputerHardwareIDs.exe) または使用可能な監査ツールを実行している OEM または ODM によって作成、 [Microsoft OEM ダウンロード サイト](https://www.microsoftoem.com)(ログインが必要です)。

CHIDs はコンピューターのハードウェア Id と、Windows は、目的の対象とする場合の特異性のさまざまなレベルでこれらの Id を使用します。 適切なドライバーがシステムに配信されると、通常の PNP 順位付けに引き継が」の説明に従って[ランク ドライバーをどのように Windows](https://docs.microsoft.com/windows-hardware/drivers/install/how-setup-ranks-drivers--windows-vista-and-later-)、仕入先は、製品ラインにとって意味がある、この問題を回避戦略を作成できます。

提供される情報に基づいて、OEM または ODM ニーズをすべての適切な SMBIOS フィールドには、データが設定されます、 [SMBIOS](smbios.md)次のガイダンスと、 [DMTF SMBIOS 仕様](http://www.dmtf.org/standards/smbios)CHIDs ことを確認するには個々 および一意。

Microsoft は、ファームウェアの更新プログラム パッケージでの一意の ID だけでなく、コンピューターのハードウェア ID (CHID) のターゲット設定を含めることが必要なようになりました**システム**EFI システム リソース テーブル (ESRT)。 [ダウンロード ドライバー発行ワークフローを Windows 10](http://download.microsoft.com/download/B/A/8/BA89DCE0-DB25-4425-9EFF-1037E0BA06F9/windows10_driver_publishing_workflow.docx)ドキュメントには CHIDs 配布を対象とすると、インストール対象とするために使用の詳細な説明が含まれています。

## <a name="related-resources"></a>関連リソース

[パートナー センター](https://docs.microsoft.com/windows-hardware/drivers/dashboard)

[コンピューターのハードウェア Id を指定します。](https://docs.microsoft.com/windows-hardware/drivers/install/specifying-hardware-ids-for-a-computer)

[Windows 10 用のワークフローの発行 Driver をダウンロードします。](http://download.microsoft.com/download/B/A/8/BA89DCE0-DB25-4425-9EFF-1037E0BA06F9/windows10_driver_publishing_workflow.docx)
